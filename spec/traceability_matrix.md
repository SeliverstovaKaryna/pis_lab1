# Матриця простежуваності вимог

## Інформаційна система контролю спортивної активності людини

| Поле | Значення |
|---|---|
| Автор | user12345 |
| Дата оновлення | 2026-10-20 |
| Базова специфікація | `spec/srs.md` v1.1 |
| Декомпозиція тікетів | `docs/sdd-ticket-decomposition.md` |
| План і ризики | `docs/sdd-risk-and-human-plan.md` |
| Система тікетів | GitHub Issues |
| Статус | Planned — aligned with SDD GitHub Issues |

---

## 1. Функціональні вимоги

| ID вимоги | Короткий опис | Критерій прийняття | BDD-сценарій | GitHub Issue | Плановий тест | Код | Документація |
|---|---|---|---|---|---|---|---|
| REQ-F-001 | Реєстрація користувача | Planned | Planned | `SDD-FEAT-AUTH-001` | TEST-AUTH-REG-001 | `app/api/v1/endpoints/auth.py`, `app/application/users/use_cases.py` | `spec/srs.md` §7.1 |
| REQ-F-002 | Вхід зареєстрованого користувача | Planned | Planned | `SDD-FEAT-AUTH-001` | TEST-AUTH-LOGIN-001 | `app/api/v1/endpoints/auth.py`, `app/application/users/use_cases.py` | `spec/srs.md` §7.1 |
| REQ-F-003 | Заборона доступу неавторизованим користувачам | Planned | Planned | `SDD-FEAT-AUTH-001` | TEST-AUTH-GUARD-001 | `app/api/deps.py`, `app/core/security.py` | `spec/srs.md` §7.1 |
| REQ-F-004 | Ізоляція даних користувача | є (§9.1) | Planned | `SDD-FEAT-AUTH-001` | TEST-AUTHZ-OWNERSHIP-001 | `app/api/deps.py`, `app/infrastructure/db/repositories/activities.py` | `spec/srs.md` §7.1, §9.1 |
| REQ-F-005 | До входу доступні лише сторінки реєстрації та входу | Planned | Planned | `SDD-FEAT-AUTH-001` | TEST-AUTH-PUBLIC-PAGES-001 | `app/api/v1/router.py`, `app/api/v1/endpoints/auth.py` | `spec/srs.md` §7.1 |
| REQ-F-006 | Logout, password recovery, account deletion out of scope | Planned | - | `SDD-ADD-001` | TEST-SCOPE-AUTH-001 | N/A | `spec/srs.md` §2, `logs/sked-dialogue-2026-10-03.md` |
| REQ-F-010 | Додавання запису активності | Planned | є (§9.2) | `SDD-FEAT-ACTIVITY-001` | TEST-ACT-CREATE-001 | `app/api/v1/endpoints/activities.py`, `app/application/activities/use_cases.py` | `spec/srs.md` §7.2, §9.2 |
| REQ-F-011 | Запис активності містить вправу з Exercise Catalog | Planned | Planned | `SDD-FEAT-ACTIVITY-001` | TEST-ACT-EXERCISE-001 | `app/domain/activities/entities.py`, `app/infrastructure/db/models.py` | `spec/srs.md` §7.2, `docs/exercise-catalog.md` |
| REQ-F-012 | Запис активності містить Duration Minutes | Planned | Planned | `SDD-FEAT-ACTIVITY-001` | TEST-ACT-DURATION-REQUIRED-001 | `app/domain/activities/schemas.py` | `spec/srs.md` §7.2 |
| REQ-F-013 | Запис активності містить Performed Date | Planned | Planned | `SDD-FEAT-ACTIVITY-001` | TEST-ACT-DATE-REQUIRED-001 | `app/domain/activities/schemas.py`, `app/utils/time.py` | `spec/srs.md` §7.2 |
| REQ-F-014 | Заборона запису без вправи з довідника | є (§9.1) | є (§9.2) | `SDD-FEAT-ACTIVITY-001` | TEST-ACT-EXERCISE-INVALID-001 | `app/domain/activities/schemas.py` | `spec/srs.md` §7.2, §9.1, §9.2 |
| REQ-F-015 | Заборона тривалості поза діапазоном 1..1440 | є (§9.1) | Planned | `SDD-FEAT-ACTIVITY-001` | TEST-ACT-DURATION-RANGE-001 | `app/domain/activities/schemas.py` | `spec/srs.md` §7.2, §9.1 |
| REQ-F-016 | Заборона дати, що не є поточною за APP_TIMEZONE | є (§9.1) | Planned | `SDD-FEAT-ACTIVITY-001` | TEST-ACT-CURRENT-DATE-001 | `app/utils/time.py`, `app/domain/activities/schemas.py` | `spec/srs.md` §7.2, §9.1 |
| REQ-F-017 | Необов'язкові Notes до 1000 символів | Planned | Planned | `SDD-FEAT-ACTIVITY-001` | TEST-ACT-NOTES-001 | `app/domain/activities/schemas.py`, `app/infrastructure/db/models.py` | `spec/srs.md` §3, §7.2 |
| REQ-F-020 | Відображення всіх власних записів активності | Planned | є (§9.2) | `SDD-FEAT-HISTORY-001` | TEST-ACT-LIST-001 | `app/api/v1/endpoints/activities.py`, `app/infrastructure/db/repositories/activities.py` | `spec/srs.md` §7.3, §9.2 |
| REQ-F-021 | Відображення записів активності за періодом | Planned | Planned | `SDD-FEAT-HISTORY-001` | TEST-ACT-FILTER-DATE-RANGE-001 | `app/infrastructure/db/repositories/activities.py` | `spec/srs.md` §7.3 |
| REQ-F-022 | Пошук за входженням Exercise Name без урахування регістру | Planned | Planned | `SDD-FEAT-HISTORY-001` | TEST-ACT-FILTER-EXERCISE-001 | `app/infrastructure/db/repositories/activities.py` | `spec/srs.md` §7.3 |
| REQ-F-023 | Activity Summary за день/тиждень/місяць/рік | є (§9.1) | Planned | `SDD-FEAT-HISTORY-001` | TEST-SUM-PERIODS-001 | `app/application/activities/use_cases.py` | `spec/srs.md` §7.3, §9.1 |
| REQ-F-024 | Структура відображення Activity Entry | Planned | є (§9.2) | `SDD-FEAT-HISTORY-001` | TEST-ACT-LIST-SHAPE-001 | `app/domain/activities/schemas.py` | `spec/srs.md` §7.3, §9.2 |
| REQ-F-025 | Одночасна фільтрація за вправою та датою/діапазоном дат | Planned | Planned | `SDD-FEAT-HISTORY-001` | TEST-SUM-COMBINED-FILTERS-001 | `app/infrastructure/db/repositories/activities.py` | `spec/srs.md` §7.3 |
| REQ-F-026 | Activity Summary містить хвилини за вправами та загалом за день | є (§9.1) | Planned | `SDD-FEAT-HISTORY-001` | TEST-SUM-BY-EXERCISE-AND-DAY-001 | `app/application/activities/use_cases.py` | `spec/srs.md` §7.3, §9.1 |
| REQ-F-027 | Сортування списку записів активності | Planned | Planned | `SDD-FEAT-HISTORY-001` | TEST-ACT-LIST-SORT-001 | `app/infrastructure/db/repositories/activities.py` | `spec/srs.md` §7.3 |
| REQ-F-030 | Редагування власного запису активності | Planned | Planned | `SDD-FEAT-MAINTAIN-001` | TEST-ACT-EDIT-001 | `app/api/v1/endpoints/activities.py`, `app/application/activities/use_cases.py` | `spec/srs.md` §7.4 |
| REQ-F-031 | Видалення власного запису активності | Planned | Planned | `SDD-FEAT-MAINTAIN-001` | TEST-ACT-DELETE-001 | `app/api/v1/endpoints/activities.py`, `app/application/activities/use_cases.py` | `spec/srs.md` §7.4 |
| REQ-F-032 | Заборона редагування/видалення чужого запису | є (§9.1) | є (§9.2) | `SDD-FEAT-MAINTAIN-001` | TEST-AUTHZ-FORBIDDEN-001 | `app/api/v1/endpoints/activities.py`, `app/api/deps.py` | `spec/srs.md` §7.4, §9.1, §9.2 |
| REQ-F-033 | Редагування застосовує ті самі правила валідації, що створення | Planned | Planned | `SDD-FEAT-MAINTAIN-001` | TEST-ACT-EDIT-VALIDATION-001 | `app/application/activities/use_cases.py`, `app/domain/activities/schemas.py` | `spec/srs.md` §7.4 |
| REQ-F-034 | Остаточне видалення без підтвердження та відновлення | є (§9.1) | Planned | `SDD-FEAT-MAINTAIN-001` | TEST-ACT-DELETE-PERMANENT-001 | `app/application/activities/use_cases.py` | `spec/srs.md` §7.4, §9.1 |

