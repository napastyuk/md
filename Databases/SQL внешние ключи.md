Короткий синтаксис

```sql
attribute_type_id INT NOT NULL REFERENCES attribute_types(id)
```

Полная запись
```sql
attribute_type_id INT NOT NULL,
FOREIGN KEY (attribute_type_id) REFERENCES attribute_types(id)
	ON DELETE SET NULL
    ON UPDATE CASCADE
```

делают одно и тоже (создают FOREIGN KEY) но только в полной можно добавить уточнения `ON DELETE`