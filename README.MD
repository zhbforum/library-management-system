<a id="top"></a>

<div align="center">
  <h1>Library Management System</h1>
  <p><strong>Full-stack library management application with catalog search, admin workflows, loans, readers and payments.</strong></p>

  <p>
    <a href="#english">English</a>
    ·
    <a href="#ukrainian">Українська</a>
    ·
    <a href="#russian">Русский</a>
  </p>

  <p>
    <img src="https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=000000" alt="JavaScript" />
    <img src="https://img.shields.io/badge/React-18.3.1-61DAFB?style=for-the-badge&logo=react&logoColor=000000" alt="React" />
    <img src="https://img.shields.io/badge/React_Router-6.28.0-CA4245?style=for-the-badge&logo=reactrouter&logoColor=ffffff" alt="React Router" />
    <img src="https://img.shields.io/badge/Axios-1.7.7-5A29E4?style=for-the-badge&logo=axios&logoColor=ffffff" alt="Axios" />
    <img src="https://img.shields.io/badge/Node.js-20+-339933?style=for-the-badge&logo=nodedotjs&logoColor=ffffff" alt="Node.js" />
    <img src="https://img.shields.io/badge/Express-4.21.1-000000?style=for-the-badge&logo=express&logoColor=ffffff" alt="Express" />
    <img src="https://img.shields.io/badge/MySQL-8+-4479A1?style=for-the-badge&logo=mysql&logoColor=ffffff" alt="MySQL" />
    <img src="https://img.shields.io/badge/JWT-9.0.2-000000?style=for-the-badge&logo=jsonwebtokens&logoColor=ffffff" alt="JWT" />
    <img src="https://img.shields.io/badge/npm-CB3837?style=for-the-badge&logo=npm&logoColor=ffffff" alt="npm" />
  </p>
</div>

---

## <a id="english"></a>English

### Overview

Library Management System is a full-stack web application for operating a small library. It provides a public-facing catalog and a protected administrative area for managing books, authors, genres, readers, active loans, fines and payments.

The project is split into a React single-page application, an Express REST API and a MySQL database. The code follows a simple and readable architecture: frontend pages call backend routes, routes delegate work to controllers, and controllers execute SQL queries through a shared database connection.

### Core Features

- Browse books, authors and genres.
- Search books by title, author and advanced filters.
- Authenticate users with JWT.
- Protect admin pages by user role.
- Create, read, update and delete books, authors, genres, readers and payments.
- Manage book loans, active returns, fines and payment records.

### Tech Stack

| Layer | Technologies |
| --- | --- |
| Frontend | React 18, React Router DOM 6, Axios, jwt-decode |
| Backend | Node.js, Express 4, CORS, JSON Web Token |
| Database | MySQL, `mysql2` |
| Tooling | npm, react-scripts |

### Architecture

```text
Browser
  |
  | React SPA, React Router, Axios
  v
Express REST API
  |
  | Controllers, SQL queries, mysql2
  v
MySQL database
```

```text
frontend/
  public/                 Static frontend assets
  src/
    assets/               Images and UI assets
    components/           Shared UI components
    pages/                Route-level screens and edit forms
    App.js                Client-side routing
    ProtectedRoute.jsx    JWT role guard for admin pages

backend/
  config/db.js            MySQL connection
  controllers/            Request handlers and SQL logic
  routes/                 REST route definitions by entity
  server.js               Express app entry point

rep_photos/               README and repository images
```

### Domain Model

| Entity | Purpose |
| --- | --- |
| `books` | Book catalog, author and genre references, total and available copies |
| `authors` | Author profiles used by catalog entries |
| `genres` | Book categories for browsing and filtering |
| `readers` | Library readers with contact information |
| `loans` | Book loans, return status, return dates and fines |
| `payments` | Reader payments connected to loans |
| `users` | Login data and role used for access control |

### API Surface

Backend runs on `http://localhost:3000`.

