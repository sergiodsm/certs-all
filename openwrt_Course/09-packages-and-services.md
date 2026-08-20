# Module 09 — Packages & Services

## In one sentence

OpenWrt extends the base system with **opkg** (or **apk** on newer snapshots) and manages daemons through **procd** init scripts in `/etc/init.d/`.

## Package manager syntax

### opkg (23.05 and most releases)

```sh
opkg update                              # refresh package lists
opkg list-installed
opkg list | grep tcpdump
opkg info luci
opkg install tcpdump
opkg install luci-ssl                    # LuCI with HTTPS
opkg remove tcpdump
opkg upgrade <pkg>                       # upgrade single package
opkg upgrade                             # upgrade all installed (careful)
opkg find '*wireguard*'
opkg files tcpdump                       # which files package installed
opkg search /usr/sbin/tcpdump
```

Flags:

```sh
opkg install --force-reinstall tcpdump
opkg install --nodeps some-package       # risky — skip dependencies
```

### apk (OpenWrt SNAPSHOT / future)

Some builds use **apk** instead of opkg:

```sh
apk update
apk add tcpdump
apk del tcpdump
apk list -I
```

Check which you have:

```sh
which opkg apk 2>/dev/null
```

## Storage and overlay

```sh
df -h
mount | grep overlay
du -sh /overlay/*
```

If `opkg install` fails with **no space**:

```sh
# Remove unused packages
opkg list-installed
opkg remove <large-unused-pkg>

# Or extroot to USB — see OpenWrt wiki extroot guide
```

## Service lifecycle (procd)

```sh
/etc/init.d/<service> start|stop|restart|reload|enable|disable|enabled|running

# Examples
/etc/init.d/network restart
/etc/init.d/firewall reload
/etc/init.d/dropbear restart
/etc/init.d/dnsmasq reload
/etc/init.d/odhcpd restart
/etc/init.d/sysntpd restart
/etc/init.d/log restart
```

Trace boot order:

```sh
ls -la /etc/rc.d/
```

## system configuration

`/etc/config/system`:

```sh
uci show system

uci set system.@system[0].hostname='router-home'
uci set system.@system[0].timezone='UTC'
uci set system.@system[0].zonename='UTC'
uci commit system
/etc/init.d/system restart

# NTP
uci set system.ntp.enabled='1'
uci add_list system.ntp.server='pool.ntp.org'
uci commit system
/etc/init.d/sysntpd restart
```

## Scheduled tasks (cron)

```sh
crontab -l
crontab -e    # vi-based

# Example: reboot weekly
echo "0 4 * * 0 /sbin/reboot" >> /etc/crontabs/root
/etc/init.d/cron restart
```

## Config persistence

| Persists reboot | Lost on reboot |
|-----------------|------------------|
| `/etc/config/*` (after uci commit) | `/tmp/*` |
| `/etc/dropbear/authorized_keys` | Uncommitted uci changes |
| `/root/*` scripts | Runtime iptables/nft manual |
| `/etc/hosts` (if on overlay) | `ps` processes |

Backup:

```sh
sysupgrade -b /tmp/backup-$(date +%F).tar.gz
scp root@192.168.1.1:/tmp/backup-*.tar.gz .
```

Restore:

```sh
sysupgrade -r /tmp/backup.tar.gz
```

## Firmware upgrade

```sh
# Download image to /tmp first
sysupgrade -v /tmp/openwrt-*-sysupgrade.bin

# Keep settings
sysupgrade -v /tmp/firmware.bin

# Factory reset upgrade
sysupgrade -n -v /tmp/firmware.bin
```

## Hotplug

USB, button, net events run scripts in `/etc/hotplug.d/`:

```sh
ls /etc/hotplug.d/net/
ls /etc/hotplug.d/usb/
```

Example: interface up notification — used internally by netifd.

## Common optional packages

| Package | Purpose |
|---------|---------|
| `tcpdump-mini` | Packet capture |
| `iperf3` | Throughput testing |
| `curl` | HTTP tests |
| `jq` / `jsonfilter` | Parse JSON (ubus) |
| `wireguard-tools` | WireGuard VPN |
| `luci-app-wireguard` | LuCI for WG |
| `sqm-scripts` | Smart queue management / SQM |
| `vnstat` | Traffic accounting |

```sh
opkg update && opkg install tcpdump-mini iperf3 curl jsonfilter
```

## LED / button (system)

```sh
uci show system | grep led
# Board-specific — see /etc/config/system
```

## Resource limits

```sh
free
cat /proc/meminfo
top -bn1 | head -20
logd -S 64    # log buffer size KB — /etc/config/system log_size
```

## Common mistakes

1. **`opkg upgrade` blindly** — can break kernel/module match; prefer full sysupgrade image.
2. **Installing LuCI on 4MB flash** — fails; need larger device or build without LuCI.
3. **Forgetting `enable` after install** — package installed but not started at boot.
4. **Mixing opkg and apk** on wrong release — use one package manager per image.

## Lab exercise

Install `tcpdump-mini` and `jsonfilter`. Capture DNS on `br-lan` for 30 seconds while resolving from a client.

## Bridge to Module 10

When something breaks, diagnostics tie everything together.
