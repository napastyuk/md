HTML формы в могут передавать не только текстовые значения, но и массивы. Точнее несколько текстовых элементов, могут маркироваться  как часть обчего списка и PHP интерпретирует это как массив.
Если отправить вот такую форму:
```html
    <form method="POST" action="process.php">
        <input type="text" name="names[]">
        <input type="text" name="names[]">
        <input type="text" name="names[]">
        <input type="submit" value="Отправить">
    </form>
```
То браузер отправит вот такой объект в нагрузке POST (он закодирован в URL encoding)
```
names%5B%5D=%D0%BF%D0%B5%D1%80%D0%B2%D1%8B%D0%B9&names%5B%5D=%D0%B2%D1%82%D0%BE%D1%80%D0%BE%D0%B9&names%5B%5D=%D1%82%D1%80%D0%B5%D1%82%D0%B8%D0%B9

//что расшифровывается как
names[]   первый
names[]   второй
names[]   третий
```
И PHP сразу в $POST преобразует это в массив
```php
    [names] => Array
        (
            [0] => первый
            [1] => второй
            [2] => третий
        )
```
Важные моменты чтобы все заработало:
- имя у html полей должно быть одинаковым. Это будет именем массива. 
- сразу после имени без пробела должны стоять `[]`
- скобочки можно оставить пустыми тогда PHP соберёт обычный массив c нумерацией от 0.
- если в скобках что-то писать, то PHP соберёт ассоцитивный массив. То что было в скобочках станет ключом. Если в ключах будут пропуски PHP они заполнятся цифрами от 0.

C чекбоксами тоже можно
```html
<label><input type="checkbox" name="colors[]" value="Красный"> Красный</label><br>
<label><input type="checkbox" name="colors[]" value="Зелёный"> Зелёный</label><br>
<label><input type="checkbox" name="colors[]" value="Синий"> Синий</label><br>
```
Браузер отправит
```
colors[]  Красный
colors[]  Синий
```
PHP соберёт массив
```
[colors] => Array
        (
            [0] => Красный
            [1] => Синий
        )
```
Важные моменты:
- если чекбоксы ставить не подряд, массив все равно придёт подряд. Т. е. не поставленная галочка `зелёный` в итоговом массиве никак не отразится. 
- значение отправится именно из атрибута value, а не из тега label
- `type="checkbox"` можно поменять на `type="radio"` в этом случае будет все то же самое, только в итоговом массиве всегда будет одни элемент с индексом 0
- все остальные input types отправляю просто текстовое значение из js свойства value. Если их объединять в массив, то отправляют массив строк.
- если оставить текстовое поле пустым, оно все равно окажется в итоговом массиве, но со значением пустой строки.
- поля можно добавлять через js
- весь пользовательский ввод браузером не экранируется, поэтому на стороне 
```html
    <form method="POST" action="process.php">
        <label>Имя: <input
                type="text"
                name="user[name]"></label><br>
        <label>Email: <input
                type="email"
                name="user[email]"></label><br>
        <label>Число: <input
                type="number"
                name="user[age]"></label><br>
        <label>Диапазон: <input
                type="range"
                min="0"
                max="200"
                name="user[height]"></label><br>
        <label>Цвет: <input
                type="color"
                value="#f6b73c"
                name="user[color]"/></label><br>
        <label>Дата: <input
                type="datetime-local"
                value="2018-06-12T19:30"
                name="user[date-birth]"/></label><br>
        <input type="submit" value="Отправить">
    </form>
```

```php
[user] => Array
	(
		[name] => ivan
		[email] => ivan@email.com
		[age] =>                  //незаполнененое значение пришло пустым
		[height] => 100
		[color] => #f6b73c
		[date-birth] => 2018-06-12T19:30
	)
```

Весь пользовательский ввод браузером не экранируется, поэтому на стороне php обязательно использовать htmlspecialchars()
```php
if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    $names = $_POST['names'];
    
    foreach ($names as $index => $name) {
        echo "Имя " . ($index + 1) . ": " . htmlspecialchars($name) . "<br>";
    }
}
```

Массивы могут быть вложенными
```html
<h3>Пользователь 1</h3>
<label>Имя: <input type="text" name="users[0][name]"></label><br>
<label>Возраст: <input type="number" name="users[0][age]"></label><br><br>

<h3>Пользователь 2</h3>
<label>Имя: <input type="text" name="users[1][name]"></label><br>
<label>Возраст: <input type="number" name="users[1][age]"></label><br><br>
```

```php
[users] => Array
(
	[0] => Array
		(
			[name] => цукц
			[age] => 12
		)
	[1] => Array
		(
			[name] => фыва
			[age] => 45
		)
)
```

Уровень вложенности может быть любой  но такие массивы сложно разбирать, потому что надо проверять каждый уровень на существование ( `isset()` )  и на пустоту ( `empty()` ) . Гораздо удобнее обработку сделать на клиенте средствами js и отправлять JSON через `JSON.stringify()` и соотв. принимать через `json_decode()`

