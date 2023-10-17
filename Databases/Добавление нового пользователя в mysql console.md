запускаем mysql консоль
`>mysql`  
в консоли
```mysql
use mysql # выбираем базу данных
select * from user; # смотрим тамблицу с пользователями
select * from user \G; # тоже самое но столбцы в строчку
CREATE USER 'otus'@'%' IDENTIFIED BY 'password'; # добавляем нового пользователя
GRANT ALL PRIVILEGES ON *.* TO 'otus'@'%'; # прописываем ему права
FLUSH PRIVILEGES; # после изменения прав надо не забывать эту команду
```

Посмотреть список текущих подключений к базе
```mysql
SHOW FULL PROCESSLIST;  
```


#MySQL  