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

## Генерация постов с заполнеными метаполями
```
shell_exec('curl -N http://loripsum.net/api/5 | wp post generate --post_content --count=10');
$post_date = date('Y-m-d-h-i-s',strtotime("-1 days"));
$post_title = ucfirst(substr(shell_exec('curl -N https://loripsum.net/api/1/short/plaintext'), rand(0, 50) , rand(50, 100)));
$new_post_id = shell_exec("curl -N http://loripsum.net/api/5 | wp post generate --count=1 --format=ids --post_content --post_status=draft --post_author=StatisticsUser --allow-root");
update_exec_post($new_post_id, $post_title);
```
