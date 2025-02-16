#php/slim 

позволяет назначать маршрутам уникальные имена, чтобы затем использовать их для построения URL

Присвоение
```php
$app->get('/users/{id}', function ($request, $response, $args) {
    $userId = $args['id'];
    $response->getBody()->write("User ID: $userId");
    return $response;
})->setName('user_profile'); //присвоение функцией setName()
```

Генерация по имени (в шаблонах или обработчиках)
```php
$routeParser = $app->getRouteCollector()->getRouteParser();
$url = $routeParser->urlFor('user_profile', ['id' => 42]);
echo $url; // Выведет: /users/42
```

Добавление query-параметров
```php
$urlWithQuery = $routeParser->urlFor('user_profile', ['id' => 42], ['sort' => 'asc']); 
echo $urlWithQuery; // Выведет: /users/42?sort=asc
```
