#php/файлы  

Функции для работы с директориями.

### Прочитать содержимое папки
```php
$dir = scandir('mydirectory'); //возвращает массив с папаками и файлами
```
Проверить содержимое папки можно циклом с помощью
```php
is_dir('mydirectory') //true - mydirectory это папка
is_file('myfile') //true - myfile это папка 
```
Обе функции принимают как абсолютный , так и относительный путь. Относительный путь рассчитывается от текущей папки.
В цикле на не забыть про виртуальные директории
`.` - это ссылка на текущую директорию
`..` - это ссылка на родительскую категорию

### Текущая папка
В PHP папка запуска скрипта является текущей.  Текущую папку можно сменить командой 
```php
chdir('newdir')
```
Проверить текущую рабочую папку
```php
getcwd() //вернет строчку с полным путём от корня
```
