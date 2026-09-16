# Stealtify — Per-App Proxy Client for Android

<p align="center">
  <b>Маршрутизация трафика каждого приложения через свой прокси. Без root.</b>
</p>

<p align="center">
  <a href="#возможности">Возможности</a> •
  <a href="#как-это-работает">Как это работает</a> •
  <a href="#установка">Установка</a> •
  <a href="#использование">Использование</a> •
  <a href="#-android-tv">Android TV</a> •
  <a href="#документация">Документация</a>
</p>

<p align="center">🇬🇧 English version: <a href="./README.md">README.md</a></p>

<p align="center">🌐 Сайт: <a href="https://stealtify.app">stealtify.app</a> · 📥 Загрузки: <a href="https://update.stealtify.app">update.stealtify.app</a></p>

---

## Документация

| Документ | Описание |
|----------|----------|
| [📥 Установка](./docs/INSTALL.ru.md) | Установка и проверка контрольной суммы |
| [📚 Руководство пользователя](./docs/USER_GUIDE.ru.md) | Полное руководство |
| [📺 Android TV](./docs/tv/TV_INSTALL.ru.md) | Установка и руководство для ТВ-сборки |
| [🛠 Решение проблем](./docs/TROUBLESHOOTING.md) | Частые проблемы и их решения |
| [🔒 Конфиденциальность](./docs/PRIVACY.md) | К чему приложение обращается, а к чему — нет |
| [📋 Roadmap](./docs/ROADMAP.md) | Что готово и что запланировано |
| [📝 Changelog](./CHANGELOG.md) | История релизов |
| [⚖️ Лицензии зависимостей](./docs/LICENSES.md) | Лицензии сторонних компонентов |

---

## Возможности

- 🎯 **Per-app маршрутизация** — назначайте разные прокси разным приложениям
- 🌐 **Доменные правила** — по ответам DNS и по TLS SNI
- 🔗 **8 протоколов** — SOCKS5, HTTP CONNECT, SSH, VLESS, VMess, Trojan, Shadowsocks, AmneziaWG
- 🚀 **Двойной движок** — Kotlin TCP/UDP стек (SOCKS5, HTTP CONNECT) + Go-движок (xray-core для VLESS/VMess/Trojan, плюс SSH, Shadowsocks, AmneziaWG)
- 🔍 **UID-идентификация** — точное определение приложений через `getConnectionOwnerUid()` (Kotlin, а не JNI callback)
- 📊 **Мониторинг** — логи подключений, статистика трафика в реальном времени
- 🔒 **Kill Switch** — защита внутри приложения на время восстановления туннеля; для гарантии на уровне ОС включите Always-on VPN
- 🚫 **DNS фильтрация** — встроенный список блокируемых доменов, по умолчанию выключена
- 🔋 **Без root** — работает на стоковом Android 10+ через VpnService API
- 📱 **Material You** — современный UI на Jetpack Compose + Material 3
- 📥 **Импорт URI** — ссылки `vless://`, `vmess://`, `trojan://`, `ss://`, `socks5://`, `http://`, `ssh://`, `awg://`, `vpn://`
- 📷 **QR-код импорт** — сканирование QR-кодов с прокси-конфигурацией
- 🔗 **Поделиться прокси** — QR-код и копирование ссылки в буфер обмена
- 🔐 **Шифрованный DNS (DoT/DoH)** — с пресетами Cloudflare, Google, AdGuard, Quad9
- ✅ **Проверка подлинности** — каждая сборка подписана и проверяется при запуске; поддельные сборки отвергаются
- ♻️ **Авто-старт** — запуск VPN при загрузке устройства
- ♥️ **Failover & Health Check** — автоматический мониторинг и переключение прокси
- 📺 **Android TV** — отдельная сборка (см. ниже)
- 🇷🇺 **Язык интерфейса: русский**

## Требования

- Android 10+ (API 29+)
- Архитектура: телефон — arm64-v8a; сборка для Android TV — arm64-v8a / armeabi-v7a / x86
- Root не требуется

## Как это работает

```
Приложение (YouTube) → VpnService TUN → Kotlin TunPacketProcessor
    → getConnectionOwnerUid() → "com.google.android.youtube"
    → Правило: YouTube → SOCKS5 proxy1:1080
    → Трафик маршрутизируется через proxy1

Приложение (Chrome) → VpnService TUN → Kotlin TunPacketProcessor
    → getConnectionOwnerUid() → "com.android.chrome"
    → Правило не найдено → прокси по умолчанию

Приложение в группе без назначенного прокси
    → Direct (напрямую, минуя VPN-интерфейс)
```

