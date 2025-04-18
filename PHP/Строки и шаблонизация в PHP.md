#php/типизация 

## Шаблонизация

В PHP есть 2 вида тегов для включения PHP кода.
`<?php >` - php код
и
`<?= >` - сокращенный вариант `<?php echo`

Что дает такой вариант шаблонизации

*logic.php*
```php
<?php
$text = "Это текст";
$title = "Это заголовок";
include "template.html"; //подключили html тут
?>
//либо Html можно написать тут, после закрывающей скобки. Он тоже выведется на страницу
```

*template.html*
```html
<html>
<title><?=$title?></title>
<body>
<?=$text?>
</body>
<html>
```

По аналогии с `template.html` можно включать не только страницу целиком, но и отдельные блоки

Условная шаблонизация
```html
<?php if ($x): ?>
Текст который выводится если $x == true
<?php else: ?>
Текст который выводится в другом случае
<?php endif; ?>
```


## Строки

### Длинна строки

1. **`strlen()`** - Используйте, если работаете с однобайтовыми строками или нужно знать точное количество байтов в строке.
2. **`mb_strlen()`** - Универсальная функция для подсчета символов в многобайтовых строках, подходит для большинства задач.
3. **`iconv_strlen()`** - Альтернатива `mb_strlen()`, если вы предпочитаете использовать расширение `iconv`.
4. **`grapheme_strlen()`** - Для подсчета визуальных символов, особенно если строка содержит составные графемы ( буквы с диакритическими знаками и юникод , в том числе совмещённые символы).

| Функция             | Уровень работы     | Кодировка | Особенности                                   | Пример "Привет" (UTF-8) | Пример "á" (графема) |
| ------------------- | ------------------ | --------- | --------------------------------------------- | ----------------------- | --------------------- |
| `strlen()`          | Байты              | Нет       | Не учитывает многобайтовые символы            | 12                      | 3                     |
| `mb_strlen()`       | Символы            | Да        | Учитывает многобайтовые символы               | 6                       | 2                     |
| `iconv_strlen()`    | Символы            | Да        | Аналогична `mb_strlen`, но использует `iconv` | 6                       | 2                     |
| `grapheme_strlen()` | Графемные кластеры | Да        | Учитывает сложные графемы                     | 6                       | 1                     |
P.S. Модуль `iconv`   похоже используется только для между кодировками.  
### Код по символу и наоборот

- **`chr` и `ord`** - для работы с базовым ASCII
- **`mb_chr` и `mb_ord`** - для работы с символами Unicode, включая эмодзи и национальные алфавиты. Нужно PHP моду `mbstring` 
```php
echo chr(65); // Получаем символ "A" из кода 65 (ASCII-код)
echo "\u{41}" //То же самое через Unicode codepoint escape syntax. Цифра другая потому что это UTF-8 код
echo ord('A'); // Вывод: 65, ASCII-код символа "A" 

echo mb_chr(128512, 'UTF-8'); // Вывод: 😀 (код 128512) 
echo mb_ord('😀', 'UTF-8'); // Вывод: 128512
```

### Интерполяция строк

Если использовать двойные кавычки в них можно выводить переменные

```
$var = 5;
echo = "$varяблок" //5 яблок, пробел добавился сам
echo = "{$var}яблок" //5яблок, выводится без пробела
//так же можно обращатся к элементам массива, в том числе вложенным
$arr = ['car'=>'Шевроле'];
$arr2 = [0][0] = 17;
echo = " {$arr[0][0]} яблок"

```


### Операции со строками

#### Взятие подстроки
`substr` / `mb_substr` 
```php
$rest = substr("abcdef", -3, 1); // Параметры могут быть орицательными. Возвращает «d» 
```

#### Поиск подстроки
`strpos` / `mb_strpos` / `iconv_strpos` / `grapheme_strpos`   

#### Замена подстроки
`str_replace` / `str_ireplace`

#### Очистка строки
`trim`
