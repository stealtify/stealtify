# Privacy Policy — Stealtify

_Last updated: 2026-07-01. Applies to the Stealtify Android app (`com.stealtify.app`)._

Stealtify is an open-source, on-device proxy/VPN client. It is designed to keep
your data on your device and under your control.

## Short version

- **No analytics, no tracking, no ads, no third-party telemetry SDKs.**
- We (the Stealtify project) **do not operate** the proxy servers you connect to
  and **do not receive** your browsing traffic.
- Everything you configure (proxies, rules, credentials) stays **on your device**.

## What stays on your device

- Proxy server configurations, groups, app/domain rules and app settings — stored
  locally in an on-device database.
- Secrets (passwords, UUIDs, private keys) — stored in the **Android Keystore**
  (`SecretStore`), not in plaintext.
- Connection logs (if you enable logging) — kept **in memory only** and cleared
  when the app restarts.
- Traffic statistics — computed and shown locally; not uploaded anywhere.

## What leaves your device

- **Your proxied traffic** goes to the **proxy servers you configure**. Those
  servers are operated by you or your provider — their handling of your traffic
  is governed by *their* privacy policy, not this one.
- **Subscription updates:** if you add a subscription URL, the app fetches the
  server list from that URL. The request may include a device identifier
  (`X-Hwid`) and a `User-Agent`; both are **configurable/anonymizable** in the
  app's secret menu. The subscription server is chosen by you.
- **App update checks:** the app periodically contacts the update endpoint
  (`update.stealtify.app`) to check for a newer version. This is a standard HTTPS
  request that reveals your IP address and the app's User-Agent to that server,
  as any web request would. No account or personal data is sent.
- **Configuration transfer (TV/Android):** The app supports transferring full
  configuration (proxies, rules, groups, **including passwords and private keys**)
  from a smartphone to a TV device or another Android device via:
  - **QR code:** configuration is encoded as Base64-compressed JSON and displayed as a QR code.
  - **Local network (LAN):** configuration is transmitted as a raw socket connection between devices.
  
  **Encryption:** the transferred data is encrypted end-to-end using AES-256-GCM
  with a passphrase derived from user input. **The transfer bypasses
  `network_security_config` pinning** (raw socket; not HTTP). The receiving device
  requires explicit user confirmation before importing. Treat QR codes and LAN
  transfers as sensitive — they contain all your proxy credentials.

## What we do NOT collect

- No names, emails (unless you email support yourself), phone numbers or accounts.
- No browsing history, DNS query contents, or traffic payloads.
- No advertising identifiers or cross-app tracking.

## Data you export

The **backup** feature writes your configuration (including secrets) to a JSON
file **you choose**. Treat that file as sensitive and store it securely — it is
never uploaded by the app.

## Permissions

See the app permissions section in the [User Guide](./USER_GUIDE.md#11-app-permissions).
Each permission (VPN, camera for QR, notifications, file access, network state)
is used only for the stated feature.

## Children

Stealtify is a general networking tool and is not directed at children.

## Changes

Because Stealtify is open source, changes to data handling are visible in the
source history. Material changes to this policy will be noted in the release
notes.

## Contact

Questions about privacy: **support@stealtify.app** or open an issue in the
repository.

---

> This document describes the behaviour of the open-source app as published. It
> is provided for transparency and is not legal advice; if you distribute a
> modified build, review and adjust this policy accordingly.
