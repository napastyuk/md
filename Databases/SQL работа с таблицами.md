
Все примеры для Postgres
## Создание таблиц CREATE

`NOT NULL` - значение обязательно должно быть указано. Даже после удаления или обновления 
`UNIQUE` - значение должно быть уникальным
`PRIMARY KEY` - объявляет этот столбец в качестве первичного ключа, что означает,  что его значения должны быть уникальными и не могут быть `NULL`
`GENERATED ALWAYS AS IDENTITY` - значения для этого столбца будут автоматически генерироваться при вставке новых строк и его нельзя задать вручную
если указать `GENERATED BY DEFAULT AS IDENTITY` то можно явно указывать значения, но если они не заданы, система все равно их сгенерирует

Ограничения можно использовать в любой комбинации
Пример:
```sql
CREATE TABLE users (
  id bigint PRIMARY KEY GENERATED BY DEFAULT AS IDENTITY,
  username VARCHAR(50) UNIQUE NOT NULL,
  birthday DATE,
  email_confirmed BOOLEAN,
  email VARCHAR(255) UNIQUE NOT NULL,
  gender VARCHAR(255) NOT NULL,
  password_digest VARCHAR(255) NOT NULL,
  first_name VARCHAR(50),
  last_name VARCHAR(50),
  created_at TIMESTAMP NOT NULL
);
```

## Изменение структуры ALTER

- добавить колонку в уже имеющуюся таблицу
```sql
ALTER TABLE users ADD COLUMN birthday DATE; -- в таблицу users добавить колонку с именем "birthday" и типом "date"
```

- переименование колонки
```sql
ALTER TABLE users RENAME COLUMN name TO first_name; -- в таблице "users" переименовать колонку "name" на "first_name"
```

- удаление колонки
```sql
ALTER TABLE users DROP COLUMN age;
```

- добавление и снятие ограничений
```sql

ALTER TABLE users ALTER COLUMN name SET NOT NULL;            -- установка NOT NULL через SET

ALTER TABLE users ALTER COLUMN name DROP NOT NULL;           -- снятие NOT NULL через DROP

ALTER TABLE users ADD UNIQUE (name);                         -- установка UNIQUE с автоматически сгенерированным именем

ALTER TABLE users ADD CONSTRAINT unique_name UNIQUE (name);  -- установка UNIQUE через ADD CONSTRAINT
ALTER TABLE users DROP CONSTRAINT unique_name;               -- снятие UNIQUE через DROP CONSTRAINT

```


#sql #php/db