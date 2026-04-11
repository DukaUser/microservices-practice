# Microservices Practice
Описание проекта

Данный проект демонстрирует реализацию микросервисной архитектуры с использованием технологий Docker, Docker Compose, Docker Swarm и NGINX.

Приложение состоит из двух независимых микросервисов:
user-service — сервис для работы с пользователями
order-service — сервис для работы с заказами

Сервисы взаимодействуют друг с другом по HTTP и обмениваются данными в формате JSON.

**Архитектура**
Система построена по принципу микросервисной архитектуры:
Клиент → NGINX → order-service → user-service
NGINX выступает в роли reverse proxy
order-service обращается к user-service для получения данных о пользователе
взаимодействие происходит через внутреннюю сеть Docker

**Используемые технологии**
Python (Flask)
Docker
Docker Compose
Docker Swarm
NGINX

**Структура проекта**
microservices-practice/
│
├── user-service/
│   ├── app.py
│   ├── Dockerfile
│   ├── requirements.txt
│   └── users.json
│
├── order-service/
│   ├── app.py
│   ├── Dockerfile
│   ├── requirements.txt
│   └── orders.json
│
├── nginx/
│   ├── Dockerfile
│   └── nginx.conf
│
├── docker-compose.yml
└── docker-stack.yml

**Для запуска с использованием Docker Compose:**

docker compose up --build

**После запуска сервисы будут доступны:**
http://localhost:3001/users
http://localhost:3002/orders
http://localhost:3002/orders/1

**Запуск проекта**
1. Инициализация Docker Swarm
docker swarm init
2. Сборка образа NGINX
docker build -t my-nginx ./nginx
3. Запуск стека
docker stack deploy -c docker-stack.yml myapp
4. Проверка работы

**Открыть в браузере:**
http://localhost/users
http://localhost/orders
http://localhost/orders/1
Взаимодействие сервисов

**При обращении к**:
/orders/1

**происходит следующий процесс:**

Запрос поступает в NGINX
NGINX перенаправляет его в order-service
order-service обращается к user-service
Формируется объединённый JSON-ответ

**Пример ответа:**

{
  "order": {
    "id": 1,
    "item": "Laptop",
    "user_id": 1,
    "amount": 1
  },
  "user": {
    "id": 1,
    "name": "Alice",
    "email": "alice@example.com"
  }
}

**Особенности реализации**
Используется Docker Swarm для оркестрации контейнеров
Настроена overlay сеть для взаимодействия сервисов
Реализован NGINX reverse proxy для маршрутизации запросов
Сервисы взаимодействуют по имени (service discovery)

**Цель работы**
Изучить основы микросервисной архитектуры
Научиться контейнеризировать приложения с помощью Docker
Освоить оркестрацию сервисов через Docker Compose и Docker Swarm
Реализовать маршрутизацию запросов с помощью NGINX

**Вывод**
В ходе выполнения работы была реализована микросервисная архитектура с использованием современных инструментов контейнеризации и оркестрации. Получен практический опыт развертывания сервисов, настройки сетевого взаимодействия и маршрутизации запросов.
