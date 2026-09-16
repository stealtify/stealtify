# Changelog

All notable changes to Stealtify are documented here.
See [Releases](../../releases) for downloads and checksums.

## 1.0.0 (2026-09-16)

First public release.

### Routing

- Per-app routing — assign a different proxy to each application.
- Domain rules — matched by DNS responses and TLS SNI.
- App groups, with a default proxy for everything else; a group can route direct.
- Source app identified via `getConnectionOwnerUid()` (Android 10+), not port heuristics.
- Full IPv6 in the packet stack (TCP/UDP, extension headers, IPv6 DNS).

### Protocols

- SOCKS5 and HTTP CONNECT (Kotlin engine).
- VLESS (Reality, XTLS-Vision), VMess, Trojan (Reality) via xray-core.
- Shadowsocks (SIP004 AEAD), SSH dynamic forwarding, AmneziaWG via the Go engine.

### Privacy and safety

- Kill switch — in-app protection while the tunnel recovers.
- DNS leak protection, plain and encrypted.
- Encrypted DNS (DoT/DoH) with Cloudflare, Google, AdGuard and Quad9 presets.
- DNS-based ad and tracker filtering with a built-in list (off by default).
- Secrets stored in the Android Keystore, never in plaintext.
- Every build is signed and verified at launch; tampered builds are rejected.
- No analytics SDK, no account, no telemetry.

### Configuration

- Import via URI links (`vless://`, `vmess://`, `trojan://`, `ss://`, `socks5://`,
  `http://`, `ssh://`, `awg://`, `vpn://`) and QR codes.
- Subscriptions with scheduled auto-refresh (~12 hours).
- Share a proxy via QR code or clipboard.
- Backup and restore of the full configuration (`.stbackup`).

### Reliability

- Failover with health checks and automatic proxy switching.
- Proxy chains.
- Auto-start on boot, auto-reconnect.

### Interface

- Jetpack Compose with Material 3 (Material You).
- Real-time traffic statistics, connection logs, customizable dashboard.
- Quick Settings tile (phone).
- In-app updates.

### Android TV

- Separate build (`com.stealtify.app.tv`), status **beta**.
- Top-bar UI adapted for D-pad navigation.
- Configuration transfer from a phone over the local network.
- Four APKs: arm64-v8a, armeabi-v7a, x86 and a universal fallback.

### Licensing

- Proprietary license (EULA); see [LICENSE](LICENSE).
- No GPL-3.0 components — Shadowsocks is implemented in-house (SIP004 AEAD).
- Modified xray-core files (MPL-2.0) available on request; see [NOTICE](NOTICE).
