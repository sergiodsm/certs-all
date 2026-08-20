# OpenWrt CLI Mastery Course

A hands-on course for network engineers and homelab operators who need to configure, troubleshoot, and automate OpenWrt **from the command line** — without relying on LuCI.

## Who This Course Is For

- Network admins moving from Cisco/Juniper/enterprise gear to OpenWrt
- Homelab builders who want reproducible, scriptable router configs
- Anyone preparing for real-world OpenWrt support (ISP CPE, travel routers, APs)

## Prerequisites

- Basic TCP/IP (IPv4 subnets, default gateway, DNS)
- Comfort with SSH and a Linux-like shell
- An OpenWrt device or VM (x86/ARM) — physical or [QEMU](https://openwrt.org/doc/howto/qemu)

## Learning Path

| # | Module | Focus |
|---|--------|-------|
| 01 | [CLI Foundation](./01-cli-foundation.md) | Shell, paths, init scripts, `ubus`, mental model |
| 02 | [UCI Syntax](./02-uci-syntax.md) | **Core priority** — read, write, commit, batch |
| 03 | [Interfaces & Routing](./03-interfaces-and-routing.md) | `network` config, bridges, VLANs, static/DHCP WAN |
| 04 | [Wireless](./04-wireless.md) | `wireless` config, radios, AP/STA, encryption |
| 05 | [Firewall & NAT](./05-firewall-and-nat.md) | Zones, forwarding, port forwards, rules |
| 06 | [DHCP & DNS](./06-dhcp-and-dns.md) | `dnsmasq`, leases, static hosts, DNS forwarding |
| 07 | [Users, SSH & Access](./07-users-ssh-and-access.md) | `dropbear`, keys, passwords, sudo-less root |
| 08 | [IPv6](./08-ipv6.md) | RA, DHCPv6-PD, static v6, firewall6 |
| 09 | [Packages & Services](./09-packages-and-services.md) | `opkg`, procd, hotplug, persistence |
| 10 | [Diagnostics & Troubleshooting](./10-diagnostics-and-troubleshooting.md) | Logs, `tcpdump`, connectivity workflow |
| — | [Quick Reference Cheatsheet](./CHEATSHEET.md) | One-page command summary |

## Recommended Study Order

1. **Modules 01 → 02** — Without UCI, nothing else on OpenWrt makes sense.
2. **Modules 03 → 04** — Layer-2/Layer-3 and WiFi (most common day-one tasks).
3. **Modules 05 → 06** — Edge security and client services.
4. **Modules 07 → 08** — Remote access and dual-stack.
5. **Modules 09 → 10** — Operations and break-fix.

## Lab Environment Setup

```sh
# From your PC — replace 192.168.1.1 with your router IP
ssh root@192.168.1.1

# Confirm OpenWrt
cat /etc/openwrt_release

# Snapshot before labs (optional, if you have extroot/overlay space)
sysupgrade -b /tmp/backup-$(date +%F).tar.gz
```

## Course Philosophy

OpenWrt is not "Linux with a web UI." It is a **declarative configuration system** (UCI) interpreted by **netifd**, **hostapd/wpa_supplicant**, **fw4**, and **procd**. The CLI teaches you that pipeline; LuCI hides it.

Master the syntax in Module 02, then every later module becomes pattern recognition.

## Version Notes

Examples target **OpenWrt 23.05+ / 24.x** with **fw4** (nftables) and **apk/opkg** depending on release. Commands note differences where relevant. Always verify on your device:

```sh
. /etc/openwrt_release && echo "$DISTRIB_RELEASE"
```
