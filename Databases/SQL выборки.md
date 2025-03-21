## Фильтр по данным WHERE

```sql
SELECT * FROM users WHERE id > 60;
```

Возможные операторы после WHERE
- `=` — равно
- `!=` — не равно
- `>` — больше
- `<` — меньше
- `>=` — больше либо равно, не меньше
- `<=` — меньше либо равно, не больше

Нечисловые данные надо оборачивать в кавычки. 
На NULL проверяется через `IS NULL` и `IS NOT NULL`
```sql
SELECT name, created_at FROM courses WHERE created_at > '2022-06-14';
```

## Поиск по подстроке LIKE

символ `%` заменяет любое количество любых символов. В том числе и ноль символов.
```sql
SELECT first_name, last_name FROM users WHERE last_name LIKE 'Sch%';
```
 `ILIKE` делает тоже самое , но без учета регистра

`NOT LIKE` тоже самое но инвертируя результаты поиска

## Поиск по регулярке SIMILAR TO

Работает медленнее чем LIKE но поддерживает мощь регулярок.

```sql
SELECT first_name FROM users WHERE first_name SIMILAR TO '[AB]%';  --выбрать пользователей, чье имя начинается на 'A' или 'B'
```
так же можно инвертировать результаты через `NOT SIMILAR TO`

поиск через `SIMILAR TO` регистрозависимый! Если надо искать в обоих регистрах можно сделать так
```sql
SELECT * FROM users WHERE LOWER(name) SIMILAR TO '[ab]%';
```

- в квадратных скобочках идет перечисление. Перечисление подряд, без символов разделителей как и всегда в регулярках.
- `%` означает любые другие символы. 
- `%[а-я]%` - означает русские буквы где угодно в тексте
- `%@%.%` - шаблон для email
- перечисления: `a-z` `0-9` `а-я`
- `_`  и `[a-z]` это одно и то же
- можно добавить квантификатор например: `[a-z]{2}` означает две любые буквы

