
| Type                            | Тип                                       | Диапазон                                    | Точность                     |
| ------------------------------- | ----------------------------------------- | ------------------------------------------- | ---------------------------- |
| `varchar` , `character varying` | строка с ограничением максимальной длины  | сколько указано                             | 1 символ                     |
| `text`                          | строк без ограничения длинны              | без ограничений                             | 1 символ                     |
| `integer`                       | типичный выбор для целых чисел            | -2147483648 .. +2147483647                  | 1                            |
| `bigint`                        | целое в большом диапазоне                 | -9223372036854775808 .. 9223372036854775807 | 1                            |
| `real`                          | вещественное число с переменной точностью | -2147483648 .. +2147483647                  | в пределах 6 десятичных цифр |
| `timestamp`                     | дата и время (без часового пояса)         | 4713 до н. э.   ..   294276 н. э.           | 1 микросекунда               |
| `date`                          | дата (без времени суток)                  | 4713 до н. э.   ..   5874897 н. э.          | 1 день                       |
| `time`                          | время суток (без даты)                    | 00:00:00 ..  24:00:00                       | 1 микросекунда               |
| `boolean`                       | true или false                            | -                                           | -                            |
Для незаданных или стертых полей используется `NULL`

Пример вставки данных
```sql
CREATE TABLE students (
  id bigint, 
  first_name VARCHAR(50), 
  last_name VARCHAR(50), 
  email VARCHAR(255), 
  bio VARCHAR(400), 
  is_studying BOOLEAN, 
  updated_at TIMESTAMP, 
  created_at TIMESTAMP
);

INSERT INTO students (id, first_name, last_name, email, bio, is_studying, updated_at, created_at)
VALUES 
(1, 'Vasya', 'Pupkin', 'vasya@hexlet.test', 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Morbi iaculis massa ut neque gravida pellentesque.', TRUE, '2024-01-01', '2024-01-01'),
(1, 'Vasya', 'Pupkin', 'vasya@hexlet.test', 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Morbi iaculis massa ut neque gravida pellentesque.', TRUE, '2024-01-01', '2024-01-01')
```

Песочница https://www.db-fiddle.com/

Ссылка на доку (ru)  https://postgrespro.ru/docs/postgresql/17/datatype