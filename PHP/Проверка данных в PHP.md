Проверка на null
```php
$some = null;
//читается как если $some равен null, то присваивай не null, а default
$action = $some ?? 'default' 

```

Проверка на пустоту (переменная создана но не инициализирована)
```php
empty($null) /*вернёт false только если переменная пустая по смыслу и равна одному из:
unset()
""
0
"0"
null
array()
false
*/
```

Проверка на существование (переменная не создана)
```php
isset($nonSet) //вернёт false только если переменная null или unset()
//либо так
$newVar = $oldVar ?? 'default_value';
```

Мнемоническое правило: `isset()` проверяет есть ли у тебя кошелек, а `empty()` проверяет есть ли кошелек и лежит ли что-то в нем.

Проверка на тип данных
```php
gettype($value) //возвращает строку с типом https://www.php.net/manual/ru/function.gettype.php
```

#php/типизация 