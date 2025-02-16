
### Чтение GET параметров

```php
$app->get('/example', function (Request $request, Response $response) {

	// Получение всех GET-параметров 
	$params = $request->getQueryParams(); 
	
	// Получение конкретного параметра с дефолтным значением 
	$param1 = $params['param1'] ?? 'default_value';
	
	$response->getBody()->write("Param1: $param1");
	return $response; 

});
```

### Установка GET параметров
в slim только через формирование URL
```php
$app->get('/posts', function ($request, $response) {
//...
$basePath = $request->getUri()->getPath();
$nexpPageUrl = $basePath.'?'.http_build_query(['page' => $nextPage]); // сформирует /post?post=2
//...
return $this->get('renderer')->render($response, 'posts/index.phtml', $params);
});
```


### Чтение POST параметров
```php
$app->post('/schools', function ($request, $response) use ($router) {
    ...
    // Извлекаем данные формы
    $schoolData = $request->getParsedBodyParam('school');
    ...
    return $this->get('renderer')->render($response, 'schools/new.phtml');
});
```

### Установка POST  параметров
Можно через отправку формы 
```php
<form action="/schools/<?= htmlspecialchars($school['id']) ?>" method="post">
    <input type="hidden" name="_METHOD" value="PATCH">
    <div>
      <label>
          Название *
          <input type="text" name="school[name]" value="<?= htmlspecialchars($school['name'] ?? ''); ?>">
      </label>
      <?php if (isset($errors['name'])): ?>
          <div><?= $errors['name'] ?></div>
      <?php endif ?>
    </div>
    <input type="submit" value="Update">
</form>
```