---

## 2. Нефункціональні вимоги

| ID вимоги | Категорія | Короткий опис | Критерій прийняття | GitHub Issue | Плановий тест | Код | Документація |
|---|---|---|---|---|---|---|---|
| REQ-NF-001 | Безпека | Хешування паролів bcrypt cost >= 10 | Planned | `SDD-FEAT-AUTH-001` | TEST-SEC-PASSWORD-HASH-001 | `app/infrastructure/auth/password_hash.py` | `spec/srs.md` §8 |
| REQ-NF-002 | Безпека | HTTP 403 при доступі до чужого запису | є (§9.1) | `SDD-FEAT-MAINTAIN-001` | TEST-SEC-FORBIDDEN-001 | `app/api/v1/endpoints/activities.py`, `app/api/deps.py` | `spec/srs.md` §8, §9.1 |
| REQ-NF-003 | Продуктивність | Вимога відкладена | - | `SDD-ADD-001` | N/A | N/A | `spec/srs.md` §8, `logs/sked-dialogue-2026-10-03.md` |
| REQ-NF-004 | Продуктивність | Вимога відкладена | - | `SDD-ADD-001` | N/A | N/A | `spec/srs.md` §8, `logs/sked-dialogue-2026-10-03.md` |
| REQ-NF-005 | Цілісність даних | Кожен Activity Entry прив'язаний до User | Planned | `SDD-FEAT-ACTIVITY-001` | TEST-DATA-USER-LINK-001 | `app/infrastructure/db/models.py` | `spec/srs.md` §8 |
| REQ-NF-006 | Конфігурація | Поточна дата визначається за `APP_TIMEZONE` | Planned | `SDD-FEAT-ACTIVITY-001` | TEST-CONF-TIMEZONE-001 | `app/core/config.py`, `app/utils/time.py` | `spec/srs.md` §8 |
| REQ-NF-007 | Інтерфейс | Підтримується ПК-версія веб-інтерфейсу | Planned | `SDD-FEAT-HISTORY-001` | TEST-UI-DESKTOP-001 | `app/api/v1/endpoints/*`, frontend layer planned | `spec/srs.md` §5, §8 |
| REQ-NF-008 | Локалізація | UI, Exercise names and user messages are in English | Planned | `SDD-FEAT-HISTORY-001` | TEST-UI-ENGLISH-001 | `app/api/v1/endpoints/*`, frontend layer planned | `spec/srs.md` §5, §8, `docs/exercise-catalog.md` |

