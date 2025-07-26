#php/основы

## Условия

```php
if ($var == "один") { 
	//делаем одно 
} elseif {
	//делаем другое
} else { 
	//делаем третье
}
```

Так же есть сокращенный синтаксис, без скобочек. Положительная ветка начинается с `:`  и заканчивается `endif`
```php
if ($a > $b):
    echo "a больше b";
endif;
```

## Циклы

**while и do while**
индекс обязателен
```php
$i = 1;
while ($i <= 10) {
    echo $i++;
};
```

```php
$i=1;
do {
	echo $i++;
} while($i<=10);
```

**for**
```php
//for (инициализирующее_выражение;проверка_условия;инкремент_или_другая_операция) {
//Тело цикла
//}

for($i=1; $i<=10;  $i++) {
	echo $i;
}
```

`break` - выход из цикла целиком;
`continue` - завершение текущей итерации цикла;

Для обхода массивов можно использовать forEach
```php
foreach ($course as $key => $value) {
    print_r("{$key}: {$value}");
}
```
или сокращенно
```php
foreach ($course as $value) {
    print_r($value);
}
```
для вложенных массивов можно использовать вместе с `list()` 
```php
//для индексированных массиво
$array = [  
	[1, 2],  
	[3, 4],  
];  
  
foreach ($array as list($a, $b)) {  
	// Переменная $a содержит первый элемент вложенного массива, а переменная $b - второй.  
	echo "A: $a; B: $b\n";  
}


//аналогичная конструкция для ассоциативных массивов
$links = [
    ['url' => 'https://google.com', 'name' => 'Google'],
    ['url' => 'https://yandex.com', 'name' => 'Yandex'],
    ['url' => 'https://bingo.com', 'name' => 'Bingo']
];

foreach ($links as ['url'=>$url, 'name'=> $name]) {
    echo "<div><a href='$url'>$name</a></div>";
};
```