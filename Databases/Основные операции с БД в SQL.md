## Создать запись
```sql
	INSERT INTO table_name (id, title, content) VALUES(2, 'Ivan', NULL);
-- Если поле в БД обязательное , то ставим NULL
```

## Прочитать
```sql
SELECT * FROM table_name;
-- Или для более быстрого запроса, определённые поля(столбцы)
SELECT id, title, content FROM table_name;
```

## Отредактировать
```sql
UPDATE table_name  SET title='Ivan', content='some content'  WHERE id=1 
```

## Удалить
```sql
DELETE FROM table_name WHERE id=1;
```


- во всех случаях вместо `id=1` можно использовать все стандартные операторы: `= != < >`
- если есть сложности с названием колонок их можно обернуть в магические кавычки     \` title\` 
- текстовое значение в ячейку всегда оборачивается только в одинарные кавычки 



#sql