# Stealtify TV — Installation

**Stealtify TV** routes the traffic of your Android TV box through your own proxy servers.
No root required. Supports SOCKS5, HTTP, Shadowsocks, SSH, VLESS, VMess, Trojan and AmneziaWG.

> 📘 What the TV build can do and how it differs from the phone build — see
> **[TV_USER_GUIDE.md](TV_USER_GUIDE.md)** next to this file.
> 🇷🇺 Russian version: **[TV_INSTALL.ru.md](TV_INSTALL.ru.md)**.

---

> ⚠️ **Stealtify TV is a beta.**
> Android TV support is under active development. Expect rough edges and
> interface changes between versions.
> Found a problem? Open an Issue labelled `tv` and include your box model,
> Android version and CPU architecture (see [Which build to download](#which-build-to-download)).

---

## Requirements

- Android TV / Google TV **10** or newer.
- A set-top box, a TV with built-in Android TV, or a TV stick.
- At least one proxy server (your proxy/VPN provider supplies the details).
- A phone with Stealtify installed — **strongly recommended**: it is by far the
  easiest way to move your configuration across without typing anything on a
  remote. See [Transferring the configuration from a phone](TV_USER_GUIDE.md#2-transferring-the-configuration-from-a-phone).
- Interface language: Russian.

The mobile build does **not** interfere with the TV build: they use different
application IDs, update independently, and can coexist on the same device.

---

## Which build to download

Unlike the phone version, **four files** are published for TV boxes. Boxes come
in both 64-bit and 32-bit flavours, so picking the right one matters.

| File | For |
|------|-----|
| `Stealtify_<version>-tv_arm64-v8a.apk` | Most modern boxes (64-bit) |
| `Stealtify_<version>-tv_armeabi-v7a.apk` | Boxes running a 32-bit system |
| `Stealtify_<version>-tv_x86.apk` | Android TV emulator (developers) |
| `Stealtify_<version>-tv_universal.apk` | Universal: works everywhere, but roughly **twice the size** |

**Not sure which architecture you have?** Take `universal` — it is guaranteed to
install. To save space, you can determine the architecture like this:

- Install **AIDA64** or **CPU-Z** from Google Play on the box → the **CPU** /
  **System** section → the ABI line: `arm64-v8a` or `armeabi-v7a`.
- Or from a computer with ADB connected (see [Method 2](#method-2-adb-from-a-computer)):

  ```powershell
  adb shell getprop ro.product.cpu.abi
  ```

If you install the wrong file, Android refuses it with "App not installed" or
"Package appears to be incompatible". No harm done — download `universal` instead.

---

## Installation

Android TV has no ordinary file manager or browser, so installation differs from
the phone. Pick any of the three methods.

### Method 1 — the Downloader app (easiest, no computer needed)

1. On the box, open **Google Play** and install **Downloader** (by AFTVnews) —
   free, and available on most Android TV devices.
2. Launch Downloader and type the APK URL into the address field using the remote.
3. Wait for the download — installation is offered automatically.
4. If prompted, allow **installing from unknown sources** for Downloader (the
   toggle appears right away, with a shortcut into settings).
5. Press **Install**.

> Typing long URLs on a remote is painful. If your link is long, use Method 2 or 3.

### Method 2 — ADB from a computer

Works when the box and the computer are on the same network.

1. On the box: **Settings → About → Build** — press it 7 times until "You are now
   a developer" appears.
2. **Settings → Developer options** → enable **USB debugging** and
   **Network debugging** (the exact name depends on the firmware).
3. Note the box's IP address there (or under **Settings → Network**).
4. On the computer:

   ```powershell
   adb connect 192.168.1.50:5555
   adb install Stealtify_<version>-tv_arm64-v8a.apk
   ```

   Substitute your IP and the file you downloaded. On first connection the box
   shows a confirmation prompt — accept it with the remote.

### Method 3 — USB drive or network share

1. Copy the APK onto a USB drive from your computer.
2. Plug the drive into the box.
3. Install a file manager from Google Play (for example **X-plore File Manager**
   or **File Commander**), open the drive and launch the APK.
4. Allow installation from unknown sources for that file manager.

---

## First launch

1. Open **Stealtify TV** — the launcher shows it as "Stealtify TV".
2. Transfer your configuration from the phone: the **Proxies** tab → the
   **Импорт с телефона** ("Import from phone") icon → a QR code appears on
   screen. Details in
   [TV_USER_GUIDE.md](TV_USER_GUIDE.md#2-transferring-the-configuration-from-a-phone).
3. On **Home**, press the large connect button.
4. On the first connection Android shows a VPN connection request — confirm it
   with the remote (**OK** / **Allow**).

> ℹ️ If the VPN permission dialog never appears, or the app closes when you press
> connect — see [Known limitations](#known-limitations).

---

## Verifying file integrity (optional)

A SHA-256 checksum is published for every build — a separate one for each of the
four files. The easiest place to check it is on your computer, before copying the
file to the box:

```powershell
Get-FileHash .\Stealtify_<version>-tv_arm64-v8a.apk -Algorithm SHA256
```

```bash
sha256sum Stealtify_<version>-tv_arm64-v8a.apk
```

The result must match the checksum listed for **your** file. Checksums differ
between architectures — that is expected.

---

## Updates

The app checks for updates itself and downloads the build matching your box's
architecture. An update prompt appears on the Home screen and under
**Settings → Updates**.

The TV and mobile builds update through **separate** channels and do not affect
each other.

---

## Known limitations

This is a beta, and some things behave differently on TV boxes than on phones.

| Limitation | What to do |
|---|---|
| **The VPN permission is never requested.** Some Android TV firmwares ship without the system VPN dialog. | Check **Settings → Network → VPN** on the box. If there is no such section, the box does not support VpnService and the app cannot work. Please report the model to us. |
| **No QR scanner.** TV boxes have no camera. | Transfer the configuration from a phone over the local network, or add proxies via a subscription link. |
| **No Quick Settings tile.** Android TV has no quick settings shade. | Control the connection from inside the app. |
| **No Data section (backups).** Configuration arrives from the phone; per-app rules work with the box's own apps. | Transfer the configuration from a phone, or add proxies via a subscription link. |
| **Import from phone replaces the box's existing configuration** (proxies, groups, rules). | The TV build has no backup feature — if the box already holds a configuration you want to keep, do not import over it. |
| **No launcher icon after installing.** Some firmwares hide apps that lack a TV banner. | Find the app under **Settings → Apps → See all apps** and launch it there, or use the launcher's search. |

---

## Help

Questions or problems — get in touch:
**Settings → Contact us** (or **support@stealtify.app**).
Website: https://stealtify.app
For box-specific problems, please include the model, Android version and ABI.
