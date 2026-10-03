# Матриця простежуваності вимог

## Інформаційна система контролю спортивної активності людини

| Поле | Значення |
|---|---|
| Автор | user12345 |
| Дата оновлення | 2026-10-03 |
| Базова специфікація | `spec/srs.md` v1.1 |
| Статус | Draft — aligned with SKED decisions |

---

## 1. Функціональні вимоги

| ID вимоги | Короткий опис | Критерій прийняття | BDD-сценарій | Тікет | Плановий тест | Код | Документація |
|---|---|---|---|---|---|---|---|
| REQ-F-001 | Реєстрація користувача | Planned | Planned | TICKET-AUTH-001 | TEST-AUTH-REG-001 | `app/api/v1/endpoints/auth.py`, `app/application/users/use_cases.py` | `spec/srs.md` §7.1 |
| REQ-F-002 | Вхід зареєстрованого користувача | Planned | Planned | TICKET-AUTH-002 | TEST-AUTH-LOGIN-001 | `app/api/v1/endpoints/auth.py`, `app/application/users/use_cases.py` | `spec/srs.md` §7.1 |
| REQ-F-003 | Заборона доступу неавторизованим користувачам | Planned | Planned | TICKET-AUTH-003 | TEST-AUTH-GUARD-001 | `app/api/deps.py`, `app/core/security.py` | `spec/srs.md` §7.1 |
| REQ-F-004 | Ізоляція даних користувача | є (§9.1) | Planned | TICKET-AUTHZ-001 | TEST-AUTHZ-OWNERSHIP-001 | `app/api/deps.py`, `app/infrastructure/db/repositories/activities.py` | `spec/srs.md` §7.1, §9.1 |
| REQ-F-005 | До входу доступні лише сторінки реєстрації та входу | Planned | Planned | TICKET-AUTH-004 | TEST-AUTH-PUBLIC-PAGES-001 | `app/api/v1/router.py`, `app/api/v1/endpoints/auth.py` | `spec/srs.md` §7.1 |
| REQ-F-006 | Logout, password recovery, account deletion out of scope | Planned | - | TICKET-SCOPE-001 | TEST-SCOPE-AUTH-001 | N/A | `spec/srs.md` §2, `logs/sked-dialogue-2026-10-03.md` |
| REQ-F-010 | Додавання запису активності | Planned | є (§9.2) | TICKET-ACT-001 | TEST-ACT-CREATE-001 | `app/api/v1/endpoints/activities.py`, `app/application/activities/use_cases.py` | `spec/srs.md` §7.2, §9.2 |
| REQ-F-011 | Запис активності містить вправу з Exercise Catalog | Planned | Planned | TICKET-ACT-002 | TEST-ACT-EXERCISE-001 | `app/domain/activities/entities.py`, `app/infrastructure/db/models.py` | `spec/srs.md` §7.2, `docs/exercise-catalog.md` |
| REQ-F-012 | Запис активності містить Duration Minutes | Planned | Planned | TICKET-ACT-003 | TEST-ACT-DURATION-REQUIRED-001 | `app/domain/activities/schemas.py` | `spec/srs.md` §7.2 |
| REQ-F-013 | Запис активності містить Performed Date | Planned | Planned | TICKET-ACT-004 | TEST-ACT-DATE-REQUIRED-001 | `app/domain/activities/schemas.py`, `app/utils/time.py` | `spec/srs.md` §7.2 |
| REQ-F-014 | Заборона запису без вправи з довідника | є (§9.1) | є (§9.2) | TICKET-ACT-005 | TEST-ACT-EXERCISE-INVALID-001 | `app/domain/activities/schemas.py` | `spec/srs.md` §7.2, §9.1, §9.2 |
| REQ-F-015 | Заборона тривалості поза діапазоном 1..1440 | є (§9.1) | Planned | TICKET-ACT-006 | TEST-ACT-DURATION-RANGE-001 | `app/domain/activities/schemas.py` | `spec/srs.md` §7.2, §9.1 |
| REQ-F-016 | Заборона дати, що не є поточною за APP_TIMEZONE | є (§9.1) | Planned | TICKET-ACT-007 | TEST-ACT-CURRENT-DATE-001 | `app/utils/time.py`, `app/domain/activities/schemas.py` | `spec/srs.md` §7.2, §9.1 |
| REQ-F-017 | Необов'язкові Notes до 1000 символів | Planned | Planned | TICKET-ACT-008 | TEST-ACT-NOTES-001 | `app/domain/activities/schemas.py`, `app/infrastructure/db/models.py` | `spec/srs.md` §3, §7.2 |
| REQ-F-020 | Відображення всіх власних записів активності | Planned | є (§9.2) | TICKET-ACT-009 | TEST-ACT-LIST-001 | `app/api/v1/endpoints/activities.py`, `app/infrastructure/db/repositories/activities.py` | `spec/srs.md` §7.3, §9.2 |
| REQ-F-021 | Відображення записів активності за періодом | Planned | Planned | TICKET-ACT-010 | TEST-ACT-FILTER-DATE-RANGE-001 | `app/infrastructure/db/repositories/activities.py` | `spec/srs.md` §7.3 |
| REQ-F-022 | Пошук за входженням Exercise Name без урахування регістру | Planned | Planned | TICKET-ACT-011 | TEST-ACT-FILTER-EXERCISE-001 | `app/infrastructure/db/repositories/activities.py` | `spec/srs.md` §7.3 |
| REQ-F-023 | Activity Summary за день/тиждень/місяць/рік | є (§9.1) | Planned | TICKET-SUM-001 | TEST-SUM-PERIODS-001 | `app/application/activities/use_cases.py` | `spec/srs.md` §7.3, §9.1 |
| REQ-F-024 | Структура відображення Activity Entry | Planned | є (§9.2) | TICKET-ACT-012 | TEST-ACT-LIST-SHAPE-001 | `app/domain/activities/schemas.py` | `spec/srs.md` §7.3, §9.2 |
| REQ-F-025 | Одночасна фільтрація за вправою та датою/діапазоном дат | Planned | Planned | TICKET-SUM-002 | TEST-SUM-COMBINED-FILTERS-001 | `app/infrastructure/db/repositories/activities.py` | `spec/srs.md` §7.3 |
| REQ-F-026 | Activity Summary містить хвилини за вправами та загалом за день | є (§9.1) | Planned | TICKET-SUM-003 | TEST-SUM-BY-EXERCISE-AND-DAY-001 | `app/application/activities/use_cases.py` | `spec/srs.md` §7.3, §9.1 |
| REQ-F-027 | Сортування списку записів активності | Planned | Planned | TICKET-ACT-013 | TEST-ACT-LIST-SORT-001 | `app/infrastructure/db/repositories/activities.py` | `spec/srs.md` §7.3 |
| REQ-F-030 | Редагування власного запису активності | Planned | Planned | TICKET-ACT-014 | TEST-ACT-EDIT-001 | `app/api/v1/endpoints/activities.py`, `app/application/activities/use_cases.py` | `spec/srs.md` §7.4 |
| REQ-F-031 | Видалення власного запису активності | Planned | Planned | TICKET-ACT-015 | TEST-ACT-DELETE-001 | `app/api/v1/endpoints/activities.py`, `app/application/activities/use_cases.py` | `spec/srs.md` §7.4 |
| REQ-F-032 | Заборона редагування/видалення чужого запису | є (§9.1) | є (§9.2) | TICKET-AUTHZ-002 | TEST-AUTHZ-FORBIDDEN-001 | `app/api/v1/endpoints/activities.py`, `app/api/deps.py` | `spec/srs.md` §7.4, §9.1, §9.2 |
| REQ-F-033 | Редагування застосовує ті самі правила валідації, що створення | Planned | Planned | TICKET-ACT-016 | TEST-ACT-EDIT-VALIDATION-001 | `app/application/activities/use_cases.py`, `app/domain/activities/schemas.py` | `spec/srs.md` §7.4 |
| REQ-F-034 | Остаточне видалення без підтвердження та відновлення | є (§9.1) | Planned | TICKET-ACT-017 | TEST-ACT-DELETE-PERMANENT-001 | `app/application/activities/use_cases.py` | `spec/srs.md` §7.4, §9.1 |