| Route | Responsibility |
| --- | --- |
| `POST /auth/login` | Authenticate user and return JWT |
| `GET /books` | List books |
| `GET /books/:bookId` | Get a single book |
| `GET /books/search` | Search books by title and author |
| `GET /books/search-with-filters` | Advanced book search with filters |
| `POST /books` | Create a book |
| `PUT /books/:bookId` | Update a book |
| `DELETE /books/:bookId` | Delete a book |
| `/authors` | Author CRUD |
| `/genres` | Genre CRUD |
| `/readers` | Reader CRUD |
| `/loans` | Loan management |
| `/payments` | Payment CRUD |

### Local Setup

Prerequisites:

- Node.js and npm;
- MySQL Server;
- a MySQL database named `semestr_work` with the tables used by the controllers.

This repository does not include migrations or a SQL dump, so the database schema must be created separately before running the app.

Database connection settings are stored in `backend/config/db.js`:

```js
const db = mysql.createConnection({
  host: '127.127.126.26',
  port: 3306,
  user: 'root',
  password: '',
  database: 'semestr_work',
});
```

Update `host`, `user`, `password` and `database` for your local MySQL environment.

Install backend dependencies from the repository root:

```bash
npm install
```

Start the backend:

```bash
node backend/server.js
```

Install and run the frontend:

```bash
cd frontend
npm install
npm start
```

The backend uses port `3000`. If Create React App asks to start the frontend on another port, confirm it.

### Authentication

Login is handled by `POST /auth/login`. The backend reads the user from the `users` table, compares the password and returns a JWT containing the user role.

Example token payload:

```json
{
  "name": "admin",
  "role": "admin"
}
```

The frontend stores the token in `localStorage`. `ProtectedRoute.jsx` decodes it and allows access to admin pages only when the role matches `admin`.

### Engineering Notes

- Frontend API calls currently target `http://localhost:3000` directly.
- Backend dependencies are installed from the root `package.json`.
- The JWT secret is hardcoded as `your_secret_key`; it should be moved to environment variables for production.
- User passwords are compared as plain text; production code should use hashing.
- Backend controllers use direct SQL queries instead of an ORM.

