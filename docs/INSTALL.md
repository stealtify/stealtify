# Stealtify 1.0.0

**Stealtify** routes the traffic of selected apps and websites through your own proxy servers.
No root required. Supports SOCKS5, HTTP, Shadowsocks, SSH, VLESS, VMess, Trojan and AmneziaWG.

> 📘 Full manual covering every feature — see **[USER_GUIDE.md](USER_GUIDE.md)** next to this file.
> 🇷🇺 Russian version: **[INSTALL.ru.md](INSTALL.ru.md)**.

---

## About this release

This is the **first public release** of Stealtify.

Everything runs on the device through the standard Android VpnService API — no
root, no account and no telemetry. You supply your own proxy servers; the app
decides which apps and sites go through them and which go out directly.
Besides your own proxy servers, the app contacts only the update server, the
IP-geolocation service ipapi.co (for the country shown on the Home screen —
this request goes directly, not through the proxy), IP-echo services through
the proxy during server tests, and the subscription and DNS servers you
configure. Details: USER_GUIDE.md, section 10.

Highlights: per-app and per-domain routing, 8 protocols, import by link / QR code
/ subscription, Kill Switch and DNS leak protection, IPv4 + IPv6, traffic
statistics and failover to backup servers. The full feature list is below and in
[USER_GUIDE.md](USER_GUIDE.md).

---

## Requirements

- Android **10** or newer.
- **arm64** processor (most modern phones).
- At least one proxy server (your proxy/VPN provider supplies the details — a link, a QR code or a subscription).
- Interface language: Russian.

---

## Installation

> ⚠️ **If you previously installed a test build:** Android does not let you install a release build over a debug build due to different signing keys. You must uninstall the old version first. **Before uninstalling, back up your configuration** in the app (**Settings → Data → Export**), then restore it after installation — otherwise your proxies and rules will be lost.

1. Download **`Stealtify_1.0.0_release.apk`**.
2. Open it. If Android asks, allow **installing from unknown sources** for your browser or file manager.
3. Tap **Install** and open the app.

Future updates are detected automatically: an update prompt appears on the Home screen and under
**Settings → Updates**.

### Verifying file integrity (optional)

A SHA-256 checksum is published for every build. To make sure the file is intact:

```powershell
Get-FileHash .\Stealtify_1.0.0_release.apk -Algorithm SHA256
```

The result must match the checksum listed for this version.

### Protection against counterfeit builds

A checksum only tells you the file downloaded intact. It says nothing about **who built it** —
anyone can repackage an APK, point it at their own servers, publish it under the Stealtify name
and provide a matching checksum of their own. For a VPN app this is the attack that actually
matters: a counterfeit build sees all your traffic.

Stealtify defends against this on its own. Every genuine release is signed with the developer's
key, and the app verifies that signature each time it starts. A repackaged build cannot carry
that signature — resigning it produces a different one, and the developer's private key is not
in the APK.

If the check fails, the app shows a warning screen instead of its interface; settings and the
connect button are unreachable. The warning cannot be dismissed from inside the app: the VPN
and your settings stay out of reach, so a counterfeit build cannot route your traffic anywhere.

You do not need to do anything for this — it works automatically. Just download the app from
the official source:

- **https://stealtify.app** (website)
- **https://update.stealtify.app**

The safest habit is to let the app update itself: built-in updates are downloaded over a pinned
TLS connection and their checksum is verified before installation.

---

## Quick start

1. **Add a proxy.** **Proxies** tab → **＋** button. Paste a proxy link or a subscription link. Or tap the **camera** icon and scan a QR code.
2. **Connect.** **Home** tab → large round **Connect** button. On first launch, confirm the VPN permission.
3. Done — the status changes to **VPN active** and traffic statistics start flowing.

By default all traffic goes through the proxy. To route only specific apps or sites through the proxy,
configure **Rules** and **Groups** (described in detail in [USER_GUIDE.md](USER_GUIDE.md)).

---

## What the app can do (in brief)

- 🎯 **Per-app routing** — assign different proxies to different apps (via groups).
- 🌐 **Per-domain routing** — rules for websites, including wildcards like `*.example.com`.
- 🔗 **8 protocols** — SOCKS5, HTTP, Shadowsocks, SSH, VLESS (Reality, XTLS-Vision), VMess, Trojan, AmneziaWG.
- 🌍 **IPv4 and IPv6** — including IPv6-only networks.
- 📥 **Import** — manually, by QR code, or by subscription link (with automatic server-list refresh every ~12 hours). Share a proxy via QR or copy the link.
- 📊 **Monitoring** — speed, external IP, per-app traffic, server reachability checks, connection log.
- 🛡 **Security** — Kill Switch, DNS leak protection, encrypted DNS (DoT/DoH), DNS-based ad blocking, encrypted credential storage.
- ⚙ **Convenience** — dark theme, auto-start on boot, auto-reconnect, backup proxies (failover), Quick Settings tile, configuration backup (.stbackup; the file contains your keys — keep it private).

---

## Known limitations

| Limitation | Details |
|---|---|
| **Signature mismatch** | Android does not allow installing an APK signed with a different key over an existing app. If you previously installed a test (debug) build, you must uninstall it first. Before uninstalling, back up your configuration in the app (**Settings → Data → Export**), then restore it after installing the official release — otherwise your proxies and rules will be lost. |
| **Not in Google Play** | The app is distributed only from https://update.stealtify.app. Android will ask to allow "Unknown sources" because the app is not from the Play Store. |
| **Builds older than 1.41.0 cannot auto-update** | Due to a change in Let's Encrypt certificate pinning, older builds cannot verify the update server's certificate and cannot download updates over the network. Download and install the latest APK manually from the official website. Your configuration and data are preserved — the signature key is the same. |
| **Russian interface only** | The app has no English (or other) UI translation and no language switch. |
| **Backup import replaces the configuration immediately** | Importing a `.stbackup` (or legacy JSON) file replaces all proxies, groups and rules at once, without a confirmation prompt — export your current configuration first if you want to keep it. |

---

## Support

Problems or questions — contact us:
**Settings → Contact us** (or email **support@stealtify.app**).
Website: https://stealtify.app
