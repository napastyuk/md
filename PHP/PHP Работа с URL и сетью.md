#php/сеть 
## Путь сетевого запроса

1. Браузер посылает запрос
2. Запрос приходит сервер, обрабатывается web-сервером(Ngixn-ом). 
3. Тот в соотв. со своим конфигом , 'берёт' файл c исходником(допустим index.php) и отдает его PHP интерпретатору
4. Тот проходится по данному ему файлу и везде внутри тегов PHP запускает выполнение кода
5. От nginx он получает исходный запрос и другие данные и складывает его в суперглобальные переменные, они  всегда доступны во всех областях видимости
## Суперглобальные или встроенные переменные в PHP

`$GLOBALS` - Ссылки на все переменные глобальной области видимости
`$_SERVER` - Информация о сервере и среде исполнения
`$_GET` - Переменные HTTP GET
`$_POST` - Переменные HTTP POST
`$_FILES` - Переменные файлов, загруженных по HTTP
`$_COOKIE` - HTTP Cookies
`$_SESSION` - Переменные сессии
`$_REQUEST` - Переменные HTTP-запроса
`$_ENV` - Переменные окружения

Важный момент. В `$_GET` помещаются параметры отправленные через URL (любым типом запроса), а в `$_POST` только вложения типа `Multipart Form` и `Form URL Encoded`.  Все остальные типы POST вложений можно прочитать через
```php
echo file_get_contents('php://input');
```
`$_REQUEST` это просто объединение `$_GET` и `$_POST` без дополнительной функциональности.

## Парсинг URL

В целом на стороне клиента разных частей URI гораздо больше.  
Если говорить о входящем запросе, то до PHP доходит 
1. Заголовки запроса (включая host и метод запроса ) 
2. параметры если GET Запрос
3. Тело если POST запрос
Остальное (user,pass, port, fragment) или уже настроено на сервер , либо не пропускается. 

Собрать полный URL можно только по частям:
- Прокол в `$_SERVER['HTTPS']`
- Хост в `$_SERVER['HTTP_HOST']`
- Путь с параметрами в `$_SERVER['REQUEST_URI']`
И потом склеить и отправить в функцию  `parse_url()`.

 
Пример содержимого `$_SERVER` для запроса  `http://localhost:8080/test?fooGET=barGET`
```
Array
(
    [DOCUMENT_ROOT] => C:\projects\test
    [REMOTE_ADDR] => ::1
    [REMOTE_PORT] => 53276
    [SERVER_SOFTWARE] => PHP/8.3.14 (Development Server)
    [SERVER_PROTOCOL] => HTTP/1.1
    [SERVER_NAME] => localhost
    [SERVER_PORT] => 8080
    [REQUEST_URI] => /test?fooGET=barGET
    [REQUEST_METHOD] => POST
    [SCRIPT_NAME] => /index.php
    [SCRIPT_FILENAME] => C:\projects\test\index.php
    [PATH_INFO] => /test
    [PHP_SELF] => /index.php/test
    [QUERY_STRING] => fooGET=barGET
    [HTTP_ACCEPT] => application/json, text/plain, */*
    [CONTENT_TYPE] => application/sparql-query
    [HTTP_CONTENT_TYPE] => application/sparql-query
    [HTTP_USER_AGENT] => bruno-runtime/1.38.1
    [HTTP_REQUEST_START_TIME] => 1737229308681
    [HTTP_ACCEPT_ENCODING] => gzip, compress, deflate, br
    [HTTP_HOST] => localhost:8080
    [HTTP_CONNECTION] => keep-alive
    [CONTENT_LENGTH] => 0
    [HTTP_CONTENT_LENGTH] => 0
    [REQUEST_TIME_FLOAT] => 1737229308.6843
    [REQUEST_TIME] => 1737229308
)
```


## Установка кодов ошибок и заголовков
Установка заголовков. Команду размещать до любого вывода.
```php
header("Cache-Control: no-cache, must-revalidate"); // HTTP/1.1  
header("Expires: Sat, 26 Jul 1997 05:00:00 GMT"); // Дата в прошлом
```

Пример с принудительным редиректом
```php
/* Перенаправление броузера на другую страницу в той же директории, что и  
изначально запрошенная */  
$host  = $_SERVER['HTTP_HOST'];  
$uri   = rtrim(dirname($_SERVER['PHP_SELF']), '/\\');  
$extra = 'mypage.php';  
header("Location: http://$host$uri/$extra");  
exit;
```


Установка кодов ошибки
```php
var_dump(http_response_code());  // Читаем текущий код 
var_dump(http_response_code(404)); // Устанавливаем новый код    
```

## Пример мини-роутера
```php
if ($_SERVER['REQUEST_URI'] === '/') {
    echo '<a href="/welcome">welcome</a>
    <br>
    <a href="/not-found">not-found</a>';
} elseif ($_SERVER['REQUEST_URI'] === '/welcome') {
    echo '<a href="/">main</a>';
} else {
    http_response_code(404);
    echo 'Page not found. <a href="/">main</a>';
};
```