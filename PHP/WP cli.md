## Вывод значений кастомных полей в WCI
`$ wp eval 'print_r(get_fields(1, false));'`

Импорт /экспорт значний спокойно делается стандарными средствами тк  acf хранит данные как записи

## Пример шоткатов для импорта-экспорта базы
Сохранить в wp-cli.yml следующий код:
```
@staging: 
     ssh: root@staging.ru/home/www/staging.ru/current
# @production: 
#      ssh: shawn@production.com/var / www / html /

#wp @staging search-replace htts://production.ru http://staging.ru --export --allow-root | wp db import -
```

## CLI копирование файлов с сервера
```
#scp -r root@your.server.example.com:/path/to/foo /home/user/Desktop/
```
Не включая завершающий '/' в конце foo, вы скопируете сам каталог (включая его содержимое), а не только его содержимое.

## Еще один пример копирования базы
```
wp @staging search-replace htts://website.ru http://website.local --export=database.sql --allow-root
wp db import database.sql --dbuser=root --dbpass=''
```