# kilo_hello

1) Сервис по README и корню: учебный сервис **предварительной оценки заявки на заём под ПТС** (carmoney-lab, проект практикума М3): принимает заявку (VIN, год, пробег, оценочная стоимость, сумма, срок), считает LTV и возвращает решение `approve` / `review` / `reject`; все данные синтетические.
2) Запуск и проверка: `Makefile` — `make up` (поднять сервис и базу), `make down`, `make ps`, `make logs`, `make install` (composer install), `make test` (PHPUnit), `make lint` (`php -l` по `backend/` и `tests/`), `make seed` (перезалить `db/seed.sql`), `make help`; `docker-compose.yml` поднимает два сервиса — `backend` (`php -S 0.0.0.0:8080 -t backend/public backend/public/router.php`, порт `${APP_PORT:-8080}:8080`) и `db` (`mysql:8.0`, БД `carmoney_lab`, init-скрипты `db/schema.sql` и `db/seed.sql`, healthcheck через `mysqladmin ping`, порт `${DB_PORT:-3307}:3306`), с healthcheck `db` и `depends_on` у backend.
3) Решение `approve` / `review` / `reject` по заявке считается в `backend/src/Domain/` — `DecisionEngine.php` (правила) поверх `LtvCalculator.php`, `AssessmentService.php` собирает шаги оценки; пороги/лимиты — из `backend/config/rules.php`.

модель: MiniMax-M3