[Back to top](#top)

---

## <a id="ukrainian"></a>Українська

### Огляд

Library Management System - це full-stack вебзастосунок для керування невеликою бібліотекою. Він містить публічний каталог і захищену адміністративну частину для роботи з книгами, авторами, жанрами, читачами, активними видачами, штрафами та платежами.

Проєкт поділений на React single-page application, Express REST API та MySQL-базу даних. Архітектура проста й прозора: frontend-сторінки викликають backend-маршрути, маршрути передають роботу контролерам, а контролери виконують SQL-запити через спільне підключення до бази.

### Основні можливості

- Перегляд книг, авторів і жанрів.
- Пошук книг за назвою, автором і розширеними фільтрами.
- Авторизація користувачів через JWT.
- Захист адміністративних сторінок за роллю користувача.
- CRUD-операції для книг, авторів, жанрів, читачів і платежів.
- Керування видачами книг, поверненнями, штрафами та платіжними записами.

### Технологічний стек

| Рівень | Технології |
| --- | --- |
| Frontend | React 18, React Router DOM 6, Axios, jwt-decode |
| Backend | Node.js, Express 4, CORS, JSON Web Token |
| Database | MySQL, `mysql2` |
| Tooling | npm, react-scripts |

### Архітектура

```text
Browser
  |
  | React SPA, React Router, Axios
  v
Express REST API
  |
  | Controllers, SQL queries, mysql2
  v
MySQL database
```

```text
frontend/
  public/                 Статичні frontend-ресурси
  src/
    assets/               Зображення та UI-ресурси
    components/           Спільні компоненти інтерфейсу
    pages/                Сторінки маршрутів і форми редагування
    App.js                Клієнтська маршрутизація
    ProtectedRoute.jsx    JWT-перевірка ролі для admin-сторінок

backend/
  config/db.js            Підключення до MySQL
  controllers/            Обробники запитів і SQL-логіка
  routes/                 REST-маршрути за сутностями
  server.js               Точка входу Express-застосунку

rep_photos/               Зображення для README та репозиторію
```

### Доменна модель

| Сутність | Призначення |
| --- | --- |
| `books` | Каталог книг, посилання на автора й жанр, загальна та доступна кількість примірників |
| `authors` | Профілі авторів, які використовуються в каталозі |
| `genres` | Категорії книг для перегляду та фільтрації |
| `readers` | Читачі бібліотеки з контактною інформацією |
| `loans` | Видачі книг, статус повернення, дати повернення та штрафи |
| `payments` | Платежі читачів, пов'язані з видачами |
| `users` | Дані входу та роль для контролю доступу |

### API

Backend працює на `http://localhost:3000`.

| Маршрут | Призначення |
| --- | --- |
| `POST /auth/login` | Авторизація користувача та повернення JWT |
| `GET /books` | Список книг |
| `GET /books/:bookId` | Отримання однієї книги |
| `GET /books/search` | Пошук книг за назвою та автором |
| `GET /books/search-with-filters` | Розширений пошук книг із фільтрами |
| `POST /books` | Створення книги |
| `PUT /books/:bookId` | Оновлення книги |
| `DELETE /books/:bookId` | Видалення книги |
| `/authors` | CRUD для авторів |
| `/genres` | CRUD для жанрів |
| `/readers` | CRUD для читачів |
| `/loans` | Керування видачами |
| `/payments` | CRUD для платежів |

### Локальний запуск

Передумови:

- Node.js і npm;
- MySQL Server;
- MySQL-база даних `semestr_work` з таблицями, які використовують контролери.

У репозиторії немає міграцій або SQL-дампа, тому схему бази потрібно створити окремо перед запуском застосунку.

Налаштування підключення до бази знаходяться в `backend/config/db.js`:

```js
const db = mysql.createConnection({
  host: '127.127.126.26',
  port: 3306,
  user: 'root',
  password: '',
  database: 'semestr_work',
});
```

Оновіть `host`, `user`, `password` і `database` відповідно до локального MySQL-середовища.

Встановіть backend-залежності з кореня репозиторію:

```bash
npm install
```

Запустіть backend:

```bash
node backend/server.js
```

Встановіть і запустіть frontend:

```bash
cd frontend
npm install
npm start
```

Backend використовує порт `3000`. Якщо Create React App запропонує запустити frontend на іншому порту, підтвердьте це.

### Автентифікація

Вхід виконується через `POST /auth/login`. Backend читає користувача з таблиці `users`, порівнює пароль і повертає JWT з роллю користувача.

Приклад payload токена:

```json
{
  "name": "admin",
  "role": "admin"
}
```

Frontend зберігає токен у `localStorage`. `ProtectedRoute.jsx` декодує його й відкриває admin-сторінки лише тоді, коли роль відповідає `admin`.

### Інженерні примітки

- Frontend API-виклики зараз напряму використовують `http://localhost:3000`.
- Backend-залежності встановлюються з кореневого `package.json`.
- JWT secret захардкожений як `your_secret_key`; для production його потрібно винести в змінні середовища.
- Паролі користувачів порівнюються як звичайний текст; production-код має використовувати хешування.
- Backend-контролери використовують прямі SQL-запити без ORM.

[До початку](#top)

---

## <a id="russian"></a>Русский

### Обзор

Library Management System - это full-stack веб-приложение для управления небольшой библиотекой. В нем есть публичный каталог и защищенная административная часть для работы с книгами, авторами, жанрами, читателями, активными выдачами, штрафами и платежами.

Проект разделен на React single-page application, Express REST API и MySQL-базу данных. Архитектура простая и читаемая: frontend-страницы вызывают backend-маршруты, маршруты передают работу контроллерам, а контроллеры выполняют SQL-запросы через общее подключение к базе.

### Основные возможности

- Просмотр книг, авторов и жанров.
- Поиск книг по названию, автору и расширенным фильтрам.
- Авторизация пользователей через JWT.
- Защита административных страниц по роли пользователя.
- CRUD-операции для книг, авторов, жанров, читателей и платежей.
- Управление выдачами книг, возвратами, штрафами и платежными записями.

### Технологический стек

| Слой | Технологии |
| --- | --- |
| Frontend | React 18, React Router DOM 6, Axios, jwt-decode |
| Backend | Node.js, Express 4, CORS, JSON Web Token |
| Database | MySQL, `mysql2` |
| Tooling | npm, react-scripts |

### Архитектура

```text
Browser
  |
  | React SPA, React Router, Axios
  v
Express REST API
  |
  | Controllers, SQL queries, mysql2
  v
MySQL database
```

```text
frontend/
  public/                 Статические frontend-ресурсы
  src/
    assets/               Изображения и UI-ресурсы
    components/           Общие компоненты интерфейса
    pages/                Страницы маршрутов и формы редактирования
    App.js                Клиентская маршрутизация
    ProtectedRoute.jsx    JWT-проверка роли для admin-страниц

backend/
  config/db.js            Подключение к MySQL
  controllers/            Обработчики запросов и SQL-логика
  routes/                 REST-маршруты по сущностям
  server.js               Точка входа Express-приложения

rep_photos/               Изображения для README и репозитория
```

### Доменная модель

| Сущность | Назначение |
| --- | --- |
| `books` | Каталог книг, ссылки на автора и жанр, общее и доступное количество экземпляров |
| `authors` | Профили авторов, используемые в каталоге |
| `genres` | Категории книг для просмотра и фильтрации |
| `readers` | Читатели библиотеки с контактной информацией |
| `loans` | Выдачи книг, статус возврата, даты возврата и штрафы |
| `payments` | Платежи читателей, связанные с выдачами |
| `users` | Данные входа и роль для контроля доступа |

### API

Backend работает на `http://localhost:3000`.

| Маршрут | Назначение |
| --- | --- |
| `POST /auth/login` | Авторизация пользователя и возврат JWT |
| `GET /books` | Список книг |
| `GET /books/:bookId` | Получение одной книги |
| `GET /books/search` | Поиск книг по названию и автору |
| `GET /books/search-with-filters` | Расширенный поиск книг с фильтрами |
| `POST /books` | Создание книги |
| `PUT /books/:bookId` | Обновление книги |
| `DELETE /books/:bookId` | Удаление книги |
| `/authors` | CRUD для авторов |
| `/genres` | CRUD для жанров |
| `/readers` | CRUD для читателей |
| `/loans` | Управление выдачами |
| `/payments` | CRUD для платежей |

### Локальный запуск

Требования:

- Node.js и npm;
- MySQL Server;
- MySQL-база данных `semestr_work` с таблицами, которые используют контроллеры.

В репозитории нет миграций или SQL-дампа, поэтому схему базы нужно создать отдельно перед запуском приложения.

Настройки подключения к базе находятся в `backend/config/db.js`:

```js
const db = mysql.createConnection({
  host: '127.127.126.26',
  port: 3306,
  user: 'root',
  password: '',
  database: 'semestr_work',
});
```

Обновите `host`, `user`, `password` и `database` под локальное MySQL-окружение.

Установите backend-зависимости из корня репозитория:

```bash
npm install
```

Запустите backend:

```bash
node backend/server.js
```

Установите и запустите frontend:

```bash
cd frontend
npm install
npm start
```

Backend использует порт `3000`. Если Create React App предложит запустить frontend на другом порту, подтвердите это.

### Аутентификация

Вход выполняется через `POST /auth/login`. Backend читает пользователя из таблицы `users`, сравнивает пароль и возвращает JWT с ролью пользователя.

Пример payload токена:

```json
{
  "name": "admin",
  "role": "admin"
}
```

Frontend сохраняет токен в `localStorage`. `ProtectedRoute.jsx` декодирует его и открывает admin-страницы только тогда, когда роль соответствует `admin`.

### Инженерные примечания

- Frontend API-вызовы сейчас напрямую используют `http://localhost:3000`.
- Backend-зависимости устанавливаются из корневого `package.json`.
- JWT secret захардкожен как `your_secret_key`; для production его нужно вынести в переменные окружения.
- Пароли пользователей сравниваются как обычный текст; production-код должен использовать хеширование.
- Backend-контроллеры используют прямые SQL-запросы без ORM.

[К началу](#top)
