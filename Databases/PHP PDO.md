## Подключение
```php
<?php
try {
  $conn = new PDO("mysql:host=localhost","root","mypassword");
  echo "Database connection established";
}
catch (PDOException $e) {
  echo "Connection failed: ".$e->getMessage();
}
?>
```
в конструкторе есть еще много необязательных опций подключения - [спека](https://www.php.net/manual/ru/pdo.connections.php)

если в коде используется `namespase` то при подключение класса PDO надо указать чтобы он искал его в глобальном пространстве имён через `\`
```php
$pdo = new \PDO($dsn, $user, $pass, $options);
```