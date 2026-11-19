# TaskFlow

![Python](https://img.shields.io/badge/python-3.11%2B-blue.svg)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?logo=fastapi&logoColor=white)
![License](https://img.shields.io/badge/license-MIT-green.svg)

**TaskFlow** — учебный REST API менеджера задач. Пользователи создают проекты, ставят в них задачи с приоритетом и сроком, назначают исполнителей и обсуждают работу в комментариях. Доступ разграничен ролями `admin` и `user`.

## Стек

- Python 3.11+
- FastAPI (валидация через Pydantic, автодокументация OpenAPI)
- SQLAlchemy + SQLite
- JWT-аутентификация, хеширование паролей (bcrypt через passlib)
- pytest

## Установка и запуск

1. Клонируйте репозиторий и перейдите в папку проекта:

   ```bash
   git clone <адрес-репозитория> taskflow
   cd taskflow
   ```

2. Создайте и активируйте виртуальное окружение:

   ```bash
   python -m venv .venv
   source .venv/bin/activate        # Windows: .venv\Scripts\activate
   ```

3. Установите зависимости:

   ```bash
   pip install -r requirements.txt
   ```

4. Создайте файл настроек на основе примера и задайте секретный ключ:

   ```bash
   cp .env.example .env             # Windows: copy .env.example .env
   ```

   В `.env` указываются `SECRET_KEY`, `DATABASE_URL` и учётные данные администратора по умолчанию (`ADMIN_EMAIL`, `ADMIN_PASSWORD`).

5. Запустите приложение:

   ```bash
   uvicorn app.main:app --reload
   ```

   При первом запуске схема БД создаётся автоматически, а также создаётся администратор с данными из `.env`.

Приложение будет доступно по адресу <http://127.0.0.1:8000>, интерактивная документация (Swagger UI) — по адресу <http://127.0.0.1:8000/docs>.

### Запуск в Docker

```bash
docker build -t taskflow .
docker run -p 8000:8000 --env-file .env taskflow
```

### Тесты

```bash
pytest
```

## Структура проекта

```text
taskflow/
├── app/
│   ├── main.py          # точка входа FastAPI
│   ├── core/            # настройки и подключение к БД
│   ├── models/          # модели таблиц SQLite
│   ├── schemas/         # схемы валидации запросов и ответов
│   └── api/             # маршруты: users, projects, tasks, comments
├── tests/               # тесты API
├── .env.example         # пример переменных окружения
├── API.md               # описание эндпоинтов
├── CHANGELOG.md         # история версий
└── README.md
```

## API

Все эндпоинты имеют префикс `/api/v1`. Подробное описание методов, тел запросов и примеров ответов — в файле [API.md](API.md).

## Лицензия

Проект распространяется на условиях лицензии MIT.
