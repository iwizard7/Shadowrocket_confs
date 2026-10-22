# AGENTS.md

Репозиторий конфигов Shadowrocket для России («ULTRA Edition»). Нет сборки, тестов и линтеров — два конфига + README.

## Структура

- `iOS/ios_ultra.conf` — конфиг для iPhone/iPad
- `MacOS/macos_ultra.conf` — конфиг для macOS
- `README.md` — описание и таблица Changelog (на русском)
- `useful_links.txt` — локальная база знаний, **в .gitignore** (не коммитится, в upstream отсутствует)
- `.kilo/` — worktree другого инструмента, не трогать

## Правила изменения конфигов

1. **iOS и macOS держать синхронизированными.** Правила `[Rule]`, группы `[Proxy Group]` и общие секции должны совпадать; различия только платформенные (в macOS — корпоративные BCS VPN IP/домены и `dns-exclude` для `*.bcs.ru`, в iOS — Yandex Go/2GIS). При правке одного конфига проверять второй (см. Changelog: «iOS синхронизирован с macOS»).
2. **Порядок правил в `[Rule]` — first-match, критичен.** Нарушение порядка ломает поведение:
   - `push.apple.com` и др. Push-домены **до** `apple.com`/`DOMAIN-KEYWORD,apple` (иначе Push уходит в DIRECT);
   - RU TLD (`.ru`/`.рф`/`.su`) и `GEOIP,RU,DIRECT` — **в конце**, после всех прокси-RULE-SET (иначе RU-домены сервисов, попадающих под прокси, станут DIRECT);
   - `FINAL,...` — всегда последняя строка `[Rule]`;
   - AdBlock REJECT-списки — до остальных правил.
3. **Имя политики в правилах должно существовать в `[Proxy Group]`** (`AI-Group`, `YouTube-Group`, `Gaming-Group`, `AUTO`). В macOS-конфиге правила используют `GAMING-GROUP` (uppercase) при определении группы `Gaming-Group` — при синхронизации сверять оба варианта, не «исправлять» вслепую.
4. **`update-url` в `[General]` должен указывать на raw-URL самого файла** в ветке main:
   `https://raw.githubusercontent.com/iwizard7/Shadowrocket_confs/main/<путь к файлу>` — обновлять при переименовании/перемещении.
5. Правила зачеркивания: `REJECT` — реклама/шпион/P2P; `DIRECT` — банки РФ, RU TLD/GeoIP, Apple (кроме Push), Yandex/VK/2GIS/Yandex Go, гейминг-загрузки; `AUTO` — всё остальное заблокированное (AI, Telegram, YouTube, соцсети), потому что группы `AI-Group`/`YouTube-Group` завязаны на regex-имена прокси, которых может не быть у пользователя (см. Changelog 2026-06-09/10).

## CI

CI отключён (workflow мониторинга upstream удалён 2026-10-22). Файл `.last_check` остался от него — легаси, безвреден, можно не трогать.

## Проверка изменений

Тестов нет. Минимальная верификация после правок:
- каждый URL `RULE-SET` доступен: `grep -o 'https://[^,]*' <файл> | xargs -n1 curl -sIL -o /dev/null -w '%{http_code} %{url_effective}\n'`
- структура секций сохранена (порядок: `[General]`, `[Proxy Group]`, `[Host]`, `[Rule]`/`[URL Rewrite]`, `[MITM]`); конфиг валиден только в реальном Shadowrocket — глубокой проверки нет.
- после изменений добавить строку в таблицу Changelog в `README.md` (формат: дата, emoji, `Fix:`/`Feature:`/`Dedup:`, на русском).
