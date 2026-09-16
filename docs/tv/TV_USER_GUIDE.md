# Stealtify TV — User Guide

What the Android TV build can do, and how it differs from the phone build.

Stealtify TV is the same app as on the phone, built for a TV box. The engine,
the protocols and the security settings are identical. What differs is the
**input method** (a remote instead of a finger) and the **set of screens**: some
features make no sense on a television and have been removed.

> 🛠 Installation and choosing a build — **[TV_INSTALL.md](TV_INSTALL.md)**.
> 📘 Full description of the shared features (protocols, DNS, Kill Switch,
> subscriptions) — **[USER_GUIDE.md](../USER_GUIDE.md)**. This file covers only
> what is TV-specific.
> 🇷🇺 Russian version: **[TV_USER_GUIDE.ru.md](TV_USER_GUIDE.ru.md)**.

---

> ⚠️ **Stealtify TV is a beta.** Expect rough edges and interface changes
> between versions.

---

## Contents

1. [How the TV build differs from the phone build](#1-how-the-tv-build-differs-from-the-phone-build)
2. [Transferring the configuration from a phone](#2-transferring-the-configuration-from-a-phone)
3. [If the transfer fails](#3-if-the-transfer-fails)
4. [Using the remote](#4-using-the-remote)
5. [The screens](#5-the-screens)
6. [How routing works on TV](#6-how-routing-works-on-tv)
7. [Troubleshooting](#7-troubleshooting)

---

## 1. How the TV build differs from the phone build

| Feature | Phone | Android TV | Why |
|---|:---:|:---:|---|
| Proxy servers, protocols, subscriptions | ✅ | ✅ | Same engine |
| Kill Switch, DNS leak protection, ad blocking | ✅ | ✅ | Identical |
| Statistics, connection logs, server checks | ✅ | ✅ | Identical |
| Configuration transfer from a phone over the network | — | ✅ | Replaces typing on a remote |
| Scanning a QR code with the camera | ✅ | — | TV boxes have no camera |
| Per-app routing, **Rules** tab | ✅ | ✅ | Works; the app list is the box's own apps |
| Notifications (traffic stats) | ✅ | ✅ | Offered, but Android TV usually shows no notifications |
| The **Data** section (backups) | ✅ | — | The configuration arrives from the phone over the network |
| Dashboard tile editor | ✅ | — | Drag and drop is impossible with a remote |
| Quick Settings tile | ✅ | — | Android TV has no quick settings shade |

The interface is additionally **more compact** on a television: the screens were
laid out for a phone and would look needlessly oversized on a large display.

---

## 2. Transferring the configuration from a phone

The headline feature of the TV build. Typing server addresses, UUIDs and Reality
keys on a remote is close to impossible, so the whole configuration is carried
over from the phone — across the local network, in a single action.

### What you need

- A phone with Stealtify installed and your proxies already configured.
- **The phone and the TV on the same network** — this is mandatory.

### Steps

1. **On the TV:** open the **Proxies** tab → the **Импорт с телефона** ("Import
   from phone") icon at the top of the screen.
2. A **QR code** appears, along with a line such as
   `Адрес телевизора: 192.168.1.50:8787` ("TV address"). The port shown may be
   anywhere from 8787 to 8796 — the QR code always carries the actual port.
3. **On the phone:** open Stealtify → the **Proxies** tab → the **QR scanner** icon.
4. Point the phone at the TV screen. The phone shows a confirmation card with the
   TV's address — tap **Отправить** ("Send") to proceed. Nothing is sent without
   this explicit tap.
5. The phone encrypts the configuration and sends it to the TV; the big screen
   shows a message such as "Импортировано: 5 прокси, 2 групп" ("Imported: 5
   proxies, 2 groups").
6. Press **Готово** ("Done").

### What gets transferred

**Proxy servers (with their passwords/keys), groups and domain rules** —
everything needed to work on a TV. Servers that came from a subscription keep
their subscription link and keep auto-refreshing on the TV afterwards.

**Per-app rules from the phone are not transferred** — the box does not have the
same apps installed, so those rules are meaningless there. If any existed, the
app says so plainly: "Правила для приложений телефона (N) пропущены" ("Phone
app rules (N) skipped"). DNS settings and other phone settings are not part of
the transfer either.

**Importing replaces whatever configuration already exists on the TV** — the
box's current proxies, groups and rules are removed and replaced by what the
phone sends. There is no merge and no confirmation prompt on the TV side.

### How safe is this

What travels is not a "list of settings" but the **access keys to your VPN
servers** — passwords, UUIDs, private keys. Hence the design of the channel:

- **The encryption key travels optically** — inside the QR code on the TV screen,
  not over the network. The same principle as pairing a Chromecast or signing in
  to WhatsApp Web.
- **Only ciphertext goes over the network** (AES-GCM). A neighbour listening to
  your Wi-Fi reads nothing.
- **The server on the TV is single-use**: it starts only on that screen, accepts
  one successful connection and then shuts down. The key lives no longer than
  5 minutes, and the server accepts at most 3 simultaneous clients and 20 failed
  attempts before giving up.
- A request without the correct key is rejected — a stray app on your network
  cannot inject anything.

---

## 3. If the transfer fails

The most common cause is **the two devices being on different networks**. Compare
the addresses: the TV shows its own below the QR code, the phone shows its own on
the scanner screen. **The first three groups of digits must match:**
`192.168.1.50` and `192.168.1.77` are the same network, while `192.168.1.50` and
`192.168.0.12` are not.

| Situation | Fix |
|---|---|
| TV on Ethernet, phone on Wi-Fi | Usually fine. If not, connect the phone to the same router over Wi-Fi. |
| Phone on a **guest** Wi-Fi network | Guest networks isolate devices from each other. Switch the phone to the main network. |
| Phone on mobile data (LTE) | Turn on Wi-Fi on the phone. |
| Client isolation (AP isolation) enabled on the router | Disable it in the router settings, or use the fallback below. |
| The TV says "This is an emulator address" | You are running the app in an emulator — the phone cannot reach it. Use a real box. |

### Fallback — a subscription URL

If a network transfer is impossible, add your servers via a **subscription link**:
it is short enough to type on a remote once.

The **Proxies** tab → **+** → paste the subscription link. The server list will
refresh automatically from then on.

---

## 4. Using the remote

- **Arrow keys** — move between elements. The focused element is highlighted.
- **OK / centre button** — activate.
- **Back** — return to the previous screen.
- **Switching tabs** — press up until you reach the tab bar at the top of the
  screen, then move left/right.

No gestures are needed on TV: every action is a button. Group settings open from
the **⋮** button on the group card; proxy actions are the icon buttons on the
server card.

---

## 5. The screens

### Home

The connect button and the tunnel status, plus the same tiles as on the phone
(speed, external IP, quick stats, proxy check, traffic, apps by traffic), shown
when relevant.

The layout is fixed on TV — the tile editor is hidden, since rearranging tiles
with a remote is not possible.

### Proxies

The server list, shown in two columns. At the top of the screen: the **Импорт с
телефона** ("Import from phone") button and the **Добавить** ("Add") button for
adding a server manually or by link.

Each server card has three icon buttons: **Проверить** ("Test"), **Редактировать**
("Edit"), **Поделиться** ("Share"). Deleting a server is done inside the editor,
not from the card.

### Settings

The same categories as on the phone, **except the "Data" section**:

- **Appearance** — theme.
- **Security** — Kill Switch, logging.
- **DNS** — leak protection, ad blocking, provider selection.
- **Connection** — auto-connect, auto-start when the box powers on, failover.
- **Notifications** — statistics display.
- **Updates** — check for and install a new version.

Auto-start on boot is especially apt on a box: the TV switches on and the tunnel
comes up by itself.

### Connection logs

A connection journal (no filter). Useful for confirming that traffic is going
through the intended server.

---

## 6. How routing works on TV

Routing works exactly as on the phone: with no rules configured, all traffic
goes through the default proxy; per-app rules apply to the box's own apps;
domain rules and fallback groups work; local (LAN) addresses go direct unless
an app rule explicitly sends that app through a proxy.

---

## 7. Troubleshooting

| Problem | What to check |
|---|---|
| The connect button does nothing / the app closes | The box may not support VPN. Check **Settings → Network → VPN** in the TV's system settings. If there is no such section, please report the model to us. |
| The VPN permission dialog never appeared | Same as above. Without system VpnService support the tunnel cannot come up. |
| No launcher icon after installing | **Settings → Apps → See all apps** → launch Stealtify TV from there. |
| The phone cannot find the TV during transfer | See [section 3](#3-if-the-transfer-fails) — almost always different networks. |
| The app would not install | Most likely the wrong architecture. Download the `universal` build — see [TV_INSTALL.md](TV_INSTALL.md#which-build-to-download). |
| The interface is too small or too large | The scale is tuned for 1080p. If it is awkward on your screen, let us know your TV's resolution. |
| The interface says "Stealtify" while the launcher says "Stealtify TV" | Expected — the app title inside the interface is shared with the phone build. |

---

## Help

Questions or problems — **Settings → Contact us** or **support@stealtify.app**.
Website: https://stealtify.app
For box-specific problems, please include the model, Android version and architecture.
