# Evidence — подтверждённые цифры и факты

Пути указаны относительно исходного (приватного) репозитория GiftQuest, ветка `test-launch`, HEAD `4dde6e7`.
Метки: **[факт]** — зафиксировано в документе/коде/команде; **[предположение]** — вывод автора отчёта без прямого
доказательства.

| # | Утверждение | Метка | Источник |
|---|---|---|---|
| 1 | `vitest run`: 1392 passed, 2 failed, 3 skipped, 117 файлов (2026-10-11) | факт | `STATUS_REPORT.md` §1 п.3, §2.3 |
| 2 | Два падения — `EPERM`/таймаут на Windows во временных каталогах, не логика продукта | предположение | `STATUS_REPORT.md` §2.3 |
| 3 | `tsc --noEmit -p tsconfig.json` — exit 0 | факт | `STATUS_REPORT.md` §2.3 |
| 4 | `biome check .`: 426 errors, 8 warnings, показанные — format | предположение | `STATUS_REPORT.md` §2.3 |
| 5 | 226 коммитов в `test-launch`; первый 2026-08-25; HEAD `4dde6e7` от 2026-09-24 | факт | `git rev-list --count HEAD`; `git log --reverse`; `STATUS_REPORT.md` §2.4 |
| 6 | 27 миграций БД (`0000`..`0026`) | факт | `ls packages/db/migrations` |
| 7 | ≈35 серверных модулей в `apps/server/src` | факт | `STATUS_REPORT.md` §2.1 |
| 8 | `giftquest.top` отвечает 200; `giftquest.service` active с 2026-10-03; релиз `60494e0` | факт | `STATUS_REPORT.md` §1 п.1, §2.7 |
| 9 | Код `apps/`+`packages/` на проде идентичен локальному HEAD | факт | `STATUS_REPORT.md` §1 п.1 |
| 10 | `REAL_GIFT_REDEMPTION=true` → сервер не стартует | факт | `apps/server/src/config.ts:258-267` |
| 11 | Реальный платёж 1 XTR сверён; дата документа 2026-09-06; на проде не перепроверялся | факт (по документу) | `docs/LAUNCH_AUDIT_CURRENT.md`; `STATUS_REPORT.md` §2.2 |
| 12 | Денежный журнал `money_entries` защищён триггерами от UPDATE/DELETE | факт | `packages/db/migrations/0017_narrow_masque.sql` |
| 13 | Уникальные индексы идемпотентности денег (`money_entry_operation`, `money_request_idempotency`, `money_request_telegram_charge`, `telegram_star_payments_charge_unique`) | факт | `packages/db/src/schema/commercial.ts:81,120,121`; `schema/index.ts:1365` |
| 14 | `ledger_transactions` — «immutable» по документу, ограничено частичными уникальными индексами (по одному debit/refund на redemption). Отдельных триггеров на таблицу баллов в миграциях не найдено | факт/уточнение | `docs/GIFT_REDEMPTION_MODEL.md`; `schema/index.ts:881-899`; grep `TRIGGER` в `packages/db/migrations` (только 0017) |
| 15 | Бэкап-таймер активен, последний запуск 2026-10-11 03:25 | факт | `STATUS_REPORT.md` §2.2 |
| 16 | Lead Hunter: таймер `gq-leads.timer`, запуск 2026-10-11 02:53, 274 лида | факт | `STATUS_REPORT.md` §2.2 |
| 17 | Тесты Stars: отказ при недоплате, переплате, неверной валюте, чужом плательщике, неизвестной заявке | факт (по документу, 2026-09-06) | `docs/LAUNCH_AUDIT_CURRENT.md` |
| 18 | Quality Score: база 50, диапазон 0–100, только просмотр админом | факт | `docs/QUALITY_AND_RISK.md` |
| 19 | Окно атрибуции 72 ч по умолчанию; хранение секретов кампаний — SHA-256 хэши; ротация с grace 24 ч | факт | `docs/ADVERTISER_INTEGRATION.md` |
| 20 | Удержание партнёрского вознаграждения 14 суток | факт | `docs/COMMERCIAL_MVP.md` |

Все цифры 1–4, 7–9, 15–16 — состояние на 2026-10-11 (аудит `STATUS_REPORT.md`, режим read-only). Цифры 11, 17 — на
2026-09-06.
