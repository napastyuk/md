psКоманды установки пакетов:
```
sudo apt update && sudo apt upgrade

# Ubuntu
sudo apt install postgresql

# Windows Subsystem for Linux (WSL)
sudo apt install postgresql postgresql-contrib
```

Проверим запустился ли процесс postgres
```
# Проверяет текущее состояние базы данных, то есть показывает запущен ли PostgreSQL или нет
sudo service postgresql status

# Команда служит для запуска PostgreSQL
sudo service postgresql start

# Команда служит для остановки PostgreSQL
sudo service postgresql stop
```

Так же проверим в `ps` 
```bash
ps aux | grep postgres
```
должно найтись что-то с  `bin/postgres`

Дальше важно не запутаться в пользователя и ролях. 
**Пользователи** - это реальные учетные записи в системе
**Роли** - это наборы прав и привилегий, назначаемые пользователям или процессам

В классическом Linux нет ролей. Но они есть в `postgres`.  В обычном linux ты запускаешь `postres` под только что созданным пользователем `postgres` (пользователь с супер правами в `postres`) и попадаешь в только что созданную базу  `postres`.  

В WSL надо добавить пару приседаний:

1. Задать пароль для нового созданного пользователя postgres
```bash
sudo passwd postgres
```

2. Создадим роль внутри postgres  
```bash
# Флаг --createdb добавляет нашей роли возможность создавать базы данных
# По умолчанию этой возможности нет
sudo -u postgres createuser --createdb hexlet
```

теперь можно подключатся с указанием базы подключения
```
psql hexlet
```

либо если что-то не сработало. Продолжаем настраивать через системную базу `postgres`

Создаем пользователя
```bash
sudo -u postgres createuser --interactive
```
Создаем базу
```bash
sudo -u postgres createdb --owner=ilya hexlet
#или 
sudo -u postgres createdb -O ilya hexlet
```
Проверяем какие базы есть в postgres
```bash
psql -l
```

Подключаемся с указанием того и другого
```bash
psql -U ilya -d ilya
```


# Подключение к WSL Postgres из DBeaver

По умолчанию postgres не разрешает подключения из сети (что логично). А DBeaver подключается хоть и по localhost но по сетевому протоколу, поэтому ослабим настройки подключения извне

1. Файл **postgresql.conf** – файл основных настроек. В Ubuntu он располагается в `/etc/postgresql/ВЕРСИЯ_БД/main/postgresql.conf`

```bash
sudo nano /etc/postgresql/12/main/postgresql.conf
```

нам нужно найти строчку `#listen_addresses = ‘localhost’` и заменить на `listen_addresses = ‘*’`

2. **pg_hba.conf** – файл с настройками аутентификации. При подключении клиента к серверу из этого файла выбирается первая строчка соответствующая соединению по четырем параметрам:
- Типу соединения
- Имени БД
- Имени пользователя
- IP адресу клиента
```bash
sudo nano /etc/postgresql/12/main/pg_hba.conf
```

и допишем в конец
```
host    all             ilya             0.0.0.0/0               md5
```

После этого перезапускаем PostgreSQL
```bash
sudo service postgresql restart
```

Получившиеся настройки
**Хост:** localhost
**Порт:** 5432
**Аутентификация:** Database Native
**Пользователь:** ilya
**Пароль:** секретный_пароль

*Если ошибки:*

Проверяем что порт все все стандартный 5432 
```bash
sudo netstat -tulnp | grep postgres
```

Сбросим пароль для пользователя
```bash
sudo -u postgres psql

#выполняем команду
ALTER USER ilya WITH PASSWORD 'new_secure_password';
```


## Подключение к postgres из консоли через psql 

```bash
psql -h server_address -U username -d dbname
```
Где _server_address_ - адрес сервера СУБД, *username* - это ваше имя пользователя, а *dbname* - название базы данных

Некоторые команды
```bash
\l # список баз даннных 

\dt # список таблиц в текущей базе

\du #список ролей
```


## Создание БД из DBeaver

По факту команда `CREATE DATABASE` выполняет копирование существующей базы данных. 

По умолчанию копируется стандартная системная база `template1`. Таким образом, `template1` это шаблон, на основе которого создаются новые базы. Если добавить объекты в `template1`, то впоследствии они будут копироваться в новые базы данных. Это позволяет внести изменения в стандартный набор объектов. Например, если в template1 установить процедурный язык PL/Perl, то он будет доступен в новых базах без дополнительных действий.

Также существует вторая системная база `template0`. При инициализации она содержит те же самые объекты, что и `template1`, предопределённые в рамках устанавливаемой версии `PostgreSQL`. Если в команде `CREATE DATABASE` указать на необходимость копирования `template0` вместо `template1`, то на выходе можно получить "чистую" пользовательскую базу данных
Это удобно когда надо стартовать с другой локали или выполнить скрипт дампа. скрипт дампа лучше выполнять в чистую базу, во избежание каких-либо конфликтов с объектами, которые могли быть добавлены в `template1`.



#php/db #sql