Соединение любого количества таблиц. Самый типичный случай использования `JOIN` - это связывание таблиц через внешний ключ.
# Соединение без условия CROSS JOIN 

Объединение двух таблиц так что бы получились все возможные комбинации из строк обоих таблиц

| color_name | material_name | color_name <br>`CROSS JOIN` <br>material_name |
| :--------: | :-----------: | :-------------------------------------------: |
|     A      |       0       |                     A  0                      |
|     B      |       1       |                     A  1                      |
|            |       2       |                     A  2                      |
|            |               |                     B  0                      |
|            |               |                     B  1                      |
|            |               |                     B  2                      |
```sql
SELECT
    color_name,  -- первый столбец 
    material_name -- второй столбец из другой таблицы
FROM colors  -- первая таблица
CROSS JOIN materials;  -- вторая таблица
```

# Соединение с условием INNER , LEFT , RIGHT JOIN

| Таблица 1 | Таблица 2 | Таблица 1<br>`INNER JOIN`<br>Таблица 2 | Таблица 1<br>`LEFT JOIN`<br>Таблица 2 | Таблица 1<br>`RIGHT JOIN`<br>Таблица 2 | Таблица 1<br>`FULL JOIN`<br>Таблица 2 |
| :-------: | :-------: | :------------------------------------: | :-----------------------------------: | :------------------------------------: | :-----------------------------------: |
|     A     |           |                                        |                A  NULL                |                                        |                A  NULL                |
|     B     |     0     |                  В  О                  |                 В  О                  |                  В  О                  |                 В  О                  |
|     С     |     1     |                  В  1                  |                 В  1                  |                  В  1                  |                 В  1                  |
|           |     2     |                  С  2                  |                 С  2                  |                  С  2                  |                 С  2                  |
|           |     3     |                                        |                                       |                 NULL 3                 |                NULL 3                 |
Объяснение

| тип соединения             | валидные пары | строки без пары из TableA | строки без пары из TableB |
| -------------------------- | ------------- | ------------------------- | ------------------------- |
| `TableA INNER JOIN TableB` | добавляются   | **не добавляются**        | **не добавляются**        |
| `TableA LEFT JOIN TableB`  | добавляются   | добавляются               | **не добавляются**        |
| `TableA RIGHT JOIN TableB` | добавляются   | **не добавляются**        | добавляются               |
| `TableA FULL JOIN TableB`  | добавляются   | добавляются               | добавляются               |
По правилам SQL, строки без пары добавляются в результат всего один раз, а вместо недостающих значений устанавливается `NULL`.

## INNER JOIN

Пример
```sql
SELECT
    author_name,
    title
FROM books -- первая таблица
INNER JOIN authors -- вторая таблица
    ON book_author_id = author_id -- условие соединения таблиц
```
Тоже самое с алиасами
```sql
SELECT
    employees.name,
    departments.name -- добавили имена таблиц для более конретного указания
FROM employees AS emp -- объявили псевдоним для employees для краткости
INNER JOIN departments AS dep -- объявили псевдоним для departments
    ON emp.department_id = dep.department_id; -- добавили имена таблиц и использовали короткое имя таблицы
```

Для наглядного итогового вывода можно добавлять алиасы/псевдонимы и для столбцов
```sql
SELECT
    emp.name AS employee,
    dep.name AS department
FROM employees AS emp
INNER JOIN departments AS dep ON
    emp.department_id = dep.department_id
```
Важно что в `INNER JOIN` можно использовать алиасы для таблицы, но нельзя использовать алиасы для столбцов. [Причина](SQL%20последовательность%20выполнения%20запроса.md)

## LEFT JOIN

На примере запроса , который считает количество сотрудников в отделе
```sql
SELECT
    dep.name AS department, -- колонка с названием отдела, по ней GROUP BY потом будет группировать
    COUNT(emp.employee_id) AS employees_count -- колонка с количеством
FROM departments AS dep -- это левая таблица, даныне из неё всегда сохраняются  
LEFT JOIN employees AS emp  -- это правая, в ней может не быть совпадений, тогда подставляется NULL
ON dep.department_id = emp.department_id  -- это равенство по которому ищут совпадения в обоих таблицах
GROUP BY dep.name
```

## FULL OUTER JOIN
Он же `FULL JOIN`  (это синонимы в SQL)  - включает не только общие строки, но и не найденные пары из обоих таблиц
```sql
SELECT
    dep.name as department,
    emp.name as employee
FROM departments AS dep
FULL JOIN employees AS emp ON
    dep.department_id = emp.department_id;
```


# Соединение с отрицанием ANTI JOIN

Все тоже самое что и при JOIN только добавляем пост фильтрацию `WHERE`.  
Допустим надо получить покупателей которые не сделали , ни одного заказа

```sql
SELECT cus.customer_name -- убрали из итоговой таблички столбец order_id, он все равно не нужен
FROM customers AS cus
LEFT JOIN orders AS ord
    ON cus.customer_id = ord.customer_id  -- выборка будет включать всех, и с заказаи и без
WHERE ord.order_id IS NULL -- отбираем только покупателей без заказа
```

# Соединение таблицы с собой SELF JOIN
`SELF JOIN` - это прием, когда выполняется соединение таблицы с самой собой. СУБД обрабатывает такие запросы так, будто мы соединяем две разные таблицы с одинаковой структурой и данными. Используется
- Когда строки внутри одной таблицы ссылаются друг на друга, то есть образуют граф
```sql
SELECT
    empl.employee_name,
    mngr.employee_name AS manager_name --алиас обязателейн для SELF JOIN
FROM employees AS empl
LEFT JOIN employees AS mngr ON  -- можно использовать другие виды JOIN это не важно
    empl.manager_id = mngr.employee_id
```

- Когда нужно выполнить поиск разных строк, у которых совпадает значение одного из полей. Например найдем найдем пользователей с которые указали один и тот же email
```sql
SELECT
    u1.nickname AS first_nickname,
    u2.nickname AS second_nickname,
    u1.email
FROM users AS u1
INNER JOIN users AS u2 ON
    u1.email = u2.email
    AND u1.user_id != u2.user_id
```

Более абстрактный пример:
```sql
SELECT
    A.*,
    B.*
FROM MyTable AS A
INNER JOIN MyTable AS B ON
    A.Id != B.Id AND A.My_Field = B.My_Field  -- условие соединения смотрит чтобы идентификаторы были разными, но значение нужного поля было одинаковым
```
# Соединение нескольких таблиц
```sql
SELECT
    drv.driver_name AS driver, -- имя водителя
    pas.passenger_name AS passenger, -- имя пассажира
    rd.price AS ride_price -- стоимость поездки
FROM rides AS rd
INNER JOIN drivers AS drv
    ON rd.driver_id = drv.driver_id  -- первое соединение
INNER JOIN passengers AS pas       
    ON rd.passenger_id = pas.passenger_id -- второе соединение
```


#sql #php/db


