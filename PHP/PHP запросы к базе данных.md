#php/базы_данных
## Подключение к БД
```ini
[db]
host = '127.0.0.1'
database = 'homestead'
user = 'otus'
password = 'password'
```

```php
$configuration = parse_ini_file('config.ini',true);
$connection = mysqli_connect(
	$configuration['db']['host'],
	$configuration['db']['user'],
	$configuration['db']['password'],
	$configuration['db']['database']
);

if(!$connection) {
	echo "Невозможно подключится к БД";
	die();
}
```

## Обычный запрос
```php
    $select = "SELECT * FROM users WHERE login = 'otus'";
    $result = mysqli_query($connection, $select);
```

## Подготовленный запрос
```php
    $userSqlStatement = mysqli_prepare($connection, "SELECT * FROM users WHERE login = ?");    
    mysqli_stmt_bind_param($userSqlStatement, "s", $login);
    mysqli_stmt_execute($userSqlStatement);  
    $result = mysqli_stmt_get_result($userSqlStatement);
```

