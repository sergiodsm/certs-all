# Module 05 — Firewall & NAT

## In one sentence

OpenWrt **fw4** (nftables) reads **`/etc/config/firewall`**, grouping interfaces into **zones** and applying forwarding, NAT, and rules.

## Commands

```sh
uci show firewall
/etc/init.d/firewall restart
/etc/init.d/firewall reload
fw4 print              # nft ruleset (if fw4 installed)
nft list ruleset       # kernel view
logread -e firewall
logread -e nft
```

Legacy **fw3** (iptables) exists on older releases — this course assumes **fw4** (23.05+).

## Zone model

```text
  [ lan zone ] ----forward----> [ wan zone ] ----> Internet
       ^                              |
       |         deny input           | masq NAT
       +-------- from wan ------------+
```

Default `/etc/config/firewall` skeleton:

```sh
config defaults
    option syn_flood '1'
    option input 'REJECT'
    option output 'ACCEPT'
    option forward 'REJECT'

config zone
    option name 'lan'
    list network 'lan'
    option input 'ACCEPT'
    option output 'ACCEPT'
    option forward 'ACCEPT'

config zone
    option name 'wan'
    list network 'wan'
    list network 'wan6'
    option input 'REJECT'
    option output 'ACCEPT'
    option forward 'REJECT'
    option masq '1'
    option mtu_fix '1'

config forwarding
    option src 'lan'
    option dest 'wan'
```

## Attach interface to zone

Guest network on `guest` interface:

```sh
uci add firewall zone
uci set firewall.@zone[-1].name='guest'
uci set firewall.@zone[-1].input='REJECT'
uci set firewall.@zone[-1].output='ACCEPT'
uci set firewall.@zone[-1].forward='REJECT'
uci add_list firewall.@zone[-1].network='guest'

uci add firewall forwarding
uci set firewall.@forwarding[-1].src='guest'
uci set firewall.@forwarding[-1].dest='wan'

uci commit firewall
/etc/init.d/firewall restart
```

## Port forward (DNAT)

Allow WAN TCP 8080 → LAN 192.168.1.100:80:

```sh
uci add firewall redirect
uci set firewall.@redirect[-1].name='WebServer'
uci set firewall.@redirect[-1].src='wan'
uci set firewall.@redirect[-1].src_dport='8080'
uci set firewall.@redirect[-1].dest='lan'
uci set firewall.@redirect[-1].dest_ip='192.168.1.100'
uci set firewall.@redirect[-1].dest_port='80'
uci set firewall.@redirect[-1].proto='tcp'
uci set firewall.@redirect[-1].target='DNAT'
uci commit firewall
/etc/init.d/firewall restart
```

## Open port on router itself

Traffic **to the router** (SSH, DNS on router):

```sh
uci add firewall rule
uci set firewall.@rule[-1].name='Allow-SSH-WAN'
uci set firewall.@rule[-1].src='wan'
uci set firewall.@rule[-1].dest_port='22'
uci set firewall.@rule[-1].proto='tcp'
uci set firewall.@rule[-1].target='ACCEPT'
uci commit firewall
/etc/init.d/firewall restart
```

**Security:** Prefer VPN over exposing SSH on WAN.

## Block / allow by IP

```sh
uci add firewall rule
uci set firewall.@rule[-1].name='Block-Bad-Host'
uci set firewall.@rule[-1].src='lan'
uci set firewall.@rule[-1].src_ip='192.168.1.99'
uci set firewall.@rule[-1].target='DROP'
uci commit firewall
/etc/init.d/firewall reload
```

## Disable masquerade (NAT)

Rare — double NAT testing:

```sh
uci set firewall.@zone[1].masq='0'   # verify index — wan zone
uci commit firewall
/etc/init.d/firewall restart
```

Find wan zone safely:

```sh
WAN_ZONE=$(uci show firewall | awk -F'[.=]' '/name=.wan./{print $2; exit}')
uci set firewall.$WAN_ZONE.masq='0'
```

## IPv6 forwarding

Separate zone options:

```sh
option masq6 '0'           # NPT or masquerade IPv6 (uncommon)
option forward 'ACCEPT'    # between zones
```

IPv6 usually relies on **delegated prefixes** and per-interface `delegate` — see Module 08.

## Custom nft include (advanced)

`/etc/firewall.user` — shell script executed on firewall start (legacy hook). Prefer UCI rules when possible.

```sh
# /etc/firewall.user example — use sparingly
# iptables -t nat -A POSTROUTING -o tun0 -j MASQUERADE
```

fw4: use `/etc/nftables.d/` includes on some builds.

## Inspection

```sh
# Verify NAT
nft list chain inet fw4 srcnat

# Counters on rules
nft list ruleset | grep -A2 counter

# Test from LAN client
curl -4 ifconfig.me
```

## Common mistakes

1. **Forward rule without zone assignment** — interface not in any zone = no policy.
2. **Redirect `dest` zone wrong** — must match where target IP lives.
3. **Testing from inside LAN with WAN IP** — hairpin NAT may need `reflection` option on redirect.
4. **Editing iptables directly** — wiped on `firewall restart`; use UCI.

## Hairpin NAT (NAT loopback)

```sh
uci set firewall.@redirect[-1].reflection='1'
uci commit firewall
/etc/init.d/firewall restart
```

## Lab exercise

Create guest zone: internet access allowed, no access to `lan` (no forwarding lan↔guest; only guest→wan).

## Bridge to Module 06

Clients need IPs and names — **dnsmasq** via `/etc/config/dhcp`.
