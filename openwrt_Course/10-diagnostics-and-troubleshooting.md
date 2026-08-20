# Module 10 — Diagnostics & Troubleshooting

## In one sentence

OpenWrt troubleshooting moves from **symptom → layer (L2/L3/DNS/firewall/service) → UCI vs runtime mismatch → logs**.

## The universal workflow

```text
1. What changed? (uci changes, upgrade, new package)
2. uci show <package>     — intended config
3. ubus / ifstatus        — runtime state
4. logread                — daemon errors
5. ip / ping / traceroute — datapath
6. tcpdump                — packet proof
```

## Logging

```sh
logread                  # full buffer
logread -e netifd        # filter substring
logread -f               # follow (like tail -f)
logread | tail -50

dmesg
dmesg | tail -30

# Increase buffer (temporary)
logread -S 128
uci set system.@system[0].log_size='128'
uci commit system
/etc/init.d/log restart
```

Remote syslog:

```sh
uci set system.@system[0].log_ip='192.168.1.10'
uci set system.@system[0].log_port='514'
uci set system.@system[0].log_proto='udp'
uci commit system
/etc/init.d/log restart
```

## Config drift detection

```sh
uci changes
diff /rom/etc/config/network /etc/config/network   # vs factory
```

## Network diagnostics

```sh
# Interface summary
ifstatus lan
ifstatus wan
ubus call network.interface dump

# Addresses and routes
ip -br addr
ip route
ip -6 route

# Link / bridge
ip link
bridge link show

# ARP / neighbors
ip neigh show

# DNS from router
nslookup openwrt.org
nslookup openwrt.org 127.0.0.1
cat /tmp/resolv.conf*

# Connectivity
ping -c 3 192.168.1.1
ping -c 3 8.8.8.8
ping -c 3 -I wan 1.1.1.1
traceroute openwrt.org
traceroute6 openwrt.org
```

## Wireless diagnostics

```sh
wifi status
iwinfo
logread -e hostapd
logread -e wpa_supplicant
iw dev wlan0 link                    # STA mode
iw dev wlan0 station dump            # AP clients
```

## Firewall diagnostics

```sh
nft list ruleset | less
fw4 print
logread -e firewall

# Test if traffic hits forward chain — use tcpdump on wan + lan
```

## DHCP / DNS diagnostics

```sh
cat /tmp/dhcp.leases
logread -e dnsmasq
tcpdump -i br-lan port 67 or port 68 -n   # DHCP
tcpdump -i br-lan port 53 -n              # DNS
```

## Process and port check

```sh
ps w | grep -E 'netifd|dnsmasq|hostapd|dropbear|fw4'
netstat -tulpn 2>/dev/null
ss -tulpn
```

## ubus deep inspection

```sh
ubus list
ubus -v list network.device
ubus call network.device status '{"name":"br-lan"}'
ubus call system board
```

Parse JSON without jq:

```sh
ubus call network.interface.wan status | jsonfilter -e '@.up'
ubus call network.interface.wan status | jsonfilter -e '@.["ipv4-address"][0].address'
```

## tcpdump (minimal but essential)

```sh
opkg install tcpdump-mini

# ICMP on WAN
tcpdump -i eth1 -n icmp

# DHCP on LAN
tcpdump -i br-lan -n 'port 67 or port 68'

# Save pcap to /tmp (RAM)
tcpdump -i br-lan -w /tmp/lan.pcap -c 500
# Copy off with scp
```

## Safe recovery modes

| Mode | Access | Use |
|------|--------|-----|
| Normal SSH | LAN IP | Daily ops |
| Failsafe | Often 192.168.1.1, minimal fw | Broken firewall |
| Serial | UART | SSH/network dead |
| `firstboot` | Factory reset CLI | Total reset |

```sh
# Factory reset (destructive)
firstboot -y && reboot now

# Reboot
reboot
```

## Common failure patterns

| Symptom | Likely cause | First commands |
|---------|--------------|----------------|
| No LAN IP on clients | dnsmasq down / wrong pool | `logread -e dnsmasq`, `uci show dhcp.lan` |
| WiFi up, no internet | DNS or WAN or firewall | `ping 8.8.8.8`, `nslookup`, `ifstatus wan` |
| WAN DHCP fails | Wrong device / VLAN | `uci show network.wan`, `ip link` |
| SSH refused | dropbear / firewall / wrong IP | `netstat -tln`, `uci show dropbear` |
| IPv6 only broken | wan6 / PD / odhcpd | `ifstatus wan6`, `logread -e odhcpd` |
| Config lost on reboot | no `uci commit` | `uci changes` before reboot |
| Out of storage | overlay full | `df -h`, `opkg remove` |

## Scripted health check

Save as `/root/health.sh`:

```sh
#!/bin/sh
echo "=== OpenWrt $(. /etc/openwrt_release; echo $DISTRIB_RELEASE) ==="
for i in lan wan; do
    echo "--- $i ---"
    ifstatus $i 2>/dev/null | jsonfilter -e '@.up' -e '@.["ipv4-address"][0].address' 2>/dev/null
done
ping -c 1 -W 2 1.1.1.1 >/dev/null && echo "WAN v4: OK" || echo "WAN v4: FAIL"
ping -c 1 -W 2 openwrt.org >/dev/null && echo "DNS: OK" || echo "DNS: FAIL"
logread | tail -5
```

```sh
chmod +x /root/health.sh
/root/health.sh
```

## Performance quick check

```sh
opkg install iperf3
iperf3 -s &                   # server on router
# From PC: iperf3 -c 192.168.1.1

cat /proc/loadavg
top -bn1
```

## When to escalate to wiki / forum

- Board-specific switch/VLAN (`swconfig` vs DSA)
- Custom kernel modules
- ISP-specific PPPoE / VLAN tags (e.g. `option device 'eth1.835'`)

Always post: `cat /etc/openwrt_release`, `uci export network`, redacted `logread`.

## Capstone lab

Break it on purpose, then fix:

1. Set wrong WAN `device` — observe no internet, fix with serial or failsafe.
2. Disable `dnsmasq` — observe no DHCP, restore.
3. Block forward lan→wan in firewall — observe isolation, restore.

## Course completion checklist

You have mastered OpenWrt CLI when you can:

- [ ] Configure any setting with `uci` + commit + service reload without LuCI
- [ ] Explain zone-based firewall and add port forward from CLI
- [ ] Stand up AP + guest WLAN on separate subnets
- [ ] Harden SSH with keys and LAN binding
- [ ] Enable IPv6 PD and verify client connectivity
- [ ] Diagnose outage using `ifstatus`, `logread`, and `tcpdump`

Return to [Cheatsheet](./CHEATSHEET.md) for daily reference.
