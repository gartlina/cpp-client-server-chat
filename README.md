# C++ Клиент-Серверное Чат Приложение с Базой Данных PostgreSQL

Этот проект представляет собой клиент-серверное чат приложение, разработанное на C++ с использованием фреймворка Qt. Приложение позволяет пользователям регистрироваться, входить в систему, отправлять публичные и приватные сообщения, а также предоставляет административные функции для управления пользователями.

## Содержание

- [Функциональность](#функциональность)
- [Используемые технологии](#используемые-технологии)
- [Установка и запуск](#установка-и-запуск)
  - [Необходимые условия](#необходимые-условия)
  - [Настройка базы данных](#настройка-базы-данных)
  - [Сборка приложения](#сборка-приложения)
- [Использование](#использование)
  - [Интерфейс сервера](#интерфейс-сервера)
  - [Использование клиента](#использование-клиента)
- [SQL Скрипт для Создания Таблиц](#sql-скрипт-для-создания-таблиц)

## Функциональность

- **Регистрация и аутентификация пользователей**
- **Публичные сообщения**: Отправка сообщений всем пользователям в чате
- **Приватные сообщения**: Отправка сообщений конкретному пользователю
- **История сообщений**: Сохранение и загрузка истории сообщений из базы данных
- **Административный интерфейс**:
  - Просмотр всех зарегистрированных пользователей
  - Блокировка и разблокировка пользователей
  - Просмотр логов и истории чата

## Используемые технологии

- **C++**: Язык программирования
- **Qt Framework**: Для создания GUI и сетевого взаимодействия
- **PostgreSQL**: Для хранения данных пользователей и сообщений
- **SQL**: Для взаимодействия с базой данных

## Установка и запуск

### Необходимые условия

- **Qt Framework**: Рекомендуется версия Qt 5.15 или выше
- **PostgreSQL**: Установленная база данных PostgreSQL
- **C++ Компилятор**: Совместимый с Qt (например, GCC или MSVC)
- **Git**: Для клонирования репозитория

### Настройка базы данных

1. **Запустите сервер PostgreSQL**.
2. **Создайте новую базу данных** для чат приложения:

   ```sql
   CREATE DATABASE chat_app;

3. **Создайте необходимые таблицы**. Используйте SQL Скрипт ниже для создания таблиц users и messages.

### Сборка приложения

1. **Клонируйте репозиторий:**

```bash
git clone https://github.com/yourusername/yourrepository.git
```

2. **Перейдите в основную ветку:**

```bash
git checkout main
```

3. **Откройте проект**

4. **Настройте подключение к базе данных** в файле database.cpp:

```cpp
db = QSqlDatabase::addDatabase("QPSQL");
db.setHostName("localhost");
db.setDatabaseName("chat_app"); // имя вашей базы данных
db.setUserName("your_db_username"); // ваше имя пользователя БД
db.setPassword("your_db_password"); // ваш пароль БД
```

## Использование
### Интерфейс сервера:

1. Вкладка "Чаты": Просмотр публичных и приватных сообщений.
2. Вкладка "Пользователи": Список всех пользователей с возможностью бана/разбана.
3. Вкладка "Лог": Просмотр системных сообщений и действий.

### Использование клиента:
1. **Регистрация:** Создайте нового пользователя, следуя инструкциям в консоли.
2. **Вход в систему:** Войдите с существующими учетными данными.
3. **Отправка сообщений:**
- Публичное сообщение: Отправьте сообщение всем пользователям.
- Приватное сообщение: Отправьте сообщение конкретному пользователю по его ID.
- Получение сообщений: Все новые сообщения будут отображаться в консоли.

## SQL Скрипт для Создания Таблиц
**Используйте следующий скрипт для создания необходимых таблиц в базе данных PostgreSQL:**
   ```sql
   -- Создание таблицы пользователей
    CREATE TABLE users (
        id SERIAL PRIMARY KEY,
        login VARCHAR(255) UNIQUE NOT NULL,
        password VARCHAR(255) NOT NULL,
        name VARCHAR(255) NOT NULL,
        is_banned BOOLEAN DEFAULT FALSE
    );

    -- Создание таблицы сообщений
    CREATE TABLE messages (
        id SERIAL PRIMARY KEY,
        sender_id INTEGER REFERENCES users(id),
        receiver_id INTEGER REFERENCES users(id),
        content TEXT NOT NULL,
        timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
        is_read BOOLEAN DEFAULT FALSE
    );
