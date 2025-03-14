### 1. Отдельные переменные в общий поток (вывод в html)
```php
error_log()

var_dump()

print_r()

echo
```

### 2. Логирование в html
```php
function debug($data) {
    echo '<pre>' . print_r($data, true) . '</pre>';
}

debug(['message' => 'Hello, world!', 'time' => time()]);
```

### 3. Логирование в файл
```php
function logToFile($data, $file = 'log.txt') {
    file_put_contents($file, print_r($data, true) . PHP_EOL, FILE_APPEND);
}

logToFile(['function' => 'test', 'status' => 'ok']);
```

### 4. Логирование в системный лог
На сервере можно найти логи в файле, указанном в `php.ini` (обычно `/var/log/apache2/error.log` или `/var/log/php_errors.log`).

```php
function logToSystem($data) {
    error_log(print_r($data, true));
}

logToSystem("Пример логирования");
```

### 5. Логирование в браузерную консоль
```php
function logToConsole($data) {
    echo "<script>console.log(" . json_encode($data) . ");</script>";
}

logToConsole(['message' => 'Hello from PHP', 'level' => 'info']);
```