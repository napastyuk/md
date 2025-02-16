#php/slim 

`public/index.php`
```php
<?php
use Slim\Factory\AppFactory;
use DI\Container;

require '/composer/vendor/autoload.php';

$container = new Container();
$container->set('renderer', function () {
    return new Slim\Views\PhpRenderer(__DIR__ . '/../templates');
});

$container->set('flash', function () {
    return new Slim\Flash\Messages();
});

$app = AppFactory::createFromContainer($container);
$app->addErrorMiddleware(true, true, true);

$repo = new App\PostRepository();
$router = $app->getRouteCollector()->getRouteParser();

$app->get('/', function ($request, $response) {
    return $this->get('renderer')->render($response, 'index.phtml');
});

$app->get('/posts', function ($request, $response) use ($repo) {
    $flash = $this->get('flash')->getMessages();
    $params = [
        'flash' => $flash,
        'posts' => $repo->all()
    ];
    return $this->get('renderer')->render($response, 'posts/index.phtml', $params);
})->setName('posts');

$app->get('/posts/new', function ($request, $response) {
    $params = [
        'post' => [],
        'error' => []
    ];
    return $this->get('renderer')->render($response, 'posts/new.phtml', $params);
});

$app->post('/posts', function ($request, $response) use ($router, $repo) {
    $post = [];
    $post['name'] = $request->getParsedBodyParam('post')['name'];
    $post['body'] = $request->getParsedBodyParam('post')['body'];

    $validator = new App\Validator();
    $error = $validator->validate($post);

    if (count($error) === 0) {
        $repo -> save($post);
        $this->get('flash')->addMessage('success', 'Post has been created');
        $url = $router->urlFor('posts');
        return $response->withRedirect($url);
    }

    $params = [
        'post' => $post,
        'error' => $error
    ];

    $newResponse = $response->withStatus(422);
    return $this->get('renderer')->render($newResponse, 'posts/new.phtml', $params);
});

$app->run();
```

`template\posts\new.phtml`
```php
<a href="/posts">Посты</a>
<br>
<br>
<form action="/posts" method="post">
    <label for="name">
        Заголовок поста
        <input type="text" name="post[name]" value="<?= htmlspecialchars($post['name'] ?? "") ?>">
    </label>
        <?php if (isset($error['name'])): ?>
            <div><?= $error['name'] ?></div>
        <?php endif ?>
        <br>
        <br>
    <label for="body">
        Тест поста
        <textarea name="post[body]" id=""><?= htmlspecialchars($post['body'] ?? "") ?></textarea>
    </label>
        <?php if (isset($error['body'])): ?>
            <div><?= $error['body'] ?></div>
        <?php endif ?>
        <br>
        <br>
    <input type="submit" value="Сохранить">
</form>
```

`template\posts\index.phtml`
```php
<?php if (count($flash) > 0): ?>
  <ul>
  <?php foreach ($flash as $messages): ?>
      <?php foreach ($messages as $message): ?>
          <li><?= $message ?></li>
      <?php endforeach ?>
  <?php endforeach ?>
  </ul>
<?php endif ?>

<a href="/posts/new">Новый пост</a>

<?php foreach ($posts as $post): ?>
  <div>
    <?= htmlspecialchars($post['name']) ?>
  </div>
<?php endforeach ?>
```