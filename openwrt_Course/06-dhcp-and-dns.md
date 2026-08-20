# Module 06 — DHCP & DNS

## In one sentence

**dnsmasq** (default) serves DHCP and DNS from **`/etc/config/dhcp`**, tied to **`network` interfaces**.

## Commands

```sh
uci show dhcp
/etc/init.d/dnsmasq restart
/etc/init.d/dnsmasq reload
logread -e dnsmasq
cat /tmp/dhcp.leases
```

Lease file format: `timestamp mac ip hostname client-id`

## DHCP server on LAN

```sh
config dhcp 'lan'
    option interface 'lan'
    option start '100'
    option limit '150'
    option leasetime '12h'
    option dhcpv4 'server'
    option dhcpv6 'server'
    option ra 'server'
    option ra_slaac '1'
```

CLI edit pool `192.168.1.100–249`:

```sh
uci set dhcp.lan.start='100'
uci set dhcp.lan.limit='150'
uci set dhcp.lan.leasetime='12h'
uci commit dhcp
/etc/init.d/dnsmasq restart
```

Pool math: start + limit − 1 = last octet (on /24 aligned with router IP).

## Disable DHCP on interface

```sh
uci set dhcp.lan.ignore='1'
uci commit dhcp
/etc/init.d/dnsmasq restart
```

Or delete section:

```sh
uci delete dhcp.lan
uci commit dhcp
/etc/init.d/dnsmasq restart
```

## Static DHCP lease (reservation)

```sh
uci add dhcp host
uci set dhcp.@host[-1].name='printer'
uci set dhcp.@host[-1].mac='AA:BB:CC:DD:EE:FF'
uci set dhcp.@host[-1].ip='192.168.1.50'
uci commit dhcp
/etc/init.d/dnsmasq restart
```

Optional DNS name for LAN:

```sh
uci set dhcp.@host[-1].dns='1'
```

## DNS on router (dnsmasq)

```sh
config dnsmasq
    option domainneeded '1'
    option local '/lan/'
    option domain 'lan'
    option expandhosts '1'
    option authoritative '1'
    option readethers '1'
    option leasefile '/tmp/dhcp.leases'
    option localservice '1'
    list server '8.8.8.8'
    list server '1.1.1.1'
```

Upstream DNS from WAN DHCP — often automatic; manual:

```sh
uci delete dhcp.@dnsmasq[0].server
uci add_list dhcp.@dnsmasq[0].server='9.9.9.9'
uci commit dhcp
/etc/init.d/dnsmasq restart
```

## Local DNS records

```sh
uci add dhcp domain
uci set dhcp.@domain[-1].name='home.lan'
uci set dhcp.@domain[-1].ip='192.168.1.10'
uci commit dhcp
/etc/init.d/dnsmasq restart
```

Or `/etc/hosts` (persistent if in overlay):

```sh
echo '192.168.1.10 nas.home.lan' >> /etc/hosts
/etc/init.d/dnsmasq restart
```

## DHCP options (advanced)

```sh
uci add_list dhcp.lan.dhcp_option='6,192.168.1.1'      # DNS
uci add_list dhcp.lan.dhcp_option='3,192.168.1.1'      # gateway
uci add_list dhcp.lan.dhcp_option='15,lan'             # domain name
uci commit dhcp
/etc/init.d/dnsmasq restart
```

Option 6 = DNS server, 3 = router, 15 = domain.

## DNS forwarding / split DNS

```sh
# Query corporate DNS for specific domain
uci add_list dhcp.@dnsmasq[0].server='/corp.example.com/10.0.0.53'
uci commit dhcp
/etc/init.d/dnsmasq restart
```

## Disable dnsmasq DNS (DHCP only)

Use `port=0` in dnsmasq or run separate DHCP — niche; typical homelab keeps both.

## WAN: DHCP client options

On **`network.wan`**, not dhcp package:

```sh
uci set network.wan.hostname='my-router'
uci commit network
/etc/init.d/network restart
```

## Testing

```sh
# From router
nslookup openwrt.org 127.0.0.1
drill @127.0.0.1 openwrt.org

# Active leases
cat /tmp/dhcp.leases
ubus call dhcp ipv4leases    # if available
```

## odhcpd (IPv6 DHCP/RA)

Often paired with dnsmasq — IPv6 DHCPv6 and RA. Config still in `dhcp` sections (`ra`, `dhcpv6` options). See Module 08.

## Common mistakes

1. **DHCP pool overlaps router IP or static hosts** — causes conflicts.
2. **Changed LAN subnet, not dhcp** — pool still old range.
3. **Two DHCP servers on LAN** — disable on upstream AP.
4. **Forgot reload** — `dnsmasq reload` usually enough for dhcp edits.

## Lab exercise

Reserve three static leases and add local DNS name `server.lan` → your server IP.

## Bridge to Module 07

Remote administration requires **SSH (dropbear)** and user hygiene.
