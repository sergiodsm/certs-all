# Module 02 — UCI Syntax (Priority)

## In one sentence

**UCI** (Unified Configuration Interface) is OpenWrt's typed key-value configuration API for files in `/etc/config/`, with staged changes until you **commit**.

## Why it exists

One config format for CLI, LuCI, and backup/restore. Services read UCI via shell hooks or libraries; you never need to learn per-daemon config syntax for basic tasks.

## Config file anatomy

Example `/etc/config/network`:

```sh
config interface 'lan'
    option device 'br-lan'
    option proto 'static'
    option ipaddr '192.168.1.1'
    option netmask '255.255.255.0'

config device
    option name 'br-lan'
    option type 'bridge'
    list ports 'lan1'
    list ports 'lan2'
```

| UCI term | File syntax | Meaning |
|----------|-------------|---------|
| Package | Filename | `network`, `wireless`, `firewall` → `/etc/config/<package>` |
| Section | `config <type> '<name>'` | One record (interface, zone, wifi-iface) |
| Option | `option key 'value'` | Scalar setting |
| List | `list key 'value'` | Repeatable values |

Section **type** (`interface`, `device`, `zone`) is what scripts match. Section **name** (`lan`, `wan`) is the human ID.

## Command reference — read

```sh
# Show entire package
uci show network

# Show one section (anonymous sections use @type[index])
uci show network.lan

# Get single option (returns value only)
uci get network.lan.ipaddr

# Get list (returns multiple lines)
uci get network.@device[0].ports

# Quiet check exit code
uci -q get network.lan.ipaddr && echo "exists"

# Show uncommitted changes (runtime vs disk)
uci changes
uci changes network
```

**Anonymous sections:** `@device[0]` = first `config device` block; index is 0-based in CLI.

```sh
# Find index of a named section
uci show network | grep "=interface" 
# network.lan=interface  → use network.lan
# network.@device[0]=device → anonymous
```

## Command reference — write

```sh
# Set scalar option (creates option if missing)
uci set network.lan.ipaddr='192.168.10.1'

# Set on anonymous section
uci set network.@device[0].name='br-lan'

# Add to list (duplicate values allowed unless service dedups)
uci add_list network.@device[0].ports='lan3'

# Remove one list entry
uci del_list network.@device[0].ports='lan3'

# Delete entire option
uci delete network.lan.ip6assign

# Delete entire section
uci delete network.guest
```

## Command reference — create sections

```sh
# Add new anonymous section; prints section ID like cfg0abc12
NEW=$(uci add network interface)
uci rename network.$NEW='guest'
uci set network.guest.proto='static'
uci set network.guest.device='br-guest'
uci set network.guest.ipaddr='192.168.50.1'
uci set network.guest.netmask='255.255.255.0'

# Add typed section with name in one step (OpenWrt 21+)
uci set network.guest=interface
uci set network.guest.proto='static'
```

```sh
# Reorder sections (rare — some packages care about order)
uci reorder network.guest=5
```

## Command reference — commit & revert

Changes exist in **runtime UCI state** until committed:

```sh
# Preview
uci changes

# Commit one package to /etc/config/<package>
uci commit network

# Commit all changed packages
uci commit

# Discard uncommitted changes for a package
uci revert network

# Discard everything pending
uci revert
```

**Workflow (always follow):**

```sh
uci set ...
uci commit network
/etc/init.d/network restart
```

## Batch mode — automation syntax

For scripts, use **batch** to apply many commands atomically:

```sh
uci batch <<'EOF'
set network.lan.ipaddr='192.168.1.1'
set network.lan.netmask='255.255.255.0'
delete network.wan6
EOF
uci commit network
/etc/init.d/network restart
```

Or from file:

```sh
uci batch < /tmp/my-changes.txt
uci commit
```

Batch errors abort the batch; nothing partial is applied from that batch invocation.

## Export / import

```sh
# Export package as UCI commands
uci export network > /tmp/network.uci

# Import (applies to runtime; still need commit)
uci import network < /tmp/network.uci
uci commit network
```

Full backup:

```sh
sysupgrade -b /tmp/backup.tar.gz   # includes /etc/config
```

## Defaults and validation

```sh
# Reset package to image defaults (destructive)
uci revert network
# Or reinstall defaults:
cp /rom/etc/config/network /etc/config/network
/etc/init.d/network restart
```

`/rom` is read-only squashfs baseline.

## Package-specific naming patterns

| Package | Section types | Named examples |
|---------|---------------|----------------|
| `network` | `interface`, `device`, `switch`, `route`, `rule` | `lan`, `wan`, `br-lan` |
| `wireless` | `wifi-device`, `wifi-iface` | `radio0`, `default_radio0` |
| `firewall` | `defaults`, `zone`, `forwarding`, `rule`, `redirect`, `nat` | `@zone[0]`, `lan`, `wan` |
| `dhcp` | `dnsmasq`, `dhcp`, `host`, `domain` | `lan`, `@dnsmasq[0]` |
| `dropbear` | `dropbear` | `@dropbear[0]` |
| `system` | `system`, `timeserver`, `led` | `@system[0]` |

## Shell scripting patterns

```sh
#!/bin/sh
. /lib/functions.sh   # OpenWrt helpers

# Safe get with default
ipaddr=$(uci -q get network.lan.ipaddr || echo "192.168.1.1")

# Iterate list options
idx=0
while uci -q get network.@device[$idx] >/dev/null 2>&1; do
    echo "device $idx: $(uci get network.@device[$idx].name)"
    idx=$((idx + 1))
done

# config_get from /lib/functions/network.sh
. /lib/functions/network.sh
config_load network
config_get proto lan proto
echo "LAN proto: $proto"
```

## LuCI ↔ UCI mapping

LuCI "Save & Apply" = `uci commit` + service reload. "Save" only = commit without reload (depending on page). Learn UCI and LuCI stops being magic.

## Common mistakes

1. **Forgot `uci commit`** — reboot loses changes.
2. **Wrong section index** — `@device[1]` after delete shifts indices; prefer named sections.
3. **Quotes** — values with spaces must be quoted: `'My SSID Name'`.
4. **Restart wrong service** — `network` changes need `network restart`; wireless often `wifi reload`.
5. **Duplicate list entries** — `add_list` twice adds two; use `del_list` first.

## Lab exercises

**Lab 2.1 — Change LAN IP**

```sh
uci set network.lan.ipaddr='192.168.10.1'
uci commit network
/etc/init.d/network restart
# Reconnect SSH to 192.168.10.1
```

**Lab 2.2 — Add guest interface section**

```sh
uci set network.guest=interface
uci set network.guest.proto='static'
uci set network.guest.device='br-guest'
uci set network.guest.ipaddr='192.168.50.1'
uci set network.guest.netmask='255.255.255.0'
uci commit network
/etc/init.d/network restart
uci show network.guest
```

**Lab 2.3 — Rollback**

```sh
uci set network.lan.ipaddr='192.168.99.1'
uci changes
uci revert network
uci get network.lan.ipaddr    # back to previous committed value
```

## Check your understanding

1. Write the three commands to change WAN from DHCP to static IP `203.0.113.2/24` gateway `203.0.113.1`.
2. What is the difference between `uci delete` and `uci revert`?

## Bridge to Module 03

You can now read and write any OpenWrt setting. Module 03 applies this to **interfaces, bridges, and routing**.
