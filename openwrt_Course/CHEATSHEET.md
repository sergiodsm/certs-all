# OpenWrt CLI — Quick Reference Cheatsheet

One-page syntax priority list for daily operations.

---

## UCI (always commit)

```sh
uci show [package]                    # read all
uci get network.lan.ipaddr            # read one
uci set network.lan.ipaddr='x'        # write
uci add_list network.wan.dns='8.8.8.8'
uci del_list network.wan.dns='8.8.8.8'
uci delete network.guest              # delete section
uci add network interface             # new section
uci rename network.@interface[-1]='guest'
uci changes                           # pending
uci commit [package]                  # save to disk
uci revert [package]                  # undo pending
uci batch <<'EOF' ... EOF             # script bulk
uci export network > backup.uci
```

---

## Services

```sh
/etc/init.d/<name> {start|stop|restart|reload|enable|disable}
# network firewall dnsmasq dropbear odhcpd wireless(sys alias: wifi)
wifi reload | wifi status
```

---

## Network

```sh
ifstatus lan|wan|wan6
ubus call network.interface.lan status
ip -br addr ; ip route ; ip -6 route
uci show network
```

**Static LAN:** `proto static`, `ipaddr`, `netmask`, `device`  
**DHCP WAN:** `proto dhcp`  
**PPPoE:** `proto pppoe`, `username`, `password`  
**Bridge:** `config device` + `type bridge` + `list ports`

---

## Wireless

```sh
uci show wireless
wifi reload ; wifi status ; iwinfo
```

**Radio:** `wifi-device` → `channel`, `band`, `htmode`, `country`  
**SSID:** `wifi-iface` → `mode ap|sta`, `ssid`, `encryption`, `key`, `network`  
**Crypto:** `none`, `psk2`, `sae`, `sae-mixed`, `wpa2`

---

## Firewall

```sh
uci show firewall
/etc/init.d/firewall restart
nft list ruleset
```

**Zone:** `name`, `list network`, `input|output|forward`, `masq`  
**Forward LAN→WAN:** `config forwarding` src lan dest wan  
**Port forward:** `config redirect` → DNAT  
**Open port:** `config rule` → ACCEPT

---

## DHCP / DNS

```sh
uci show dhcp
cat /tmp/dhcp.leases
/etc/init.d/dnsmasq reload
```

**Pool:** `start`, `limit`, `leasetime`  
**Reservation:** `config host` + `mac` + `ip`  
**IPv6 RA:** `ra server`, `dhcpv6 server`, `ra_slaac 1`

---

## SSH / Users

```sh
passwd
uci show dropbear
/etc/init.d/dropbear restart
# keys: /etc/dropbear/authorized_keys
```

**Harden:** `PasswordAuth off`, `RootPasswordAuth off`, `Interface lan`

---

## IPv6

```sh
ifstatus wan6
ip -6 addr ; ip -6 route
logread -e odhcpd
```

**WAN:** `wan6` + `proto dhcpv6` + `reqprefix auto`  
**LAN:** `ip6assign 64`, `delegate 1`  
**Disable v6 LAN:** `ra disabled`, `dhcpv6 disabled`

---

## Packages & system

```sh
opkg update && opkg install <pkg>
opkg list-installed
sysupgrade -b /tmp/backup.tar.gz
uci set system.@system[0].hostname='name'
logread -e <daemon>
```

---

## Diagnostics

```sh
logread | tail -50
dmesg
ping -c 3 8.8.8.8
nslookup openwrt.org 127.0.0.1
tcpdump -i br-lan -n port 53
ps w ; ss -tulpn
ubus list
```

---

## Typical change workflow

```sh
uci set ...
uci commit <package>
/etc/init.d/<service> restart   # or reload / wifi reload
ifstatus <iface>                # verify
logread -e <daemon>             # if broken
```

---

## Emergency

```sh
# Failsafe / serial
mount_root
uci revert network
uci set dropbear.@dropbear[0].PasswordAuth='on'
uci commit
reboot

firstboot -y && reboot now        # factory reset
```

---

See full course: [README](./README.md)