---

## 2. Нефункціональні вимоги

| ID вимоги | Категорія | Короткий опис | Критерій прийняття | Тікет | Плановий тест | Код | Документація |
|---|---|---|---|---|---|---|---|
| REQ-NF-001 | Безпека | Хешування паролів bcrypt cost >= 10 | Planned | TICKET-SEC-001 | TEST-SEC-PASSWORD-HASH-001 | `app/infrastructure/auth/password_hash.py` | `spec/srs.md` §8 |
| REQ-NF-002 | Безпека | HTTP 403 при доступі до чужого запису | є (§9.1) | TICKET-SEC-002 | TEST-SEC-FORBIDDEN-001 | `app/api/v1/endpoints/activities.py`, `app/api/deps.py` | `spec/srs.md` §8, §9.1 |
| REQ-NF-003 | Продуктивність | Вимога відкладена | - | TICKET-NFR-DEFER-001 | N/A | N/A | `spec/srs.md` §8, `logs/sked-dialogue-2026-10-03.md` |
| REQ-NF-004 | Продуктивність | Вимога відкладена | - | TICKET-NFR-DEFER-002 | N/A | N/A | `spec/srs.md` §8, `logs/sked-dialogue-2026-10-03.md` |
| REQ-NF-005 | Цілісність даних | Кожен Activity Entry прив'язаний до User | Planned | TICKET-DATA-001 | TEST-DATA-USER-LINK-001 | `app/infrastructure/db/models.py` | `spec/srs.md` §8 |
| REQ-NF-006 | Конфігурація | Поточна дата визначається за `APP_TIMEZONE` | Planned | TICKET-CONF-001 | TEST-CONF-TIMEZONE-001 | `app/core/config.py`, `app/utils/time.py` | `spec/srs.md` §8 |
| REQ-NF-007 | Інтерфейс | Підтримується ПК-версія веб-інтерфейсу | Planned | TICKET-UI-001 | TEST-UI-DESKTOP-001 | `app/api/v1/endpoints/*`, frontend layer planned | `spec/srs.md` §5, §8 |
| REQ-NF-008 | Локалізація | UI, Exercise names and user messages are in English | Planned | TICKET-UI-002 | TEST-UI-ENGLISH-001 | `app/api/v1/endpoints/*`, frontend layer planned | `spec/srs.md` §5, §8, `docs/exercise-catalog.md` |

---

## 3. Артефакти простежуваності

| Артефакт | Призначення |
|---|---|
| `spec/srs.md` | Основна специфікація вимог |
| `spec/concept.md` | Концепція системи |
| `docs/exercise-catalog.md` | Початковий фіксований Exercise Catalog |
| `src/src.md` | Планована структура коду і бази даних |
| `logs/sked-dialogue-2026-10-03.md` | Журнал уточнення вимог |
| `logs/glossary-alignment-2026-10-03.md` | Журнал вирівнювання термінів |
| `logs/spec-control-review-2026-10-03.md` | Контрольна перевірка, що виявила потребу оновити матрицю |