1. **VpnService** создаёт TUN-интерфейс, перехватывая весь трафик устройства
2. **Kotlin TunPacketProcessor** парсит каждое TCP/UDP соединение
3. Приложение определяется через `getConnectionOwnerUid()`
4. **RouteResolver** ищет правило (app → domain → прокси по умолчанию)
5. Если правило есть → трафик идёт через прокси из этого правила (или напрямую, если у группы правила нет прокси)
6. Если правила нет → трафик идёт через прокси по умолчанию

## Установка

1. Скачайте последний APK из [Releases](../../releases)
2. Установите на устройство с Android 10+
3. Подтвердите разрешение на VPN

Пошаговая инструкция и проверка контрольной суммы: **[docs/INSTALL.ru.md](./docs/INSTALL.ru.md)**.
Полное руководство пользователя: **[docs/USER_GUIDE.ru.md](./docs/USER_GUIDE.ru.md)**.

## Использование

### 1. Добавьте прокси

**Прокси** → **+** → настройте (или импортируйте URI: `vless://...`, `ss://...`)

### 2. Создайте правила

**Правила** → выберите приложение → назначьте прокси

### 3. Подключитесь

Нажмите **Подключить** на главном экране.

---

## Поддерживаемые протоколы

| Протокол | Auth | UDP |
|----------|------|-----|
| SOCKS5 | ✅ user:pass | ✅ (UDP ASSOCIATE) |
| HTTP CONNECT | ✅ Basic | ❌ |
| SSH Tunnel | ✅ password | ✅ |
| VLESS (+ Reality, XTLS-Vision) | ✅ UUID | ✅ (xray-core) |
| VMess | ✅ UUID | ✅ (xray-core) |
| Trojan (+ Reality) | ✅ password | ✅ (xray-core) |
| Shadowsocks | ✅ password | ✅ (Go engine) |
| AmneziaWG | ✅ privateKey | ✅ (amneziawg-go) |

## FAQ

**Q: Требуется ли root?**
A: Нет. Используется стандартный Android VpnService API.

**Q: Можно ли использовать вместе с другим VPN?**
A: Нет. Android допускает только один активный VPN.

**Q: Как определяется приложение-источник пакета?**
A: Через `ConnectivityManager.getConnectionOwnerUid()` (API 29+).

**Q: Что происходит с приложениями без правил?**
A: Идут через прокси по умолчанию. Чтобы отправлять приложение напрямую, поместите его в группу без прокси.

**Q: Отправляет ли приложение телеметрию?**
A: Нет SDK аналитики и учётной записи. Приложение обращается к серверу обновлений, ipapi.co (страна для плитки «Внешний IP», напрямую), сервисам определения внешнего IP при проверке серверов (через прокси), а также к вашим серверам подписок и DNS. См. USER_GUIDE.ru.md §10.

## 📺 Android TV

Stealtify также поставляется сборкой для Android TV — отдельным пакетом `com.stealtify.app.tv`.

Статус: **beta** — возможны шероховатости; см. TV-руководства.

- Четыре APK: arm64-v8a, armeabi-v7a, x86 и универсальный вариант.
- Интерфейс с верхней панелью навигации, адаптированный под пульт (D-pad) вместо сенсора.
- Перенос конфигурации с телефона по локальной сети — на ТВ-сборке нет сканера QR-кодов
  и плитки быстрых настроек (на Android TV нет камеры и шторки уведомлений).

Инструкции: [docs/tv/TV_INSTALL.ru.md](./docs/tv/TV_INSTALL.ru.md) · [docs/tv/TV_USER_GUIDE.ru.md](./docs/tv/TV_USER_GUIDE.ru.md)

## Лицензия

Проприетарная лицензия (EULA) — Copyright © 2025–2026 Stealtify. Все права защищены.
См. [LICENSE](./LICENSE). Сторонние компоненты (MPL-2.0 / Apache-2.0 / BSD / MIT)
сохраняют свои лицензии — см. [NOTICE](./NOTICE) и [docs/LICENSES.md](./docs/LICENSES.md).

---

<p align="center">
  Made with ❤️ for privacy and freedom
</p>

---

📥 [Установка](./docs/INSTALL.ru.md) · 📚 [Руководство](./docs/USER_GUIDE.ru.md) · 📋 [Roadmap](./docs/ROADMAP.md) · 🔒 [Конфиденциальность](./docs/PRIVACY.md)