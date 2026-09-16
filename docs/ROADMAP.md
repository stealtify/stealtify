# Stealtify — Roadmap

What's shipped and what's planned. This is a direction, not a set of dated
promises — priorities may change. Current release: **v1.0.0**.

> Release history: [CHANGELOG.md](../CHANGELOG.md).

---

## ✅ Shipped (v1.0.0)

- **Per-app** and **per-domain** routing (via groups), with a default proxy for everything else; groups can route direct.
- **8 protocols:** SOCKS5, HTTP CONNECT, SSH, VLESS, VMess, Trojan, Shadowsocks, AmneziaWG.
- **Full IPv6** in the packet stack (TCP/UDP, extension headers, IPv6 DNS).
- **Kill Switch**, **DNS leak protection** (plain and encrypted), **encrypted DNS (DoT/DoH)** with presets, **DNS-based ad/tracker filtering** (built-in list).
- **Failover & health checks**, **proxy chains**.
- **Subscriptions** (import + scheduled auto-refresh every ~12 hours), **QR import**, **share proxy via QR/clipboard**, config **backup/restore** (.stbackup).
- Real-time **traffic statistics**, **connection logs**, customizable dashboard.
- Auto-start on boot, auto-reconnect, Quick Settings tile (phone), in-app updates.
- **Android TV build** (top-bar UI, phone→TV config transfer over LAN).

---

## 🔜 Near-term

- **Real-time connection monitor** — live view of active connections (app → domain → proxy).
- **Explicit split-tunneling** — a clear "bypass VPN / direct" option per rule.
- **Speed test on the dashboard** and a live per-app bandwidth indicator.
- **Self-hosted crash reporting** (privacy-friendly, not Firebase).

---

## 🌐 More protocols

Expanding the protocol set, focused on modern DPI-resistant transports:

- **Hysteria2** — QUIC-based, strong for censorship circumvention.
- **TUIC** — QUIC-based, low-latency.
- **Standard WireGuard** — in addition to the existing AmneziaWG.

---

## 🗣 Multi-language (i18n)

Making Stealtify usable beyond a Russian-speaking audience:

- Move all UI strings into resources and ship a **full English** translation.
- **Automatic language** selection by the device's system locale (fallback to English).
- High-demand VPN locales next: **Farsi (fa)** and **Chinese (zh)**.
- Localize service notifications, the Quick Settings tile, errors and toasts.
- Infrastructure for **community translations**.

---

## 📶 Network profiles (Wi-Fi / SSID)

Automatically switch behaviour based on the network you're on:

- A **profile** = a named preset (default proxy + which groups are active + kill
  switch + DNS).
- Bind a profile to a **specific Wi-Fi (SSID)**, a **network type**
  (Wi-Fi / cellular), or a **trusted/untrusted** label.
- Example: *home Wi-Fi → direct*, *public Wi-Fi → everything through the proxy*,
  *mobile data → profile Y*.
- Priority: SSID binding > network type > default profile.

> Note: reading a specific Wi-Fi SSID on Android 10+ requires the location
> permission. Without it, profiles still work by **network type**. The location
> permission will be optional, with a clear explanation.

---

## 🎯 Advanced per-app routing

- **Per-app kill switch** — block a specific app's traffic (instead of leaking to
  direct) when its proxy fails.
- **Per-app / per-group DNS** — a different DNS resolver for chosen groups.

---

## Feedback

Ideas and requests are welcome — open an issue or contact **support@stealtify.app**.
