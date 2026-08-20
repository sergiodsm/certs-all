# Module 04 — Wireless (WiFi)

## In one sentence

OpenWrt wireless is configured via **`/etc/config/wireless`** (`wifi-device` + `wifi-iface` sections) and driven by **hostapd** (AP) or **wpa_supplicant** (client).

## Essential commands

| Command | Purpose |
|---------|---------|
| `wifi status` | Radio + iface state (JSON) |
| `wifi reload` | Apply UCI wireless changes |
| `wifi up` / `wifi down` | Bring radios up/down |
| `wifi reconnect` | STA reconnect to upstream AP |
| `iw dev` | Linux wireless devices |
| `iwinfo` | Human-readable (package `iwinfo`) |
| `ubus call hostapd.wlan0 get_clients` | Associated clients (if available) |

```sh
opkg update && opkg install iwinfo   # if missing
iwinfo
iwinfo wlan0 assoclist
```

## UCI structure

```sh
# Physical radio
config wifi-device 'radio0'
    option type 'mac80211'
    option path 'platform/10300000.wmac'   # or pci0000:00/...
    option channel '36'
    option band '5g'                        # 2g | 5g | 6g
    option htmode 'VHT80'                  # HT20, HE40, etc.
    option country 'US'
    option disabled '0'

# Logical SSID / interface
config wifi-iface 'default_radio0'
    option device 'radio0'
    option network 'lan'
    option mode 'ap'                       # ap | sta | mesh | adhoc
    option ssid 'MyNetwork'
    option encryption 'psk2'
    option key 'StrongPassphrase123'
    option hidden '0'
```

## Radio options reference

```sh
option channel 'auto'    # or 1-13 (2.4), 36-165 (5)
option band '2g'
option htmode 'HT20'     # width: HT20/40, VHT80, HE160
option txpower '20'      # dBm
option disabled '1'      # disable entire radio
option country 'DE'      # regulatory domain — legal requirement
```

List channels:

```sh
iw list | grep -A 50 "Band 1"
iw phy phy0 info
```

## wifi-iface modes

| mode | Daemon | Typical network |
|------|--------|-----------------|
| `ap` | hostapd | `lan`, guest bridge |
| `sta` | wpa_supplicant | `wwan` interface |
| `mesh` | wpad mesh | custom |
| `adhoc` | ibss | rare |

## Encryption syntax

| encryption value | Meaning |
|------------------|---------|
| `none` | Open |
| `psk` | WPA-PSK (TKIP — legacy) |
| `psk2` | WPA2-PSK (AES) |
| `psk-mixed` | WPA + WPA2 |
| `sae` | WPA3-Personal |
| `sae-mixed` | WPA2 + WPA3 |
| `wpa2` | WPA2-Enterprise (needs `option eap_type`, certs) |

```sh
# WPA2-Personal
uci set wireless.default_radio0.encryption='psk2'
uci set wireless.default_radio0.key='YourWiFiPassword'

# WPA3
uci set wireless.default_radio0.encryption='sae'
uci set wireless.default_radio0.key='YourWiFiPassword'

uci commit wireless
wifi reload
```

## Enterprise (802.1X) sketch

```sh
uci set wireless.default_radio0.encryption='wpa2'
uci set wireless.default_radio0.eap_type='tls'
uci set wireless.default_radio0.server='radius.example.com'
# Certificates via EAP config — see OpenWrt wiki for full example
```

## Access Point on LAN bridge

Default pattern — `network 'lan'` attaches to `br-lan`:

```sh
uci set wireless.default_radio0.network='lan'
uci set wireless.default_radio0.mode='ap'
uci commit wireless
wifi reload
```

## Guest WiFi (separate network)

```sh
# Assume network.guest + firewall zone exist (Modules 03 & 05)
uci add wireless wifi-iface
uci set wireless.@wifi-iface[-1].device='radio0'
uci set wireless.@wifi-iface[-1].mode='ap'
uci set wireless.@wifi-iface[-1].network='guest'
uci set wireless.@wifi-iface[-1].ssid='GuestWiFi'
uci set wireless.@wifi-iface[-1].encryption='psk2'
uci set wireless.@wifi-iface[-1].key='GuestPassword'
uci set wireless.@wifi-iface[-1].isolate='1'    # AP client isolation
uci commit wireless
wifi reload
```

## STA mode (WiFi as WAN)

```sh
uci set network.wwan=interface
uci set network.wwan.proto='dhcp'
uci set network.wwan.device='wlan0'    # often set by wireless up

uci add wireless wifi-iface
uci set wireless.@wifi-iface[-1].device='radio0'
uci set wireless.@wifi-iface[-1].mode='sta'
uci set wireless.@wifi-iface[-1].network='wwan'
uci set wireless.@wifi-iface[-1].ssid='UpstreamSSID'
uci set wireless.@wifi-iface[-1].encryption='psk2'
uci set wireless.@wifi-iface[-1].key='UpstreamPassword'

uci commit
/etc/init.d/network restart
wifi reload
ifstatus wwan
```

## Multi-SSID (same radio)

Multiple `wifi-iface` sections on one `wifi-device`:

```sh
uci add wireless wifi-iface
uci set wireless.@wifi-iface[-1].device='radio0'
uci set wireless.@wifi-iface[-1].mode='ap'
uci set wireless.@wifi-iface[-1].network='iot'
uci set wireless.@wifi-iface[-1].ssid='IoT'
uci set wireless.@wifi-iface[-1].encryption='psk2'
uci set wireless.@wifi-iface[-1].key='iot-secret'
uci commit wireless
wifi reload
```

## MAC filter

```sh
uci set wireless.default_radio0.macfilter='allow'
uci add_list wireless.default_radio0.maclist='AA:BB:CC:DD:EE:01'
uci commit wireless
wifi reload
```

Values: `disable`, `allow`, `deny`.

## Runtime debugging

```sh
wifi status
logread -e hostapd
logread -e wpa_supplicant

# Scan (STA)
iw dev wlan0 scan | grep -E 'SSID|signal'

# Connected clients
iwinfo wlan0 assoclist
```

## Common mistakes

1. **Forgot `wifi reload`** — UCI committed but hostapd still old config.
2. **Wrong `path` after driver change** — radio won't start; check `dmesg | grep -i wifi`.
3. **Channel/width illegal for country** — hostapd fails silently; read `logread`.
4. **STA + AP on same radio** — possible but performance hit; prefer dual-radio hardware.
5. **`network` mismatch** — SSID up but no IP if not bridged to an interface with proto.

## Lab exercises

1. Change 2.4 GHz channel and SSID; verify with `iwinfo`.
2. Add open guest SSID on separate subnet with isolation.
3. Configure STA mode to phone hotspot; verify default route via `wwan`.

## Bridge to Module 05

Wireless clients land on **zones** filtered by **firewall**. Next: NAT and forwarding rules.
