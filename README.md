# Shadowrocket Configurations for Russia (ULTRA Edition 2026)

🚀 **Самый продвинутый набор оптимизированных конфигураций Shadowrocket для бесшовного интернета на macOS и iOS в условиях 2026 года.**

## Главные фишки версии ULTRA

В этой версии мы выжали максимум из возможностей Shadowrocket для работы в сложной сетевой среде.

### 🚕 Yandex Go & 2GIS Fix
- Приложения **Яндекс Go** и **2ГИС** работают напрямую без прокси. Решает проблему «ошибки соединения с сервером» при включённом VPN и проблемы с загрузкой карт/геопозиции.

### 🎧 Discord — Полное покрытие
- Заменено 3 ручных правила на полный `RULE-SET` из blackmatrix7 (30+ доменов). Голосовые каналы, CDN, стриминг — всё работает стабильно.

### 📱 WhatsApp & Instagram — Звонки
- Добавлены IP-диапазоны WhatsApp (CIDR), доменный RULE-SET Whatsapp и Meta IP для стабильных голосовых и видеозвонков через прокси.

### 🇷🇺 Russia Stack 2026
- Интеграция **roscomvpn** (RCVPN-SR): geoblock-ru, GitHub, Gemini/DeepMind.
- **runetfreedom** / **Master-Yoba**: antifilter-community, Telegram IP.
- **misha antifilter** + RU TLD/ASN (`.ru`, `.рф`, Yandex AS).
- **Apple Push** через PROXY для стабильных push-уведомлений.

### 🏦 Банковские приложения
- Встроенный список российских банковских доменов (Сбер, ВТБ, Тинькофф и др.) идёт напрямую (`DIRECT`), чтобы банковские приложения не блокировали вход при включённом VPN.

### ⚡ DNS-over-QUIC / DoH / DoT
- Использование защищённых и быстрых протоколов DNS. Минимальная задержка при резолве имён даже на нестабильном 4G/5G.

### 🎮 Мастер Гейминга (Steam/Epic)
- **Умное разделение**: Игровой трафик и загрузки идут напрямую (`DIRECT`) для нулевого пинга, а чаты и заблокированные порталы — через прокси.

### 🚀 Технологический стек
- **[Host] Mapping**: Высокоскоростной маппинг доменов для мгновенного доступа.
- **[URL Rewrite]**: Автоматические редиректы с заблокированных локальных версий сайтов на глобальные.
- **Proxy Groups**: Правила привязаны к группам YouTube-Group, Gaming-Group и AUTO. Группы AI-Group и YouTube-Group сохранены в конфигурации, но по умолчанию трафик ИИ и YouTube направлен в AUTO для бесшовной работы без переименования прокси-серверов.

## Базовые возможности

### 🛡️ Блокировка и защита
- **AdBlock**: Полное вырезание рекламы, баннеров и аналитики (Rule-Sets от blackmatrix7).
- **Security First**: DoH/DoT/QUIC шифрование всех DNS-запросов.

### 🌎 Сервисы и Соцсети
- **YouTube & Streaming**: Полная разблокировка без троттлинга.
- **Telegram**: Полный rule-set + IP CIDR для надёжного обхода блокировок.
- **AI Tools**: Приоритетный доступ к OpenAI (ChatGPT), Claude, DeepL.
- **Apple & VK**: Прямой доступ к сервисам Apple, VK Video и мессенджеру MAX.

## Структура репозитория

```
/iOS/ios_ultra.conf     — ULTRA для iPhone/iPad
/MacOS/macos_ultra.conf — ULTRA для macOS
```

## Как установить

1. Скопируйте ссылку на RAW-файл нужного конфига.
2. В Shadowrocket: **Config** → **«+»** → **Download from URL**.
3. Вставьте ссылку (например: `https://raw.githubusercontent.com/iwizard7/Shadowrocket_confs/main/iOS/ios_ultra.conf`).
4. Установите **Global Routing** в режим **Config**.
5. (Опционально) Для URL Rewrite — установите и включите CA-сертификат в разделе **HTTPS Decryption**.

## Changelog

| Дата | Изменения |
|---|---|
| 2026-06-10 | ✅ Fix: Трафик YouTube и Spotify перенаправлен в AUTO во избежание DIRECT-фоллбека при отсутствии YouTube-серверов в списке |
| 2026-06-09 | ✅ Fix: Трафик AI (OpenAI, Claude и др.) перенаправлен в AUTO во избежание DIRECT-фоллбека при отсутствии AI-серверов в списке |
| 2026-06-09 | ✅ Fix: Apple Push порядок, RU TLD в конец, Proxy Groups активны |
| 2026-06-09 | ✅ Dedup: GitHub/Telegram IP, объединён блок Apple |
| 2026-06-09 | ✅ iOS: udp-timeout, dns-exclude; macOS: mDNS в tun-routes |
| 2026-06-09 | ✅ Russia Stack: roscomvpn, runetfreedom, antifilter, geoblock-ru |
| 2026-06-09 | ✅ Apple Push PROXY, GitHub/DeepMind, win-spy REJECT, RU TLD/ASN |
| 2026-06-09 | ✅ useful_links расширен (12+ новых RU-репозиториев) |
| 2026-06-09 | ✅ iOS синхронизирован с macOS (iCloud, Telegram IPv6, Antigravity) |
| 2026-06-09 | ✅ YouTube supplement, Whatsapp domains, geo-detect RULE-SET |
| 2026-06-09 | ✅ useful_links + CI: itdoginfo/allow-domains, убраны мёртвые репо |
| 2026-05-04 | ✅ Telegram CIDR Fix (5.28.192.0/18) |
| 2026-05-04 | ✅ DNS-over-QUIC / DoH optimizations |
| 2026-05-04 | ✅ Repack.me / Eax.me rules added |
| 2026-04-18 | ✅ 2GIS Route DIRECT (maps/geo fix) |
| 2026-04-17 | ✅ Yandex Go DIRECT fix (ios + macos) |
| 2026-04-17 | ✅ Discord → полный RULE-SET (30+ доменов) |
| 2026-04-17 | ✅ WhatsApp CIDR + Meta IPs + Telegram IPs |
| 2026-04-17 | ✅ Банковские приложения РФ → DIRECT |
| 2026-04-09 | 🎉 Первый релиз ULTRA Edition |

---
*Проект поддерживается и обновляется с учетом новых методов фильтрации трафика в России.*
