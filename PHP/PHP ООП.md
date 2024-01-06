---
tags:
  - ооп
  - oop
---

Класс - это прототип/чертёж/образ для объекта

Объект создается из класса с помощью оператора `new`
`$objA = new ClassA`

Для более удобного создания используется функция конструктор , которая вызывается всегда при `new`
```php
class One 
{
    public function __constructor() {
    }
}
```
Конструктор может использовать другие функции и переменные, их помещают `static` чтобы они были недоступны в готовом объекте 
```php
class One  {
	privat static $secret = "123";
	privat static function doIt() {
	}
}
```

## Область видимости свойств / методов / констант

`public` - доступ разрешён отовсюду 
`protected` - разрешён самому классу и его наследникам
`private` - доступ только внутри самого класса


Вызов метода класса
`classA::methodB()`

Вызов метода объекта
`objectA->methodB()`

### Пространство имён
Создание
```php
/*person.php*/
namespace base

class Person
{
}
```

Обращение
```php
include "person.php";
$tom = new \base\Person()
//или
use \base\classes\Person as User
```

Пространства имён могут быть вложенными 

Подключать можно не только классы, но и константы и функции
```php
use \base\classes\Person;
use const \base\classes\adminName;
use function \base\classes\printPerson;

```
