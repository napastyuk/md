#php/ооп #php/инструменты 

Без автозагрузки файлы с классами надо подключать вручную, плюс следить чтобы не было пересечений имён. Чтобы это упростить ввели пространство имён и автозагрузка классов 

Код без автозагрузки:
```php
require_once 'src/Controllers/HomeController.php';
require_once 'src/Services/UserService.php';

$user = new HomeController();
$service = new UserService();
```

Как получить код с автозагрузкой:

1. Придерживаться файловой структуры PSR-4. Тогда путь к файлу будет соответствовать пространству имён
   - Пространство имен: `App\Models\User`
   - Соответствующий файл: `src/Models/User.php`

2. В подключаемом классе прописывают к какому namespace он относится. Имя файла и класса совпадают! Namespace может быть вложенным чтобы соответствовать файловой структуре. Вложенность разделяется `\`
```php
//src/Services/Mailer.php
namespace App\Services;

class Mailer {
    public function send() {
	    //...
    }
}
```

3. В composer.json не забываем указать соответствия пространства имён и файлов
Пример структуры файлов
```
project/
├── src/
│   ├── Controllers/
│   │   └── HomeController.php
│   └── Services/
│       └── UserService.php
|       └── Mail.php 
├── vendor/
└── composer.json
```

```json
"autoload": {
    "psr-4": {
        "App\\": "src/" //указание на соотвествие
    }
},
"require": {
	//...
}
```
Для обновления настроек автозагрузки
```bash
composer dump-autoload
```

4. В корневом файле подключаем composer и указываем какие namespace нам нужны. Последнее слово в цепочке `use` соответствует  имени класса перед `new` 
```php
require __DIR__ . '/vendor/autoload.php';

use App\Services\Mailer; //теперь не придётся искать класс mailer по всему глобальному namespace, у него указан путь

$mailer = new Mailer();
$mailer->send();

```

5. Есть namespace которые начинаются с App. Обычно это структура задается фреймворком.  И есть namespace которые начинаются с `\` Если пространство имен начинается с `\`, это означает абсолютный путь, начиная от глобального пространства имен. Он используется для стандартных классов или инструментов, которые должны быть доступны из любого места в проекте.
```php
namespace base\classes; 
class Utils { 
	// ... 
}
```
использование
```php
$utils = new \base\classes\Utils();
```

6. Подключать можно не только классы, но и константы и функции
```php
use function App\Utils\helperFunction; 
use const App\Config\DEFAULT_VALUE; 

helperFunction(); 
echo DEFAULT_VALUE;
```

7. Можно использовать и без `use`.  Тогда namespace указывают перед именем класса. 
```php
$mailer = new App\Services\Mailer(); 
$logger = new App\Utils\Logger();
```

8. А можно добавлять псевдонимы чтобы разруливать одинаковые имена  и просто писать после  `new` меньше букв
```php
use App\Services\Mailer as ServiceMailer; 
use External\Libs\Mailer as ExternalMailer; 

$serviceMailer = new ServiceMailer(); 
$externalMailer = new ExternalMailer();
```



### Пример подключения не класса, а функции с автозагрузкой
index.php
```php
require_once __DIR__ . '/vendor/autoload.php';
use function App\MyList;
MyList();
```

src/MyList.php
```php
namespace App;
function MyList() {
	echo "List function";
};
```

Не забыть добавить в `composer.json` 
```json
"autoload": {
	"psr-4": {
		"App\\": "src/"
	},
	"files": [
		"src/MyList.php"
	]
}
```
секция files нужна для того чтобы загружать не класс(по умолчанию ищется класс) а только функцию. 


Кстати `namespace` может быть не только `App` (глобальный) но и любой строчкой , например  `Hexlet\Php\Runner`
В случае классов эта строчка должна соответствовать папкам внутри проекта, а случае функций , это не так важно так как мы все равно указываем файлы вручную в  `composer.json`