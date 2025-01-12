#php/сеть #php/файлы  


## Отправка писем в PHP
```php
<?php  
  
$to = 'nobody@example.com';  
$subject = 'the subject';  
$message = 'hello';  
$headers = array(  
'From' => 'webmaster@example.com',  
'Reply-To' => 'webmaster@example.com',  
'X-Mailer' => 'PHP/' . phpversion()  
);  
  
mail($to, $subject, $message, $headers);  
  
?>
```
Остальные параметры функции mail https://www.php.net/manual/ru/function.mail. Для самой отправки надо ставить модули которые будут либо сами отправлять (phpmailer, swiftmailer, zend-mail), либо носить почту до SMTP сервера

## Вывод списка фалов и папок в директории
```php
    // Получение текущей директории
    $currentDir = getcwd();

    // Сканирование содержимого директории
    $contents = scandir($currentDir);

    // Вывод списка файлов и директорий
    echo "<h2>Папки в директории: {$currentDir}</h2>";
    echo "<ul>";

    foreach ($contents as $item) {
        // Исключение специальных папок '.' и '..'
        if ($item === '.' || $item === '..' || $item === 'index.php') {
            continue;
        }

        // Проверяем, является ли элемент директорией
        if (is_dir($item)) {
            // Делаем имя директории ссылкой
            echo "<li><a href=\"{$item}\">{$item}</a></li>";
        } else {
            echo "<li>[Файл] {$item}</li>";
        }
    }

    echo "</ul>";
```
