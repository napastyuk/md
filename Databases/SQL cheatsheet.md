**`SELECT`** – указывает, какие колонки нужно выбрать

**`FROM`** – указывает, из какой таблицы брать данные

**`WHERE`** – задаёт условие фильтрации строк (выбирает только те, которые соответствуют условию)

Пример:
```sql
SELECT name, age  
FROM users  
WHERE age > 18;
```
Этот запрос выберет только имя (`name`) и возраст (`age`) пользователей (`users`), у которых возраст больше 18.

## Работа с базами

**Создание базы из bash**
```bash
createdb -T template0 cinema  
# без указания template тоже можно, по умолчанию возьмётся template1

# или если у текущего пользователя не хватате прав, создать через системного пользователя postgres
# при таком создании надо будет себе приписать права owner
sudo -u postgres createdb --owner=ilya cinema
```

**Подключение к базе**
```bash
psql -U ilya -d cinema  --пользователя можно не указывать. Тогда возьмётся текущий. Главное, чтобы он был завёден в postgres.  
```

**Отключение** и выход в bash командой `\q`

**CRUD команды**
```sql
CREATE DATABASE hexlet_db TEMPLATE template0;   -- тоже создание но уже через SQL 
 
SELECT datname FROM pg_database; -- чтение списока всех баз для PG

ALTER DATABASE hexlet_db RENAME TO new_hexlet_db;   -- редактирование имени
ALTER DATABASE hexlet_db OWNER TO new_owner;        -- редактирование владельца

DROP DATABASE hexlet_db;      --удаление

DROP SCHEMA public CASCADE;
CREATE SCHEMA public;         --очистка

ALTER DATABASE old_db_name RENAME TO new_db_name;  --переименование (только из под другого пользователя и без активных подключений к базе)
```

## Работа с таблицами
```sql
CREATE TABLE users ( first_name VARCHAR(50) );  -- создание

SELECT * FROM users;  -- чтение
-- Или для более быстрого запроса, определённые поля(столбцы)
SELECT name FROM users;  -- чтение

DROP TABLE users;   -- удаление
```
За редактирование отвечает  **`ALTER`** - изменения структуры таблицы в базе данных
```sql
ALTER TABLE users ADD COLUMN email VARCHAR(255);  -- добавление колонки
ALTER TABLE users DROP COLUMN email;              -- удаление колонки
ALTER TABLE users MODIFY COLUMN age INT;          -- измение типа данных колонки
ALTER TABLE users RENAME TO customers;            -- переименование колонки
```

## Работа с записями
```sql
INSERT INTO users (first_name) VALUES ('Lucienne');   -- создание
-- если поле в БД обязательное , то ставим NULL

SELECT * FROM users WHERE first_name = 'Ramiro';  -- чтение

UPDATE users SET first_name = 'Casimer' WHERE id = 1;  -- редактирование
-- во всех случаях вместо `id=1` можно использовать все стандартные операторы: `= != < >`

DELETE FROM users WHERE first_name = 'Casimer';   -- удаление

/*
пример
многосточного
комментария
*/

```


#sql #php/db