Полный список есть в [доке](https://www.postgresql.org/docs/current/functions-matching.html#FUNCTIONS-SIMILARTO-REGEXP)

Для более гибких регулярок именно в Postgres используется поиск через `~` 
```sql
-- Найти все имена, начинающиеся с буквы "A"
SELECT * FROM users WHERE name ~ '^A';

-- Найти имена, содержащие две буквы "o" подряд
SELECT * FROM users WHERE name ~ 'o{2}';

-- Найти имена, начинающиеся с буквы "a" или "A", игнорируя регистр
SELECT * FROM users WHERE name ~* '^a';

-- Найти все имена, начинающиеся с букв от "A" до "F"
SELECT * FROM users WHERE name ~ '^[A-F]';
```

## Объединение условий OR AND

```sql
SELECT
    first_name,
    email
FROM users
WHERE (created_at >= '2022-07-01' AND created_at < '2022-08-01')
    AND email NOT LIKE '%@%.%';
-- пользователи которые зарегистрировались в июле 2022 года и указали некорректную почту при регистрации
```
- Делается через операторы `AND` и `OR`
- У оператора `AND` приоритет выше
- Можно группировать скобочки
- Рекомендуется разносить на разные строчки для читаймости

Тоже самое можно делать через `BETWEEN`
```sql
SELECT *
FROM users
WHERE birthday BETWEEN '2022-01-01' AND '2022-02-01';  --пользователей с датой рождения от 1 января до 1 февраля 2022 года

SELECT *
FROM users 
WHERE birthday NOT BETWEEN '2022-01-01' AND '2022-02-01';  --тоже самое но инвертировано

```

`BETWEEN` Работает включительно!

## Поиск по списку IN
```sql
SELECT id
FROM users
WHERE id IN (1, 2, 5);

-- тоже самое но инвертировано
SELECT id, first_name, last_name
FROM users
WHERE id NOT IN (1, 2, 5);

-- перечислять можно строки
SELECT id
FROM users
WHERE first_name IN ('Lionel', 'Lucienne', 'Jennyfer');
```

## Сортировка выборки ORDER BY

Минимальный пример
```sql
SELECT id
FROM users ORDER BY username;
```

Максимальный пример
```sql
SELECT id
FROM users ORDER BY created_at ASC , created_at DESC NULLS LAST;
```

- обратный порядок `DESC`, прямой порядок (значение по умолчанию) `ASC`
- `NULL` сначала списка `NULLS LAST` , наоборот соотв. `NULLS FIRST` . Дефолт везде разный
- несколько условий сортировки можно перечислять через запятую, второе и последующие условия будут применятся в случае одинаковых значений после первой сортировки 

## Пагинация LIMIT & OFFSET
```sql
SELECT id
FROM users ORDER BY id LIMIT 10 OFFSET 10;
```
- `LIMIT` - ограничить выборку 10 строчками. Можно подставить слово `ALL` чтобы отключить ограничение
- `OFFSET` - сдвиг от начала выборки


## Фильтрация уникальных значений DISTINCT

```sql
SELECT DISTINCT course_id FROM course_members;  -- на какие курсы записались студенты

SELECT DISTINCT course_id, created_at
FROM course_members;  -- тоже самое но в списке будут не id курсов , а уникальные пары id и когда на курс записались

SELECT DISTINCT ON (course_id, created_at)
    course_id,
    created_at
FROM course_members
ORDER BY course_id, created_at DESC; -- тоже самое но в выдачу добавятся еще данные из колонки name 
```

- При использовании `DISTINCT ON` сначала в скобочках указываем поля для фильтрации по уникальному значению, а после скобочек поля которые мы хотим видеть в выдаче (это могут быть те же самые поля).
- ORDER BY тоже важен когда делаешь выборку из нескольких столбцов, чтобы видеть корректность фильтрации


## Агрегатные функции

1. `count()` - количество строк в результате запроса, которые не равны NULL 
```sql
SELECT COUNT(*) FROM users WHERE gender = 'female';  -- сколько непустых строчек в колонке gender равно значению 'female' 

SELECT COUNT(email_confirmed) FROM users;  -- можно указать конкретные столбцы и тогда не NULL строки будут подсчитаны там
```

2. `SUM` сумма всех значений
```sql
SELECT SUM(spent_minutes) FROM course_reviews;
```
поддерживает только числа. Если передать звёздочку, дату или число текстом то выдаст ошибку `Query Error: error: function sum() does not exist`
Если нужна арифметика с датами, то в Postgress можно использовать `INTERVAL`.

3. `AVG` - среднее
```sql
SELECT AVG(spent_minutes) FROM course_reviews WHERE job_title = 'Engineer';
```

4. MIN и MAX 
```sql
SELECT MAX(spent_minutes) FROM course_reviews;

SELECT MIN(spent_minutes) FROM course_reviews;
```
В качестве аргументов в функции `MAX` и `MIN` можно передавать поля числовых типов, а так же даты и строки. 

5. В целом SQL поддерживает почти любую математическую операцию с числовыми типами
```sql
SELECT price + tax AS total_price FROM products;
```
вместо сложения можно подставить любую операцию из [доки](https://postgrespro.ru/docs/postgresql/17/functions-math)

## Группировки GROUP BY

Оператор `GROUP BY` позволяет **объединить одинаковые** значения в заданных полях в группы, а затем выполнить **расчеты** для каждой группы по отдельности.
Пример без подсчета, просто с выводом
```sql
SELECT               -- выбрать и вывести  
    user_id,         -- значение user_id   
    COUNT(user_id)   -- и количество строк в каждой группе 
FROM course_members  -- из таблицы course_memeber 
GROUP BY user_id;    -- одной группой считай уникальные значения из колонки user_id   
```
В более императивном порядке это можно прочитать как:
1. Выбери из таблицы `course_members` колонку `user_id`
2. Отсортируй по колонке `user_id`
3. По результатам сортировки будут видны группы с одинаковым `user_id`. Раздели таблицу на эти группы.   
4. К каждой группе примени операцию `COUNT()`  чтобы посчитать сколько повторяющихся значений `user_id` в каждой группе
5. Кроме `COUNT()` там же  могут быть перечислены агрегатные операции с другими колонками.  
6. Выведи группы парами `user_id` и  `COUNT()` в результирующую табличку

Тоже самое с псевдонимами для результирующих колонок
```sql
SELECT
    user_id AS student,
    COUNT(user_id) AS courses_count
FROM course_members
GROUP BY user_id
ORDER BY user_id;
```

Если надо уникальность не только по полю user_id, но и по двум полям. Например если на курс можно записываться несколько раз, за группу можно взять пользователя который записался на определённый курс. В результатах больше одного будет только у пользователей которые повторно записались на курс.
```sql
SELECT user_id, course_id, COUNT(*)
FROM course_members
GROUP BY user_id, course_id;
```

Таким образом если мы работаем с несколькими полями 
1. Группу полей делаем ключом тогда все эти поля перечисляем и в `GROUP BY` и в `SELECT`  первыми  и в `GROUP BY`
2. Остальным полям обязательно добавить агрегирующую функцию чтобы Postgress понимал что это часть результата а не ключа. 

Еще один пример. Найти самую большую у самую маленькую зарплату по списку должностей
```sql
SELECT
    job_title,
    MAX(salary) AS max_salary,
    MIN(salary) AS min_salary
FROM staff
GROUP BY job_title
ORDER BY job_title;
```
Результат: 
```
    ┌─────────┬─────────────┬────────────┬────────────┐
    │ (index) │ job_title   │ max_salary │ min_salary │
    ├─────────┼─────────────┼────────────┼────────────┤
    │ 0       │ 'Director'  │ 1341       │ 1095       │
    │ 1       │ 'Engineer'  │ 1994       │ 849        │
    │ 2       │ 'Geologist' │ 863        │ 705        │
    │ 3       │ 'Librarian' │ 1114       │ 525        │
    │ 4       │ 'Manager'   │ 1934       │ 583        │
    │ 5       │ 'Professor' │ 1871       │ 840        │
    └─────────┴─────────────┴────────────┴────────────┘
```

## Пост GROUP фильтрация HAVING

`HAVING` задает условие на строки выборки уже после группировки данных

Пример: найти пользователей, которые потратили менее 30 минут в онлайн-школе. У нас есть таблица с логом просмотров курсов разными пользователями , разных курсов.  
```sql
SELECT
    user_id,                   -- (2) по данным из колонки user_id
    SUM(spent_minutes)         -- (4) в каждой группе просуммируй значение из колонки spent_minutes
FROM course_reviews            -- (1) по данным из таблицы course_reviews 
GROUP BY user_id               -- (3) сгруппируй по одинаковым user_id
HAVING SUM(spent_minutes) < 30 -- (5) результат отфильтруй по условию сумма должна быть меньше 30   
```

- Важно что `HAVING` это не `WHERE`.  `HAVING` фильтрует только сгруппированную выборку, а `WHERE` все записи из таблицы.  
- Фильтрация через `WHERE` дешевле чем через `HAVING` !
- В `HAVING` тоже может быть несколько условий объединённых `OR` `AND`

Комплексный пример:
```sql
SELECT
    user_id,
    SUM(spent_minutes)
FROM course_reviews
WHERE created_at >= '2020-01-01'
GROUP BY user_id
HAVING SUM(spent_minutes) < 30 AND user_id <= 40
ORDER BY user_id;
```