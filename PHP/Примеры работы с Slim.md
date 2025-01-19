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