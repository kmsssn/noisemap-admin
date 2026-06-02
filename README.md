# NoiseMap Admin Panel

Веб-панель администрирования для NoiseMap: управление пользователями, ролями,
модерация записей и комментариев на карте.

```
https://admin-noisemap.duckdns.org
```

API при этом остаётся на основном домене `https://noisemap.duckdns.org`.

---

## Что внутри

| Файл | Назначение |
|------|-----------|
| `index.html` | Сама панель. Адрес API зашит в константе `API_BASE` вверху `<script>`. |
| `Dockerfile` | Собирает nginx-образ со статикой. |
| `nginx/default.conf` | Конфиг nginx (отдаёт `index.html`). |
| `README.md` | Этот файл. |

Разделы панели и используемые эндпоинты (все уже существуют в бэкенде):

- **Дашборд** — `GET /api/v1/stats/city`, `GET /api/v1/moderation/stats`
- **Пользователи** — `GET/PUT /api/v1/admin/users/**` (только ADMIN)
- **Модерация** — `GET/PUT /api/v1/moderation/queue/**` (MODERATOR/ADMIN)
- **Комментарии** — `GET /api/v1/comments`, `DELETE /api/v1/comments/{id}` (soft delete)

Вход в панель разрешён только для ролей **ADMIN** и **MODERATOR** — проверяется
по claim `role` в JWT после логина.