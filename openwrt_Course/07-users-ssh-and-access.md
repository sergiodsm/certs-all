# Module 07 — Users, SSH & Access

## In one sentence

OpenWrt defaults to a single **root** account over **Dropbear SSH**; there is no sudo — root access is full system control.

## User model

| Aspect | OpenWrt default |
|--------|-----------------|
| Admin user | `root` only (typical) |
| sudo | Not installed by default |
| Shell | `/bin/ash` in `/etc/passwd` |
| Password | `passwd` command |
| Extra users | Possible but uncommon for routers |

```sh
cat /etc/passwd
cat /etc/shadow          # hashed passwords — root only
passwd                   # change root password — do first boot
passwd root
```

## Create a non-root user (optional)

```sh
# Add user with home and ash shell
echo "operator:x:1000:1000:Operator:/home/operator:/bin/ash" >> /etc/passwd
echo "operator::19000:0:99999:7:::" >> /etc/shadow
passwd operator

mkdir -p /home/operator
chown operator:operator /home/operator
```

Non-root users **cannot** run `/etc/init.d/*` or `uci` by default unless you add group permissions — most operators use **root over SSH with keys** instead.

## Dropbear SSH — UCI syntax

Config: `/etc/config/dropbear`

```sh
config dropbear
    option PasswordAuth 'on'
    option RootPasswordAuth 'on'
    option Port '22'
    option Interface 'lan'
    # option GatewayPorts '1'
```

### Harden SSH (recommended baseline)

```sh
# Disable password auth — keys only
uci set dropbear.@dropbear[0].PasswordAuth='off'
uci set dropbear.@dropbear[0].RootPasswordAuth='off'
uci commit dropbear
/etc/init.d/dropbear restart
```

**Warning:** Ensure SSH keys work before disabling passwords.

### Bind SSH to LAN only

```sh
uci set dropbear.@dropbear[0].Interface='lan'
uci commit dropbear
/etc/init.d/dropbear restart
```

### Change port

```sh
uci set dropbear.@dropbear[0].Port='2222'
uci commit dropbear
/etc/init.d/dropbear restart
```

Multiple instances — add section:

```sh
uci add dropbear dropbear
uci set dropbear.@dropbear[-1].Port='2222'
uci set dropbear.@dropbear[-1].Interface='lan'
uci commit dropbear
/etc/init.d/dropbear restart
```

## SSH public key authentication

OpenWrt uses **`/etc/dropbear/authorized_keys`** (Dropbear format, not always OpenSSH).

### From your PC — install key

```sh
# On OpenWrt (paste your public key)
mkdir -p /etc/dropbear
echo 'ssh-ed25519 AAAA...your-key... user@host' >> /etc/dropbear/authorized_keys
chmod 600 /etc/dropbear/authorized_keys
/etc/init.d/dropbear restart
```

Or from PC with `ssh-copy-id` (OpenSSH client):

```sh
ssh-copy-id -i ~/.ssh/id_ed25519.pub root@192.168.1.1
```

If `ssh-copy-id` fails, manual paste to `/etc/dropbear/authorized_keys`.

### Key-only for root

```sh
# After key verified:
uci set dropbear.@dropbear[0].PasswordAuth='off'
uci set dropbear.@dropbear[0].RootPasswordAuth='off'
uci commit dropbear
/etc/init.d/dropbear restart
```

## OpenSSH vs Dropbear

Default: **dropbear** (small). Optional **openssh-server** via opkg for OpenSSH-specific features:

```sh
opkg update
opkg install openssh-server
/etc/init.d/sshd enable
/etc/init.d/sshd start
# Keys: /etc/ssh/authorized_keys
```

Do not run both on same port.

## Serial console

Always available if UART pinned — bypasses SSH lockout:

```sh
# /etc/inittab enables login on serial
# Recovery: fail-safe mode — press button during boot (device-specific)
```

## LuCI access (related)

```sh
uci show uhttpd
uci set uhttpd.main.listen_http='192.168.1.1:80'
uci set uhttpd.main.listen_https='192.168.1.1:443'
uci commit uhttpd
/etc/init.d/uhttpd restart
```

Restrict to LAN interface binding for security.

## Firewall interaction

WAN SSH requires explicit rule (Module 05):

```sh
uci add firewall rule
uci set firewall.@rule[-1].name='Allow-SSH-from-WAN'
uci set firewall.@rule[-1].src='wan'
uci set firewall.@rule[-1].dest_port='22'
uci set firewall.@rule[-1].proto='tcp'
uci set firewall.@rule[-1].target='ACCEPT'
uci commit firewall
/etc/init.d/firewall restart
```

Better: VPN (WireGuard) to LAN, SSH only on LAN.

## Session inspection

```sh
who
w
logread -e dropbear
```

## Lockout recovery checklist

1. Serial console → fix `dropbear` / firewall
2. Fail-safe boot (failsafe IP often `192.168.1.1`, no firewall)
3. `mount_root` and edit overlay if extroot

Failsafe trigger (many devices):

```text
Power cycle → wait for LED blink → press reset button repeatedly
```

Then:

```sh
# In failsafe, only RAM mounted — press enter for shell
mount_root
nvram show    # older; or directly:
vi /etc/config/dropbear
uci set dropbear.@dropbear[0].PasswordAuth='on'
uci commit dropbear
reboot
```

## Common mistakes

1. **Disable password before testing keys** — locked out except serial.
2. **Wrong authorized_keys path** — Dropbear uses `/etc/dropbear/`, not `/root/.ssh/`.
3. **Editing keys without restart** — dropbear reads on start; restart after change.
4. **Exposing SSH on WAN with weak password** — bots scan within minutes.

## Lab exercise

1. Set root password.
2. Install Ed25519 key; verify login without password.
3. Disable password auth; confirm LAN SSH still works.

## Bridge to Module 08

Dual-stack networking: **IPv6** delegation, RA, and firewall6 considerations.
