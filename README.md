# taski-docker

Локальный запуск frontend и backend:

```bash
docker compose up --build -d
```

Приложение: http://localhost:8080. Nginx раздаёт React и передаёт запросы
`/api/` в backend. Миграции применяются перед запуском backend, данные SQLite
сохраняются в Docker volume `taski_data`.

Остановка:

```bash
docker compose down
```

При push в `main` GitHub Actions проверяет оба приложения, собирает и публикует
образы `<DOCKER_USERNAME>/taski_backend:latest` и
`<DOCKER_USERNAME>/taski_frontend:latest`.

В GitHub → Settings → Secrets and variables → Actions нужны два секрета:

- `DOCKER_USERNAME` — логин Docker Hub.
- `DOCKER_PASSWORD` — персональный токен этого аккаунта с правами Read & Write.

В Docker Hub создайте репозитории `taski_backend` и `taski_frontend` под этим
аккаунтом. Если Docker Hub отклоняет push с `insufficient_scope`, проверьте
права токена и владельца репозиториев. Изменение Dockerfile не выдаёт токену
права на публикацию.
