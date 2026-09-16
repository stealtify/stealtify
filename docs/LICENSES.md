# Лицензии сторонних компонентов — Stealtify

> Лицензии всех прямых и значимых transitive-зависимостей.
> Последняя сверка: **v1.40.1** (август 2026 г.).

Само приложение распространяется под **проприетарной лицензией (EULA)** —
см. [LICENSE](../LICENSE). Публикуется собранный APK и документация;
исходный код приложения закрыт.

Перечисленные ниже зависимости (MPL-2.0 / Apache-2.0 / BSD / MIT /
LGPL-3.0-linking-exception) допускают такое распространение при сохранении их
атрибуций — см. [NOTICE](../NOTICE).

Проект **не содержит компонентов под GPL-3.0**: Shadowsocks реализован
собственными силами (SIP004 AEAD поверх стандартной библиотеки Go и
`golang.org/x/crypto`), библиотеки `sagernet/sing` и `sagernet/sing-shadowsocks`
не используются.

## ⚠️ MPL-2.0 (xray-core)

В состав входит **изменённая** версия xray-core. MPL-2.0 обязывает предоставлять
получателям APK исходные тексты **изменённых файлов** — даже при закрытом
основном коде.

Исходники изменённых файлов предоставляются бесплатно любому получателю
по письменному запросу на **support@stealtify.app**.

---

## Лицензии зависимостей

### Android (Kotlin / JVM)

| Зависимость | Лицензия | Совместимость |
|-------------|----------|---------------|
| AndroidX (`core`, `lifecycle`, `activity`, `compose.*`, `navigation`, `camera`, `security-crypto`, `room`, `hilt-navigation-compose`) | Apache-2.0 | OK |
| Jetpack Compose BOM | Apache-2.0 | OK |
| Material Components / Material Icons Extended | Apache-2.0 | OK |
| Dagger / Hilt (`com.google.dagger:*`) | Apache-2.0 | OK |
| KSP (`com.google.devtools.ksp`) | Apache-2.0 | OK |
| Kotlin stdlib / coroutines / serialization | Apache-2.0 | OK |
| Coil (`io.coil-kt:coil-compose`) | Apache-2.0 | OK |
| ML Kit barcode-scanning | Google ML Kit ToS (Apache-2.0-совместимо) | OK |
| JUnit 4 | EPL-1.0 (тесты, не входит в APK) | OK |
| MockK | Apache-2.0 | OK |
| Robolectric | MIT | OK |
| Espresso / androidx.test | Apache-2.0 | OK |

### Go Engine

| Зависимость | Лицензия | Совместимость |
|-------------|----------|---------------|
| `github.com/xtls/xray-core` | MPL-2.0 | OK (требование: сохранять MPL-заголовки) |
| `github.com/xtls/reality` | MPL-2.0 | OK |
| `github.com/amnezia-vpn/amneziawg-go` | MIT | OK |
| `golang.zx2c4.com/wireguard` | MIT | OK (upstream WireGuard-Go) |
| `golang.org/x/crypto`, `x/mobile`, `x/net`, `x/sys`, `x/text`, `x/mod`, `x/tools`, `x/exp`, `x/sync`, `x/time` | BSD-3-Clause | OK |
| `gvisor.dev/gvisor` | Apache-2.0 | OK |
| `github.com/refraction-networking/utls` | BSD-3-Clause | OK |
| `github.com/apernet/quic-go` | MIT | OK |
| `github.com/quic-go/qpack` | MIT | OK |
| `github.com/miekg/dns` | BSD-3-Clause | OK |
| `github.com/cloudflare/circl` | BSD-3-Clause | OK |
| `github.com/gorilla/websocket` | BSD-2-Clause | OK |
| `github.com/juju/ratelimit` | LGPL-3.0-linking-exception | OK |
| `github.com/klauspost/compress` | BSD-3-Clause / Apache-2.0 (mixed) | OK |
| `github.com/klauspost/cpuid/v2` | MIT | OK |
| `github.com/andybalholm/brotli` | MIT | OK |
| `github.com/pelletier/go-toml` | MIT | OK |
| `github.com/pires/go-proxyproto` | Apache-2.0 | OK |
| `github.com/vishvananda/netlink` | Apache-2.0 | OK |
| `github.com/vishvananda/netns` | Apache-2.0 | OK |
| `github.com/ghodss/yaml` | MIT + BSD-3-Clause | OK |
| `github.com/google/btree` | Apache-2.0 | OK |
| `gopkg.in/yaml.v2` | Apache-2.0 + MIT | OK |
| `go4.org/netipx` | BSD-3-Clause | OK |
| `google.golang.org/grpc` | Apache-2.0 | OK |
| `google.golang.org/protobuf` | BSD-3-Clause | OK |
| `google.golang.org/genproto/googleapis/rpc` | Apache-2.0 | OK |
| `lukechampine.com/blake3` | MIT | OK |
| `golang.zx2c4.com/wintun` | MIT (не попадает в Android-сборку) | OK |

---

## Атрибуция

- **В APK** — атрибуции из `NOTICE` включены в сборку.
- **В Play Listing** — указано использование xray-core (MPL-2.0) и AmneziaWG (MIT).

---

📄 [NOTICE](../NOTICE) · ⚖️ [LICENSE](../LICENSE)
