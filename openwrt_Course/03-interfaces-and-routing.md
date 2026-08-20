# Module 03 — Interfaces & Routing

## In one sentence

OpenWrt **interfaces** are logical L3 configs bound to **devices** (physical ports, bridges, VLANs) and managed by **netifd**.

## Key packages and commands

| Task | UCI / command |
|------|----------------|
| Show config | `uci show network` |
| Runtime status | `ubus call network.interface.lan status` |
| Quick status | `ifstatus lan` |
| IP addresses | `ip addr show` |
| Routes | `ip route show` |
| Links | `ip link show` |
| Restart networking | `/etc/init.d/network restart` |
| Reload (soft) | `/etc/init.d/network reload` |

## Interface section syntax

```sh
config interface 'lan'
    option device 'br-lan'       # L2 master
    option proto 'static'        # static | dhcp | dhcpv6 | pppoe | none
    option ipaddr '192.168.1.1'
    option netmask '255.255.255.0'
    option gateway '192.168.1.254'   # rarely on LAN
    option dns '8.8.8.8'
    option delegate '0'          # IPv6: accept RA on this iface
```

### proto values (most common)

| proto | Use case |
|-------|----------|
| `static` | LAN, management, fixed WAN |
| `dhcp` | Cable/ISP DHCP WAN |
| `dhcpv6` | IPv6 WAN via DHCPv6 |
| `pppoe` | DSL/fiber PPPoE |
| `none` | Bridge member only (no IP on iface) |
| `wireguard` | VPN tunnel (needs extra options) |

## Device & bridge syntax (DSA / modern)

OpenWrt 21+ uses **device** sections for bridges and VLANs:

```sh
# Bridge
config device
    option name 'br-lan'
    option type 'bridge'
    list ports 'lan1'
    list ports 'lan2'
    list ports 'lan3'

# VLAN on DSA switch (example — names vary by board)
config device
    option name 'lan1.10'
    option ifname 'lan1'
    option vid '10'

config interface 'vlan10'
    option device 'lan1.10'
    option proto 'static'
    option ipaddr '10.10.10.1'
    option netmask '255.255.255.0'
```

Legacy **swconfig** switches use `config switch` / `switch_vlan` — check your device:

```sh
swconfig list
# or
ls /proc/switch/
```

## WAN static configuration

```sh
uci set network.wan.proto='static'
uci set network.wan.device='eth1'      # board-specific
uci set network.wan.ipaddr='203.0.113.2'
uci set network.wan.netmask='255.255.255.0'
uci set network.wan.gateway='203.0.113.1'
uci delete network.wan.dns
uci add_list network.wan.dns='1.1.1.1'
uci add_list network.wan.dns='8.8.8.8'
uci commit network
/etc/init.d/network restart
```

## WAN DHCP (client)

```sh
uci set network.wan.proto='dhcp'
uci delete network.wan.ipaddr
uci delete network.wan.netmask
uci delete network.wan.gateway
uci commit network
/etc/init.d/network restart
ifstatus wan
```

## PPPoE syntax

```sh
uci set network.wan.proto='pppoe'
uci set network.wan.device='eth1'
uci set network.wan.username='user@isp'
uci set network.wan.password='secret'
uci set network.wan.ipv6='auto'        # if ISP offers IPv6
uci commit network
/etc/init.d/network restart
logread -e pppd
```

## Multiple IP addresses (alias)

```sh
uci add network alias
uci set network.@alias[-1].interface='lan'
uci set network.@alias[-1].device='br-lan'
uci set network.@alias[-1].ipaddr='192.168.1.2'
uci set network.@alias[-1].netmask='255.255.255.0'
uci commit network
/etc/init.d/network restart
```

Or use list on interface (some setups):

```sh
uci add_list network.lan.ipaddr='192.168.1.2/24'
```

## Static routes

```sh
config route
    option interface 'wan'
    option target '10.0.0.0'
    option netmask '255.0.0.0'
    option gateway '203.0.113.1'
```

CLI:

```sh
uci add network route
uci set network.@route[-1].interface='wan'
uci set network.@route[-1].target='10.0.0.0'
uci set network.@route[-1].netmask='255.0.0.0'
uci set network.@route[-1].gateway='203.0.113.1'
uci commit network
/etc/init.d/network restart
ip route show
```

## Policy routing (advanced)

```sh
config rule
    option priority '100'
    option mark '0x1'
    option lookup '100'

config route
    option table '100'
    option interface 'wan'
    option target '0.0.0.0'
    option netmask '0.0.0.0'
    option gateway '203.0.113.1'
```

## Runtime inspection

```sh
# JSON: addresses, uptime, errors
ubus call network.interface.wan status | jsonfilter -e '@.ipv4-address[0].address'

# Shell-friendly
ifstatus wan

# Physical mapping
ip -br link
bridge link show

# Which device is WAN?
uci get network.wan.device
```

## DNS on interface

```sh
uci delete network.wan.dns
uci add_list network.wan.dns='9.9.9.9'
uci commit network
/etc/init.d/network restart
```

Resolver on router itself uses `/tmp/resolv.conf.d/` — often populated by netifd from WAN DHCP.

## MTU / metrics

```sh
uci set network.wan.mtu='1492'          # PPPoE common
uci set network.wan.metric='10'
uci commit network
/etc/init.d/network restart
```

## Troubleshooting workflow

```sh
# 1. Config vs runtime
uci show network.wan
ifstatus wan

# 2. Link up?
ip link show dev eth1

# 3. DHCP client running?
logread -e netifd
logread -e odhcp6c

# 4. Ping from router
ping -c 3 203.0.113.1
ping -c 3 -I br-lan 192.168.1.50
```

## Common mistakes

1. **Bridging WAN into LAN** — creates loops and bypasses firewall NAT.
2. **Wrong `device` name** — use `ip link` and board docs; `eth0` vs `lan1` differs.
3. **Changing LAN IP without updating DHCP** — align `dhcp.lan` subnet or clients lose access.
4. **Restart during SSH on same subnet change** — use serial or schedule `sleep 5 && reboot`.

## Lab exercise

Create a dedicated management VLAN interface `192.168.99.1/24` on VLAN ID 99 — adapt port names to your hardware.

## Bridge to Module 04

Interfaces carry IP; **wireless** binds 802.11 to those bridges. Next: `wireless` package and `wifi` commands.
