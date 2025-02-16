#php/slim

Каркас приложения `public/index.html`
```php
<?php
// подключения внешних классов
use Slim\Factory\AppFactory;
use DI\Container;
use App\Validator;
//подключение библиотке из композера
require '/composer/vendor/autoload.php';

//активация хранилища для основной сущности - курсов
$repo = new App\CourseRepository();

//подключение шаблонов
$container = new Container();
$container->set('renderer', function () {
    return new \Slim\Views\PhpRenderer(__DIR__ . '/../templates');
});
$app = AppFactory::createFromContainer($container);

//загушка slim для обработки методов с ошибкой
$app->addErrorMiddleware(true, true, true);

//загрузка первого экрана. На нем только ссылка на основной экран
$app->get('/', function ($request, $response) {
    return $this->get('renderer')->render($response, 'index.phtml');
});

//загрузка экрана с курсами
$app->get('/courses', function ($request, $response) use ($repo) {
    $params = [
        'courses' => $repo->all()
    ];
    return $this->get('renderer')->render($response, 'courses/index.phtml', $params);
});
```

Во время первых загрузок там ничего нет. Во время последующих он будет выводит список курсов.   Шаблон `courses/index.phtml`

```php
<a href="/courses/new">Новый курс</a>
<?php foreach ($courses as $course): ?>
  <div>
    <?= htmlspecialchars($course['title']) ?>
  </div>
<?php endforeach ?>
```

После перехода по ссылке `Новый курс` открывается форма ввода новых курсов. 

```php
$app->get('/courses/new', function ($request, $response) use ($repo) {
// поставим заглушку на массив с ошибками, они будут в другом обработчике , но тоже отправлятся на тот же шаблон     
    $params = [  
        'course' => ['title' => '', 'paid' => ''],
        'errors' => []
    ];
    return $this->get('renderer')->render($response, 'courses/new.phtml', $params);
});
```

Вот сам шаблон `templates\courses\new.phtml`

```php
<form action="/courses" method="post">
    <label for="title">Имя курса</label>
    <input type="text" name="course[title]" id="title" value="<?= htmlspecialchars($course['title']) ?>">
	    <?php if (isset($errors['title'])): ?>
	      <div><?= $errors['title'] ?></div>
	    <?php endif ?>
    <br>
    
    <label for="paid">Платность курса</label>
    <input type="checkbox" name="course[paid]" id="paid">
	    <?php if (isset($errors['paid'])): ?>
	      <div><?= $errors['paid'] ?></div>
	    <?php endif ?>
    <br>
    
    <button type="submit">Создать</button>
</form>
```

После нажатия на кнопку `submit`  как указано в теге `form`  отправляется POST запрос на адрес `/courses`

```php
$app->post('/courses', function ($request, $response) use ($repo) {
    $validator = new Validator(); //призываем валидатора
    
    $course = $request->getParsedBody()['course']; //достаем из запроса данные формы
    
    $errors = $validator->validate($course); // отправляем даныне формы в валидатор

    if (count($errors) === 0) { //если все ок - сохраняем форму и редиректимся со страницы формы страницу списока курсов
        $repo->save($course);
        return $response->withRedirect('/courses', 302);
    }
	//а вот если есть ошибки надо их показать прямо в форме 
	//для этого в шаблоне templates\courses\new.phtml были php вставки.
	//заполненые поля вернем обратно в форму и добавим div-ы c ошибками
    $params = [
        'course' => [
                    'title' => $course['title'] ?? '',
                    'paid' => $course['paid'] ?? ''
                    ],
        'errors' => $errors
    ];
	
    $newResponse = $response->withStatus(422); //ну и добавим нужный код ошибки
    return $this->get('renderer')->render($newResponse, 'courses/new.phtml', $params);
});

$app->run();
```

