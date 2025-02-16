#php/slim

### Начальный шаблон
```php
require __DIR__ . '/../vendor/autoload.php';
use Slim\Factory\AppFactory;

$faker = \Faker\Factory::create();
$faker->seed(1234);

$domains = [];
for ($i = 0; $i < 10; $i++) {
    $domains[] = $faker->domainName;
}

$phones = [];
for ($i = 0; $i < 10; $i++) {
    $phones[] = $faker->phoneNumber;
}

$app = AppFactory::create();
$app->addErrorMiddleware(true, true, true);

$app->get('/', function ($request, $response) {
    return $response->write('go to the /phones or /domains');
});

$app->get('/phones', function ($request, $response) use ($phones) {
    return $response->write(json_encode($phones));
});

$app->get('/domains', function ($request, $response) use ($domains) {
    return $response->write(json_encode($domains));
});

//пример возврата кода ошибки
$app->get('/users', function ($request, $response) {
    return $response->withStatus(302);
});

//пример возврата json
$app->get('/companies', function ($request, $response) use ($companies) {
    $page = $request->getQueryParam('page', 1);
    $per = $request->getQueryParam('per', 5);
    $offset = ($page === 1) ? 0 : ($page - 1) * $per;
    $newResponse = $response->withHeader('Content-type', 'application/json');
    $currentPart = array_slice($companies, $offset, $per);
    return $newResponse->write(json_encode($currentPart));
});

$app->run();
```

### Динамическая маршрутизация по id
```php
$app->get('/companies/{id:[0-9]+}', function ($request, $response, array $args) use ($companies) {
    $id = $args['id'];
    if (array_key_exists($id, $companies)) {
        $companiesCollection = collect($companies);
        $result = $companiesCollection->firstWhere('id', $id);
        $okResponse = $response->withHeader('Content-type', 'application/json');
        return $okResponse->write(json_encode($result));
    } else {
        $notFoundResponse = $response->withStatus(404);
        return $notFoundResponse->write("404 error");
    }
});
```

Шаблонизация
```php
$app->get('/courses', function ($request, $response, $args) use ($courses) {
	params = ['id' => $args['id'], 'nickname' => 'user-' . $args['id']];
    return $this->get('renderer')->render($response, 'courses/index.phtml', $params);
});
```

```php
<table>
  <?php foreach ($courses as $course): ?>
    <tr>
      <td>
          <?= $course['id'] ?>
      </td>
      <td>
          <?= $course['name'] ?>
      </td>
    </tr>
  <?php endforeach ?>
</table>
```

### Еще пример шаблонизации. Вывод пользователей
```php 
$app->get('/users', function ($request, $response) use ($users) {
    $params = ['users' => $users];
    return $this->get('renderer')->render($response, 'users/index.phtml', $params);
});

$app->get('/users/{id}', function ($request, $response, $args) use ($users) {
    $id = (int) $args['id'];
    $user = collect($users)->firstWhere('id', $id);
    $params = ['user' => $user];
    return $this->get('renderer')->render($response, 'users/show.phtml', $params);
});
```

//index.phtml вывод списка пользователей
```php
<table>
    <?php foreach ($users as $user) : ?>
        <tr>
            <td>
                <?= $user['id'] ?>
            </td>
            <td>
                <a href="/users/<?= $user['id'] ?>"><?= $user['firstName'] ?></a>
            </td>
        </tr>
    <?php endforeach ?>
</table>
```

//show.phtml вывод конкретного пользователя
```php
<?php foreach ($user as $key => $value) : ?>
    <div>
        <?= $key ?>: <?= $value ?>
    </div>
<?php endforeach ?>
```


### Пример поисковой строки. Поиск по пользователям
```php
$app->get('/users', function ($request, $response, $args) use($users) {
    $searchingString = $request -> getQueryParams('user-name')['user-name'] ?? "";
    
    #или через стрелочную функцию
    $foundUsers = array_filter($users, fn($user) => str_contains($user, $searchingString));

	#или через анонимную функцию
	$foundUsers = array_filter($users, function($userItem) use ($searchingString) {
        return str_contains($userItem['firstName'], $searchingString); 
    });
   
    $params = ['users' => $foundUsers, 'value' => $searchingString];
    return $this->get('renderer')->render($response, 'users/index.phtml', $params);
});
```

```php
<form action="" method="get">
    <label for="find-user">Найти пользователя</label>
    <input type="text" name="user-name" id="find-user" value="<?= htmlspecialchars($value) ?>">
    <button type="submit">Найти</button>
</form>
<hr>
<ul>
    <?php foreach ($users as $user) : ?>
    <li><?= $user ?></li>
    <?php endforeach ?>
</ul>
```

//удаление
public/index.php
```php 
$app->delete('/posts/{id}', function ($request, $response, array $args) use ($repo, $router) {
    $repo->destroy($args['id']);
    $this->get('flash')->addMessage('success', 'Post has been deleted');
    return $response->withRedirect($router->urlFor('posts'));
});
```

template/posts/index.phtml
```php
<?php foreach ($posts as $post): ?>
  <div>
    <?= htmlspecialchars($post['name']) ?>
    <form action="/posts/<?= $post['id'] ?>" method="post">
      <input type="hidden" name="_METHOD" value="DELETE">
      <input type="submit" value="Delete">
    </form>
  </div>
<?php endforeach ?>
```

### Мидлвара с добавлением заголовка
```php
$addHashMiddlware = function (Request $request, RequestHandler $handler): ResponseInterface {
    $response = $handler->handle($request);
    $body = $response->getBody();
    $hash = hash(algo: 'sha256', data: $body);
    $response = $response->withHeader('X-Content-Hash', $hash);
    return $response;
};
$app->add($addHashMiddlware);
```

### Работа с куками. Корзина товаров
```php
$app->post('/cart-items', function ($request, $response) {
    $item = $request->getParsedBodyParam('item');
    $cart = json_decode($request->getCookieParam('cart', json_encode([])), true);

    $id = $item['id'];
    if (!isset($cart[$id])) {
        $cart[$id] = ['name' => $item['name'], 'count' => 1];
    } else {
        $cart[$id]['count'] += 1;
    }

    $encodedCart = json_encode($cart);
    return $response->withHeader('Set-Cookie', "cart={$encodedCart}")
        ->withRedirect('/');
});

$app->delete('/cart-items', function ($request, $response) {
    $encodedCart = json_encode([]);
    return $response->withHeader('Set-Cookie', "cart={$encodedCart}")
        ->withRedirect('/');
});
```