---

## 3. SDD-циклові тікети

| GitHub Issue | Тип | Роль у простежуваності |
|---|---|---|
| `SDD-SPEC-001` | Specification | Фіксує затверджену SRS, межі системи, глосарій і правила ID вимог. |
| `SDD-ADD-001` | Addendum | Фіксує out-of-scope та відкладені вимоги без розширення поточного обсягу. |
| `SDD-TEST-001` | Test | Покриває вимоги, що плануються до реалізації, через TDD/BDD тести. |
| `SDD-VER-001` | Verification | Перевіряє відповідність реалізації, тестів і документації ID вимог. |
| `SDD-VAL-001` | Validation | Підтримує приймальну перевірку; фінальна валідація задуму залишається за людиною. |
| `SDD-DOC-001` | Documentation | Оновлює супровідну документацію і матрицю простежуваності. |
| `SDD-GATE-001` | Gate | Підтримує контрольну точку; Gate-рішення залишається за людиною. |

---

## 4. Артефакти простежуваності

| Артефакт | Призначення |
|---|---|
| `spec/srs.md` | Основна специфікація вимог |
| `spec/concept.md` | Концепція системи |
| `docs/sdd-ticket-decomposition.md` | Декомпозиція SRS у GitHub Issues, відповідальність і поетапний план |
| `docs/sdd-risk-and-human-plan.md` | Оцінка людських дій, реєстр ризиків і Gate-перевірки для вимог з вищою ціною відмови |
| `docs/exercise-catalog.md` | Початковий фіксований Exercise Catalog |
| `src/src.md` | Планована структура коду і бази даних |
| `logs/sked-dialogue-2026-10-03.md` | Журнал уточнення вимог |
| `logs/glossary-alignment-2026-10-03.md` | Журнал вирівнювання термінів |
| `logs/spec-control-review-2026-10-03.md` | Контрольна перевірка, що виявила потребу оновити матрицю |
