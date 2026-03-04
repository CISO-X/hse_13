
# Mock Antivirus API (Homework 13)

Небольшой учебный проект, реализующий **mock API антивирусного сервиса** и клиента для взаимодействия с ним.

Проект демонстрирует работу с:

- HTTP API
- Python `http.server`
- REST-запросами
- библиотекой `requests`
- запуском сервера в фоне

---

# Структура проекта

```

.
├── mock_av_server.py   # HTTP сервер (mock antivirus API)
├── av_client.py        # клиент для взаимодействия с API
└── README.md

```

---

# API Endpoints

## Health check

```

GET /api/v1/health

````

Проверяет работоспособность сервера.

Ответ:

```json
{
  "status": "ok"
}
````

---

## Scan file

```
POST /api/v1/scan
```

Заголовок запроса:

```
X-API-Key: demo-key
```

Тело запроса:

```json
{
  "filename": "sample.bin",
  "sha256": "hash_value"
}
```

Ответ:

```json
{
  "verdict": "clean",
  "filename": "sample.bin",
  "sha256": "hash_value"
}
```

Правило проверки:

* если `sha256` заканчивается на `bad` → `malicious`
* иначе → `clean`

---

# Установка

Требуется **Python 3.9+**

Установить зависимости:

```
pip install requests
```

---

# Запуск сервера

```
python mock_av_server.py
```

Сервер запускается на:

```
http://127.0.0.1:8000
```

---

# Запуск сервера в фоне (Linux / Colab)

```
nohup python mock_av_server.py > server.log 2>&1 &
```

Проверить лог:

```
tail server.log
```

---

# Запуск клиента

```
python av_client.py
```

Клиент выполняет:

1. проверку `/health`
2. создание тестового файла
3. вычисление SHA256
4. отправку запроса `/scan`

Пример вывода:

```
HEALTH: 200 {'status': 'ok'}
SCAN: 200 {'verdict': 'clean', 'filename': 'sample.bin'}
```

---

# Используемые технологии

* Python
* HTTP API
* REST
* requests
* http.server

---

# Назначение проекта

Проект создан в рамках **домашнего задания по курсу информационной безопасности** и демонстрирует базовую архитектуру взаимодействия клиента и антивирусного API.

