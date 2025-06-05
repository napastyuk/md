## Запуск
PHP скрипты можно запускать не только вместе с web-сервером, но и отдельно командами в терминале.
```bash
php youScript.php
```
Это удобно когда надо выполнить сервисную функцию или через crone  запустить регулярное выполнение скрипта. Причем файл не обязательно должен быть один, запускаемый файл может быть точкой запуска для целого микросервиса.
## Обработка параметров
Все что написано после `php` в команде запуска доступно в переменной `$argv`

```bash
php cli.php 1 2

array(3) {
  [0] =>
  string(7) "cli.php"
  [1] =>
  string(1) "3"
  [2] =>
  string(1) "4"
}
```

Обработка именных параметров
```php
unset($argv[0]); 
$params = []; 
foreach ($argv as $argument) { 
    preg_match('/^-(.+)=(.+)$/', $argument, $matches); //регулярка которая ищет слова начинающиеся с тире
    if (!empty($matches)) { 
       $paramName = $matches[1]; 
       $paramValue = $matches[2]; 
       $params[$paramName] = $paramValue; 
    } 
}
var_dump($params);
```

```bash
>php cli.php -a=3 -b=4

array(2) {
  'a' =>
  string(1) "3"
  'b' =>
  string(1) "4"
}
```