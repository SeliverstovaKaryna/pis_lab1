змінили структуру проекту з майстру 1234    
# Структура майбутнього проєкту (`Python` + `PostgreSQL`)

## Дерево директорій (цільова структура)

```text
src/
  app/
    __init__.py
    main.py                  # ASGI entrypoint (HTTP API)

    api/
      __init__.py
      deps.py                # DI-залежності (db session, current user)
      v1/
        __init__.py
        router.py            # збірка роутерів v1
        endpoints/
          __init__.py
          auth.py            # реєстрація/вхід/refresh/logout
          workouts.py        # CRUD спортивних справ + фільтри/сума
          health.py          # healthcheck/readiness

    core/
      __init__.py
      config.py              # налаштування з env (DB URL, JWT, логування)
      logging.py
      security.py            # JWT, перевірки доступу, ролі/скоупи (за потреби)
      errors.py              # єдиний формат помилок API

    domain/
      __init__.py
      users/
        __init__.py
        entities.py          # User
        schemas.py           # DTO/валідація (Pydantic)
      workouts/
        __init__.py
        entities.py          # WorkoutEntry
        schemas.py           # DTO/валідація (назва, хвилини, дата, нотатки)

    application/
      __init__.py
      users/
        __init__.py
        use_cases.py         # реєстрація/автентифікація
      workouts/
        __init__.py
        use_cases.py         # додавання/вивід/редагування/видалення/сума

    infrastructure/
      __init__.py
      db/
        __init__.py
        postgres.py          # engine/session + транзакції
        models.py            # ORM-моделі/мапінги (PostgreSQL)
        repositories/
          __init__.py
          users.py           # доступ до таблиць користувачів
          workouts.py        # доступ до таблиць спортивних справ
      auth/
        __init__.py
        password_hash.py     # bcrypt (cost >= 10)
        tokens.py            # access/refresh токени

    utils/
      __init__.py
      time.py                # робота з датами/UTC/валідація "не в майбутньому"
```

## Відповідність вимогам зі `spec/`

- `app/api/v1/endpoints/auth.py` → `REQ-F-001`, `REQ-F-002`, `REQ-NF-001`
- `app/api/v1/endpoints/workouts.py` → `REQ-F-010..016`, `REQ-F-020..024`, `REQ-F-030..032`, `REQ-NF-002`, `REQ-NF-005`
- `app/application/*/use_cases.py` → бізнес-логіка та перевірки доступу/валідації (включно з редагуванням)
- `app/infrastructure/db/*` → PostgreSQL-персистентність + ізоляція даних користувача (`user_id`)

## Дані (PostgreSQL)

- `users`: `id`, `username/email`, `password_hash`, `created_at`, `updated_at`
- `workout_entries`: `id`, `user_id`, `exercise_name`, `duration_minutes`, `performed_date`, `notes`, `created_at`, `updated_at`
