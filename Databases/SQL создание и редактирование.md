## Добавление данных INSERT
Пример:
```sql
INSERT INTO users (
	username, 
	email, 
	first_name, 
	last_name, 
	birthday, 
	gender, 
	id, 
	created_at, 
	password_digest
)
VALUES (
	'AgentJ', 
	'wsmith09@gmail.com', 
	'Will', 
	'Smith', 
	'1968-09-25', 
	'male', 
	100, 
	'2023-05-01', 
	'11111'
	),
	(
	'MrBatman', 
	'benaff@gmail.com', 
	'Ben', 
	'Affleck', 
	'1973-08-15', 
	'male', 
	101, 
	'2023-05-01', 
	'22222'
);
```

## Редактирование UPDATE

```sql
UPDATE 
	users                          -- обновим таблицу users 
SET 
	first_name = 'Pierce',         -- в каких колонках , какие данные обновить  
	last_name = 'Brosnan' 
WHERE 
	email = 'agent007@yahoo.com';  -- к каким записям/строкам применить это обновление  
```
- `UPDATE` идемпотентен т е его можно применять несколько раз, если данные уже обновлены, ничего не произойдет
- `WHERE` очень важен. Если запрос выполнить без него, обновление применится ко всем строкам таблицы
- В `WHERE` можно 
	- использовать логические операции `<` `>` и др. 
	- объединять условия через `AND` `OR`  
	- группировать условия с помощью `(` `)` 

## Удаление DELETE
```sql
DELETE FROM                     -- оператор 
users                           -- имя таблицы из которой удаляем данные
WHERE username = 'secretagent'; -- условие фильтрации, какие именно записи удалить 
```
Условия аналогичны операции UPDATE

```sql
DELETE FROM users;   -- удаляет таблицу целиком

TRUNCATE users;      -- делает тоже самое но быстрее
```