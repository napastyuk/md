запускаем mysql консоль
`>mysql`  
в консоли
```mysql
use mysql # выбираем базу данных
CREATE USER 'otus'@'%' IDENTIFIED BY 'typePasswordHere'; # добавляем нового пользователя
GRANT ALL PRIVILEGES ON *.* TO 'otus'@'%'; # прописываем ему права
FLUSH PRIVILEGES; # после изменения прав надо не забывать эту команду
```

Посмотреть список текущих подключений к базе
```mysql
SHOW FULL PROCESSLIST;  
```


#sql