# Stealtify — User Guide

Complete manual covering every feature of the app.

Stealtify is an Android app (a userspace VPN) that routes the traffic of individual apps and domains through proxy servers. It supports the **SOCKS5, HTTP, Shadowsocks, SSH, VLESS, VMess, Trojan and AmneziaWG** protocols. Runs on Android 10+ (arm64).

> 🇷🇺 Russian version: **[USER_GUIDE.ru.md](USER_GUIDE.ru.md)**.

---

## Contents

1. [Quick start](#1-quick-start)
2. [Home screen (Dashboard)](#2-home-screen-dashboard)
3. [Proxy servers](#3-proxy-servers)
4. [Rules and groups](#4-rules-and-groups)
5. [App rules](#5-app-rules)
6. [Settings](#6-settings)
7. [Connection logs](#7-connection-logs)
8. [How routing works](#8-how-routing-works)
9. [Common tasks](#9-common-tasks)
10. [App permissions](#10-app-permissions)

---

## 1. Quick start

1. Open the app — you land on the **Home** screen.
2. Go to the **Proxies** tab (bottom) and add at least one server (the **+** button, a QR code, or a subscription link).
3. Return to **Home** and tap the large round **Connect** button.
4. On the first connection Android asks for VPN permission — confirm it.
5. The status changes to **Protected** ("Защищено") and traffic statistics begin.

By default (no rules configured) all traffic goes through the **default proxy**. Use **Rules** and **Groups** to send only chosen apps/sites through a proxy, or to send some of them directly instead (see sections 4–5).

The bottom navigation bar has 4 tabs: **Home**, **Proxies**, **Rules**, **Settings**. The **Apps** screen also opens from the "Rules" section, or by tapping the "Rules" figure in the Home quick-stats tile.

---

## 2. Home screen (Dashboard)

The central screen for managing the connection and monitoring.

### Connect button
- A large round button in the center: **Connect** ("Подключить") / **Disconnect** ("Отключить").
- Above it — a status indicator: **Protected** ("Защищено"), **Not connected** ("Не подключено"), or **Reconnecting…** ("Переподключение...").
- If no proxy has been added, tapping it shows a red hint card and a snackbar "Сначала добавьте прокси-сервер во вкладке Прокси" ("Add a proxy server in the Proxies tab first"). If the health check finds every server down, a snackbar "Все прокси недоступны. Проверьте подключение." ("All proxies are unreachable. Check your connection.") appears instead.

### Customizable tiles
The edit icon **"Настроить плитки"** ("Customize tiles") in the top-right corner enables tile edit mode: tiles can be **dragged** (long-press + drag), **hidden/shown** (eye icon), reordered with up/down arrows, or reset via **"Сбросить по умолчанию"** ("Reset to default"). Six tiles are available:

| Tile | What it shows |
|------|---------------|
| **Speed** | Two meters, "Прокси" (Proxy) and "Напрямую" (Direct), each with download ↓ and upload ↑ speed, updated every second, shown only while connected |
| **External IP** | Flag/country and server name, with a refresh button; shown only while connected. The country is looked up via ipapi.co |
| **Quick stats** | "Серверов" (active servers), "Пинг, мс" (best ping, ms), "Правил" (active rules) — only "Правил" is tappable and navigates to the Apps screen |
| **Proxies (check)** ("Прокси (проверка)") | List of servers with reachability status (green/red), ping and type. Tapping a row makes that server the **default server** and restarts the tunnel if connected (~1 s pause); a re-check button is available |
| **Traffic** | Total session traffic, "N% via proxy / N% direct" bar, session duration, active connection count, blocked-DNS counter |
| **Apps by traffic** | Top 5 apps by traffic volume (proxy/direct/total), plus "and N more apps" |

### Update notification
If a new version is available, a dialog with the version number and changelog appears on open: **Update** or **Later**. Mandatory updates cannot be postponed. The same dialog also shows download progress once an update starts, an **Install** button, and retry/cancel controls; the download continues in the background via a foreground-service notification even if you leave the app.

---

## 3. Proxy servers

The **Proxies** tab manages servers. An empty list shows the hint "Tap + to add".

### Supported protocols
`SOCKS5` · `HTTP` · `Shadowsocks` · `SSH` · `VLESS` · `VMess` · `Trojan` · `AmneziaWG`

### Ways to add a server

**A. The + button (quick add)**
Opens a full-screen **"Добавить"** ("Add") dialog with a single field, **"Прокси или подписка"** ("Proxy or subscription"), where you can paste:
- a proxy link in any format (see below) — a plain `host:port` without a scheme is treated as SOCKS5, and `http(s)://host:port` without a path is an HTTP proxy,
- or a subscription URL (a URL with a path) — it is auto-detected and all its servers are imported.
The name field is optional (defaults to "Type host", e.g. "VMess example.com"). The **"Расширенный ввод"** ("Advanced input") button opens the full editor with every protocol field. A **"Обновить все"** ("Refresh all") button refreshes every subscription at once.

**B. QR scanner** (camera icon at the top)
Point the camera at a QR code — both proxy links and subscription links are recognized; after scanning, a confirmation card offers **Добавить** (Add) / **Импортировать** (Import) / **Пропустить** (Skip). The scanner also recognizes a TV transfer QR code (`stealtify://…`; see the TV guide). A flashlight toggle is available. Requires camera permission.

**C. Subscription by URL**
Paste a subscription link into the quick-add field. The app downloads the server list and shows a "Подписка импортирована" ("Subscription imported") dialog: "Добавлено прокси: N" ("Proxies added: N").

### Supported link formats
Recognized schemes: `socks5://`, `socks://`, `http://`, `https://` (host:port with no path = HTTP proxy; with a path = subscription), `ss://`, `shadowsocks://`, `vless://`, `vmess://`, `trojan://`, `awg://`, `vpn://` (AmneziaVPN format), `ssh://`, and a bare `host:port` (treated as SOCKS5). The `wg://` scheme is **not** supported. Subscriptions can be a plain link list or an xray JSON config.

### Server actions
On each server's card there are three icons — there is no ⋮ menu and no enable/disable toggle:
- **Проверить** ("Test") — a full protocol handshake plus an external-IP fetch (7 s timeout); shows latency or an error.
- **Редактировать** ("Edit", gear icon) — opens the advanced editor.
- **Поделиться** ("Share") — opens a screen with a QR code and a proxy link you can copy to the clipboard ("Скопировать ссылку"); the link text itself is never shown on screen, and the clipboard entry is marked sensitive. Before the QR code is revealed, a warning dialog "Ссылка содержит учётные данные" ("The link contains credentials") is shown with Показать (Show) / Отмена (Cancel) — the link contains passwords and access keys for the server, so share it only with people you trust.

**Delete is not on the card.** It is inside the advanced editor: a **"Удалить прокси"** ("Delete proxy") button at the bottom opens a confirmation ("Удалить прокси?" … "Это действие нельзя отменить" / "This action cannot be undone").

### Advanced editor
Basic fields: name, protocol type (8 types), host, port (auto-filled with a per-type default: 1080/8080/8388/22/443/443/443/51820), username/password with an "eye" button — shown only for **SOCKS5, HTTP, Shadowsocks and SSH** — and a **"Цепочка через прокси"** ("Chain through proxy") dropdown. Depending on the protocol, extra fields appear:
- **VLESS:** UUID; Security none/tls/reality; Transport tcp/ws/grpc/httpupgrade/mkcp/quic/splithttp; Flow (xtls-rprx-vision); SNI; Fingerprint (chrome, firefox, safari, ios, android, edge, 360, qq, random, randomized); ALPN; Reality Public Key / Short ID / SpiderX; WebSocket path/host; gRPC service name; Header Type; mKCP header + seed; QUIC security/key/header; SplitHTTP path/host; Мультиплексирование (mux) with concurrency 1–16; Фрагментация TLS (TLS fragmentation) with length/interval.
- **VMess:** UUID, Alter ID, Security auto/aes-128-gcm/chacha20-poly1305/none, the same 7 transports, SNI, Fingerprint, ALPN, WebSocket path/host, gRPC service name, Header Type. No Reality.
- **Trojan:** Password (required), Transport (7 options), Security tls/reality, SNI, Fingerprint, ALPN, Reality fields, WebSocket/gRPC fields.
- **Shadowsocks:** encryption method — aes-256-gcm, aes-192-gcm, aes-128-gcm, chacha20-ietf-poly1305, xchacha20-ietf-poly1305 (no SS-2022 or plain); password comes from the common password field.
- **SSH:** host key fingerprint (captured automatically on first connection), cipher (optional). Password authentication only — no key-based auth.
- **AmneziaWG:** private key, peer public key, preshared key, client address (10.0.0.2/32), DNS (1.1.1.1), MTU (1280), keepalive (25), and obfuscation parameters Jc/Jmin/Jmax, S1/S2, H1–H4, I1–I5 (no S3/S4 fields).

**Chain:** works when the outer (last) proxy in the chain is SOCKS5, HTTP, VLESS, VMess or Trojan. SSH, AmneziaWG and Shadowsocks cannot be the outer hop (they ignore the chain setting) but can be used as an inner hop. Chain depth up to 5.

### Subscriptions
Servers from the same subscription are grouped under a collapsed header row showing the subscription title (or "Подписка"), "N прокси" (N proxies), a Refresh button and a Delete button (with confirmation). Tapping the row expands it to show used/total traffic (%) with a progress bar that turns red above 90%, "безлимит" (unlimited) when there is no cap, "Действует до" (valid until) / "Истекла" (expired), and the subscription URL (tap to copy).

**Automatic subscription refresh:** the server list refreshes in the background automatically, roughly every 12 hours when the network is available. The system picks the exact moment, so the gap may be longer. Opening the app or connecting the VPN does not trigger a refresh — use **Refresh** on the subscription card for an immediate update.

Each refresh **replaces the subscription's servers entirely**: the old ones are deleted and re-added from scratch. Manual edits to subscription servers are therefore not preserved, and a group bound to a subscription server loses that binding after refresh and becomes "Без прокси (напрямую)" ("No proxy (direct)"). Automatic refresh cannot be disabled, and the interval cannot be changed in settings.

---

## 4. Rules and groups

The **Rules** tab holds **routing groups**. A group bundles apps and/or domains and is (optionally) bound to a proxy. If no proxy is selected, the group's traffic goes **directly**.

The **+** button at the top offers:
- **New group**
- **App rule** (jumps to the "Apps" screen)

### Creating a group
- Enter a name (e.g. "Video", "Social", "Work").
- Pick a proxy from the list or "No proxy (direct)".

### Group card
Shows:
- The name and an **enabled/disabled** toggle. When the toggle is off, the card shows "Выключена — не маршрутизируется" (Disabled — not routed).
- The group's proxy — `TYPE · host:port` — or "Без прокси (напрямую)" (No proxy, direct).
- The fallback group, if set: "Резерв: <Group> (<server name>)" (Fallback: Group (server name)).
- **Domains** and **Apps** lists, each item removable (an X).

### Managing a group (the ⋮ menu → full-screen **"Редактирование правила"** editor)
- **Rename** — a name field with an OK button.
- **Choose a proxy** for the group.
- **Fallback group** — a dropdown, default "Без резерва" (No fallback); if the group's proxy is unavailable or slow, traffic goes through the fallback group.
- **Add app** ("Добавить приложение") — search with chips **Все / Установленные / Системные** (All / Installed / System), default "Установленные".
- **Add domain** ("Добавить домен", hint text "youtube.com, *.google.com, mail.ru") — only two forms are accepted: `example.com` matches the domain and all its subdomains, `*.example.com` matches subdomains only. There is no separate exact/subdomain/wildcard mode selector. An invalid entry shows "Неверный формат домена" (Invalid domain format).
- **Delete group** ("Удалить правило") — confirmation "Группа «name» и все её правила будут удалены." (Group "name" and all its rules will be deleted.)

---

## 5. App rules

The **Apps** screen ("Правила приложений") — opened from "Rules" → "App rule", or by tapping "Rules" in the Home quick-stats tile. Lets you assign a group to each app.

- **Search** by name.
- **Filters** (chips): Все / Установленные / Системные (All / Installed / System), default Установленные (Installed).
- Tapping an app card opens a dropdown:
  - **No group** — the app works directly (no proxy);
  - or any of the created groups.
- The choice is saved automatically.

> Apps are assigned to **groups**, not to proxies directly. The proxy is set on the group — so a single proxy setup can be reused for many apps.

---

## 6. Settings

Settings are organized into 7 category "folders". At the bottom of the screen there are also "Contact us" and the version number.

### Appearance
- **Dark theme** — a dark/light appearance toggle, on by default. There is no "follow system theme" option.

### Security
- **Kill Switch** — off by default. When the network drops or the app is reconnecting, it keeps the VPN interface open with no traffic passing, so nothing leaks while the app stays alive. It does **not** use Android's system-level VPN lockdown — if the app or its service is killed, protection ends. For an OS-level guarantee, the app shows the hint "Для надёжной защиты включите Always-on VPN в системных настройках" ("For reliable protection, enable Always-on VPN in system settings") with a **VPN** jump button — enable both **Always-on VPN** and **Block connections without VPN** there.
- **Connection logging** ("Логирование соединений") — off by default; records connection events and errors. When enabled, a **"Посмотреть логи"** ("View logs") button appears.

### DNS
- **DNS leak protection** ("Защита от утечек DNS") — DNS queries only through the VPN tunnel (enabled by default). All DNS from apps is intercepted (port 53); when domain rules or DNS filtering are active, other apps' DoT/DoH (port 853, known DoH IPs) is blocked too, so domain rules keep working.
- **DNS filtering** ("DNS-фильтрация") — block ads and trackers via DNS; off by default. Uses a **built-in list of about 90 domains** shipped inside the app — it is not downloaded or updated over the network.
- **DNS servers** — pick a provider from a single list of 9 presets. Entries marked with a lock 🔒 encrypt your queries; the others do not:
  - Cloudflare (1.1.1.1) — default,
  - Cloudflare · DoT 🔒 and Cloudflare · DoH 🔒,
  - Google (8.8.8.8) and Google · DoT 🔒,
  - AdGuard (94.140.14.14) and AdGuard · DoT 🔒,
  - Quad9 · DoT 🔒,
  - **Свои DNS** (Custom DNS) — DNS 1 (primary) and DNS 2 (secondary) fields. Accepted formats: a plain IP (`9.9.9.9`), `tls://9.9.9.9#dns.quad9.net`, or `https://dns.quad9.net/dns-query#9.9.9.9` — an IP address is required, a hostname alone is rejected. A **"Сохранить DNS"** ("Save DNS") button applies the choice, after which the app asks you to reconnect.

  DoT (DNS-over-TLS) and DoH (DNS-over-HTTPS) hide from your ISP which sites you open. Encrypted DNS queries are sent through the default proxy, and results honour the record's TTL.
- **Encrypted DNS only** ("Только шифрованный DNS") — off by default. Encrypted presets normally keep an unencrypted fallback: if your ISP blocks DoT/DoH, queries silently go out in the clear. This setting removes that fallback — resolution fails instead, but nothing leaves unencrypted; a fallback-to-plaintext event is logged as "Шифрованный DNS недоступен — откат на обычный DNS" when the setting is off and a downgrade happens.

### Connection
- **Auto-reconnect** — restore the connection when the network changes (enabled by default).
- **Auto-start on boot** — off by default; launches the VPN automatically after a device restart, but only if VPN permission was already granted earlier.
- **Failover proxy** — off by default. When enabled, checks the proxy before connecting (and whenever the Home screen opens) and switches to a backup if it's unavailable. Controlled by a **"Порог задержки"** ("Latency threshold") slider from 500 ms to 30 s, default 3 s: if latency is higher, or the check fails, the fallback group is used. The check is a TCP connect to host:port (a UDP probe for AmneziaWG), capped at 10 s. Note: the **default proxy itself is not auto-switched** — if it goes down, connections through it simply fail.

### Notifications
- **Traffic statistics** ("Статистика трафика") — off by default; shows proxy/direct speeds in the VPN notification. When enabled, if system notifications are off, the app asks for notification permission.

### Data
- **Configuration backup** — export/import proxies, rules and settings.
  - **Export** — saves the entire configuration to a file `stealtify_backup.stbackup` (via the system file picker), encrypted with a key built into the app rather than a password you choose — it stops casual reading but not a determined attacker with the app itself. It contains your proxies **with their passwords and keys**, groups, app rules and domain rules, plus two settings (dark theme, auto-reconnect); treat the file as a secret. The legacy plain-JSON format is still supported when importing.
  - **Import** — ⚠️ **WARNING:** the system file picker opens immediately and, once you pick a file, it completely REPLACES all current configuration with the new one (proxies, rules, groups) **at once, with no confirmation dialog**. The old configuration is deleted. Export your current state first if you want to keep it.

### Updates
- **Check for updates** ("Проверить обновления") — shows the current/available version. Checked automatically when the Home screen opens, and on manual **"Проверить"** ("Check") in this card — there is no periodic background check. The button cycles through **Проверить / Обновить / Установить / Повторить** (Check / Update / Install / Retry), with **Отмена** (Cancel) available during download.

### At the bottom of the screen
- **Contact us** ("Связаться с нами") — an email to support@stealtify.app.
- The app **version**, e.g. "Stealtify 1.0.0 (108)".

---

## 7. Connection logs

Opened from Settings → Security → "View logs" (when logging is enabled).

- Shows 8 event types: connect, disconnect, error, DNS query, network change, Kill Switch, reconnect, and update check — each with its own icon and color. There is no filter.
- Each entry has: time (HH:MM:SS), text, and optional details.
- A counter shows "N записей" (N entries). The clear button (trash) is shown only when there are entries and deletes all of them. Logs are kept in memory (up to 500 entries) and lost on restart.

---

## 8. How routing works

For each connection, the decision is made by priority:

1. **App rule** → the app's group and its proxy (e.g. YouTube → the "Video" group → its proxy). A group with "No proxy (direct)" sends the app's traffic directly, bypassing the VPN interface entirely.
2. **Domain rule** → its group's proxy or direct. The domain is learned from the app's DNS answers or from the TLS SNI on port 443 (e.g. `youtube.com` → the "Video" group).
3. If at least one domain rule exists anywhere in the app but none matched this connection → **direct**.
4. **Private/LAN, link-local, loopback and multicast destinations** → direct. This check happens only after steps 1–3, so an explicit app rule still sends LAN traffic through a proxy if you set one up that way.
5. Otherwise → the **default proxy** (the server selected in the Home "Proxies (check)" tile, or the first active server if none was picked).

Consequences: with no rules configured at all, **all traffic goes through the default proxy** — it is not sent directly. Use Rules/Groups to carve out apps or domains that should go direct or through a different proxy.

Additionally: **proxy chains** (traffic passes through several servers), **failover** by latency (the default proxy itself is not auto-switched), and the **Kill Switch**, which keeps the VPN interface open with no traffic passing while the network is down or reconnecting.

---

## 9. Common tasks

**Connect to the VPN**
Home → **Connect** button → confirm the VPN permission (on first launch).

**Add a proxy manually**
Proxies → **+** → paste the link/details → (if needed, "Advanced input") → **Add**.

**Import by QR**
Proxies → camera icon → point at the QR code.

**Import a subscription**
Proxies → **+** → paste the subscription URL → "Proxies added: N".

**Route an app through a proxy**
Rules → create a group with a proxy → Apps → assign that group to the app.
(Or add the app directly to the group via its menu.)

**Route a site through a proxy**
Rules → open/create a group → add a domain (`example.com` or `*.example.com`).

**Choose the default server**
Home → **"Прокси (проверка)"** ("Proxies (check)") tile → tap a row to make it the default server.

**Delete a proxy**
Proxies → open the server's **Редактировать** (Edit) editor → **"Удалить прокси"** ("Delete proxy") at the bottom → confirm.

**Set up a backup for proxy failure**
Settings → Connection → enable **Failover**, set the latency threshold. For a group, set a **fallback group**.

**Enable the Kill Switch**
Settings → Security → **Kill Switch** (also enabling Always-on VPN in the system is recommended).

**Back up / restore**
Settings → Data → **Export** (saves `stealtify_backup.stbackup`) / **Import** (opens the file picker immediately and replaces the whole configuration as soon as you pick a file, with no confirmation prompt — back up first!).

---

## 10. App permissions

- **VPN service** — the core function (traffic interception), run as a foreground service (also used for update downloads).
- **Camera** — scanning QR codes.
- **Notifications** — stats in the shade and the running status.
- **No storage permission** — export/import use the system file picker instead.
- **Install packages** — installing downloaded updates.
- **Query installed apps** — building the app list for rules.
- **Network state** — auto-reconnect and auto-start.
- **Boot completed** — auto-start on boot (if enabled and permission was already granted).

### Network connections the app makes on its own

There are no analytics or crash-reporting SDKs and no account. Besides your proxy servers, the app contacts:

- **update.stealtify.app** — checked when the Home screen opens and on a manual check, and used to download the APK when you install an update.
- **ipapi.co** — looked up to show the country on the "External IP" tile; this request is sent **directly, not through the proxy**, so this service sees your real exit IP.
- **api.ipify.org**, **ifconfig.me**, **icanhazip.com** — external-IP echo services used during a server "Проверить" ("Test") check; these requests go **through the proxy being tested**.
- **Your subscription URLs** — each request carries a random per-install identifier header (`X-Hwid`) and a User-Agent.
- **The DNS servers you selected** in Settings.

---

*The app's interface is in Russian; technical terms (UUID, SNI, ALPN, gRPC, MTU, etc.) are kept in their conventional form. There is no language setting — no English (or other) interface resources exist.*
