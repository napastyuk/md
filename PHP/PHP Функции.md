#php/функции #рекурсия

### Пример функции
```php
$third = 0;

/**
 * Возвращает сумму двух переменных
 * @param int $first , $second - слагаемые
 * @return int сумма
 */
function name(int $first = 0 , &int $second = 0): void //функция ничего не возрашщает и работает с глобальным $second
{
	statis $acc = 0 // static сохраняет значение $acc между вызовами функции, но снаружи функции не видна
	global $third; //добавляем внешнюю переменную через ключевое слово global, т к она global она видна везде
	
	$acc = $first + $second + $third;
	echo $acc //если функцию не нужно использовать раньше , можно сразу echo
	//return $acc  
}
```
- после параметров указывается возвращаемый функций тип. Если функция ничего не возвращает то для определения типа пишут `void` 
- `&` перед second определяет, что во время вызова переменная будет не копироваться внутрь функции , а изменятся будет глобальная переменная
- после равно - значение по умолчанию, что делает параметр необязательным
- название функции и параметров - в camelCase
- если функция возвращает boolean название принято начинать с 'is'

### Передача неизвестного количества параметров
```php
function test(...$items): ?string {  //функция может вернуть строку или null
	foreach ($items as $args) {
		echo $args;
	}
}

test('one','two','three');
//либо подать массив
$arr = ['one','two','three'];
test(...$arr);
```

### Прием из функции большого количества параметров
```php
function generate() {
	//...
	return ['one','two','three']
}
list ($one,$two,$three) = generate();
//теперь в переменных результаты работы функции
```

### Контекст / Область видимости переменной
Контекст / Область видимости переменной в PHP определяется только функций в которой определена переменная.  Переменные-параметры и переменные объявленные внутри функции являются *локальными* и не видны снаружи функции. Так же переменные снаружи тоже не видны в функции.

Есть 3 способа использовать переменные внешние переменные внутри функции:
1. Передача как параметра при вызове функции. Важно что примитивы по умолчанию передаются **по значению** т е как бы копируются внутрь функции и их изменение внутри функции не влияет на внешние переменные.  Можно передавать по ссылке (чтобы изменения сохранялись глобально) , тогда в функции надо использовать `&`
```php
$number = 5;
function modifyNumber($number) {  
    echo ++$number;
}

modifyNumber($number); // Выведет 6
echo $number; // Выведет 5
```
альтернатива - написать `modifyNumber(&$number)` для захвата по ссылке

3. Передача в **анонимную** функцию через `use`
```php
$number = 5;
$closure = function() use ($number) {   
    echo ++$number; // захватывает переменную по значению
};
$closure(); // Выведет 6
echo $number; // Всё ещё 5 т к передача была по значению
```
альтернатива - написать `use (&$number)` для захвата по ссылке

3. Вызов c `global`  внутри обычной функции
```php
$number = 5; 
function modifyNumber() { 
	global $number; // доступ к глобальной переменной $number 
	echo ++$number; 
} 
modifyNumber(); // Выведет 6
echo $number; // Выведет снова 6, потому что переменная была изменена глобально
```

### Рекурсия.
Для написания рекурсивной функции нужно
1. Определить условие выхода из рекурсии (или счетчик , но он должен быть или параметром или static)
2. Дописать вызов рекурсивный вызов по другой ветке условия
3. Если это функция-аккумулятор - определить static переменную для хранения
4. Дописать остальную логику

### Возврат больше чем одного значения

#### Через массив
Массив может содержать любые данные, такие как строки, числа, объекты и т. д.
```php
function getValues() {
    $a = 10;
    $b = 20;
    return [$a, $b]; // Возвращаем массив с двумя значениями
}
list($value1, $value2) = getValues(); // Декомпозиция массива в переменные
echo $value1; // 10
echo $value2; // 20

```

#### Через ассоциативный массив
Если нужно вернуть значения с понятными именами
```php
function getValues() {
    $a = 10;
    $b = 20;
    return [
        'first_value' => $a,
        'second_value' => $b
    ];
}
$result = getValues(); // Получаем ассоциативный массив
echo $result['first_value'];  // 10
echo $result['second_value']; // 20

```

#### Через объект
Если надо вернуть данные с большой вложенностью или с инкапсулированными данными
```php
class Values {
    public $a;
    public $b;

    public function __construct($a, $b) {
        $this->a = $a;
        $this->b = $b;
    }
}

function getValues() {
    $a = 10;
    $b = 20;
    return new Values($a, $b);
}

$values = getValues();
echo $values->a; // 10
echo $values->b; // 20

```

#### Через передачу по ссылке
Функция будет просто изменять переданные значения и их не надо будет возвращать.


