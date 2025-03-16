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

**`ALTER`** - изменения структуры таблицы в базе данных
```sql
ALTER TABLE users ADD COLUMN email VARCHAR(255);  -- добавление колонки
ALTER TABLE users DROP COLUMN email;              -- удаление колонки
ALTER TABLE users MODIFY COLUMN age INT;          -- измение типа данных колонки
ALTER TABLE users RENAME TO customers;            -- переименование колонки
```

#sql