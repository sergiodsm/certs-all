# Module 01 — CLI Foundation

## In one sentence

OpenWrt exposes a BusyBox **ash** shell where almost all persistent settings live in **UCI config files** under `/etc/config/`, applied by init scripts and **procd**.

## Why it exists

Embedded routers have limited flash and RAM. OpenWrt avoids heavy daemons with separate config formats. One syntax (`uci`) feeds LuCI, shell scripts, and automation equally.

## Mental model

```text
  You (SSH/serial)
        │
        ▼
   ash shell + uci
        │
        ▼
  /etc/config/*  ──commit──►  procd / netifd / hostapd / fw4
        │
        ▼
   Running kernel + netlink (ip, wireless, nftables)
```

## Shell environment

OpenWrt uses **ash** (Almquist shell), not bash. Implications:

| Feature | ash on OpenWrt | bash |
|---------|------------------|------|
| Arrays | Limited | Full |
| `[[ ]]` | No — use `[ ]` | Yes |
| `source` | Use `. file` | Both |
| History | Basic | Rich |

```sh
# Current shell
echo $SHELL          # often /bin/ash

# Environment
env | grep -E 'PATH|HOME|USER'
echo $PATH           # /usr/sbin:/usr/bin:/sbin:/bin

# Root is the normal admin account
whoami               # root
```

## Critical paths

| Path | Purpose |
|------|---------|
| `/etc/config/` | UCI configuration (network, wireless, firewall, system, …) |
| `/etc/init.d/` | Service start/stop scripts |
| `/etc/rc.d/` | Symlinks — enable/disable at boot (S## / K##) |
| `/etc/hotplug.d/` | Scripts triggered by kernel hotplug events |
| `/overlay/` | Writable layer (extroot moves this to USB) |
| `/tmp/` | RAM-backed — lost on reboot |
| `/lib/functions/` | Shell helpers sourced by init scripts |

## Service control syntax

Every major service has an init script:

```sh
# Syntax
/etc/init.d/<name> <action>

# Actions (most services)
start | stop | restart | reload | enable | disable | enabled

# Examples
/etc/init.d/network restart
/etc/init.d/firewall reload
/etc/init.d/dropbear restart
/etc/init.d/dnsmasq reload
/etc/init.d/wireless reload    # alias; often use: wifi reload
```

**Enable vs start:**

```sh
/etc/init.d/dropbear enable     # run at boot (creates /etc/rc.d/S50dropbear)
/etc/init.d/dropbear start      # run now only
/etc/init.d/dropbear enabled    # prints 0 if enabled, 1 if not
```

## ubus — internal message bus

Daemons expose status and actions via **ubus** (similar in spirit to D-Bus, lighter).

```sh
# List all objects
ubus list

# Network interface status (JSON)
ubus call network.interface.lan status

# All interfaces
ubus call network.interface dump

# System info
ubus call system board
ubus call system info

# Wireless (if hostapd exposes it)
ubus list | grep wireless
```

Use **ubus** for *runtime state*; use **uci** for *persistent config*.

## uci vs direct file edit

| Method | When to use |
|--------|-------------|
| `uci` commands | Always for production changes — validates syntax |
| `vi /etc/config/network` | Emergency recovery, bulk edits, then `uci commit` |
| LuCI | Quick GUI — still writes UCI underneath |

**Rule:** After manual file edits:

```sh
uci changes          # show uncommitted diffs
uci commit network   # apply to /etc/config/network on disk
/etc/init.d/network restart
```

## Basic read-only inspection

```sh
# OpenWrt version
cat /etc/openwrt_release

# Kernel / hardware
uname -a
cat /proc/cpuinfo
free
df -h

# Running processes
ps w | grep -E 'netifd|hostapd|dnsmasq|dropbear|fw4'

# Listening ports
netstat -tulpn 2>/dev/null || ss -tulpn
```

## Serial / first-login access

If IP is unknown:

```sh
# On serial console (115200 8N1 typical)
# Login: root, blank password on fresh install — set immediately:
passwd
```

## Common mistakes

1. **Editing `/etc/config` without commit or restart** — changes on disk may not match running state until service reload.
2. **Assuming bash** — scripts fail on `[[`, arrays, or bashisms.
3. **Writing to `/tmp` expecting persistence** — it is tmpfs.
4. **Using `ifconfig`** — prefer `ip`; OpenWrt aligns with iproute2.

## Check your understanding

1. What is the difference between `ubus call network.interface.lan status` and `uci show network.lan`?
2. What does `/etc/init.d/dropbear enable` do that `start` alone does not?

## Bridge to Module 02

Everything persistent flows through **UCI**. Module 02 is the syntax reference you will use in every subsequent lab.
