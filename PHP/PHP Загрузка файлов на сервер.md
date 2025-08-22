#php/файлы #php/сеть 
## Пример формы для загрузки аватарки. 

На клиенте:
```html
<form 
	  name="file_upload" 
	  method="POST" 
	  action="form.php" 
	  enctype="multipart/form-data"> 
	  
	  <label>Ваш аватар: 
	  <input type="file" name="avatar"></label> 
	  <input type="submit" name="send" value="Отправить файл"> 
</form>
```

На стороне сервера:
```php
<?php 
	$current_path = $_FILES['avatar']['tmp_name']; //сначала все загружаемые файлы складываются в $_FILES 
	$filename = $_FILES['avatar']['name'];  //достанем имя загруженного файла
	//так же доступны
	//$_FILES['avatar']['size'] размер в байтах
	//$_FILES['avatar']['type'] MIME тип файла
	$new_path = __DIR__ . '/' . $filename; //новый путь это папка с именем картинки , которая находится там же где и выполняемый скрипт
	move_uploaded_file($current_path, $new_path); //перемщаем из временной папки в постоянную

?>
```


## Этапы проверки файла на размер:

### 1. В html Добавить
```html
<form>
<input type="hidden" name="MAX_FILE_SIZE" value="4194304" />
</form>
```
Правда важный момент, что при таком ограничении, файл все таки начнёт загружаться и прервется по достижении максимума

### 2. Параметры в файле конфигурации `php.ini`
`upload_max_filesize` - Максимальный размер одного загружаемого файла
`post_max_size` - Максимальный размер всех данных, переданных через POST-запрос (включая файлы)
`max_file_uploads` - Максимальное количество файлов, которые могут быть загружены за один раз

### 3. Проверка на уровне PHP
```php
if ($_FILES['uploaded_file']['error'] === UPLOAD_ERR_OK) {
    $maxSize = 5 * 1024 * 1024; // Максимум 5 МБ (в байтах)
    $fileSize = $_FILES['uploaded_file']['size'];

    if ($fileSize > $maxSize) {
        echo "Файл слишком большой. Допустимый размер: 5 МБ.";
        unlink($_FILES['uploaded_file']['tmp_name']); // Удаляем временный файл
    } else {
        // Обрабатываем файл, если он подходит
        $destination = __DIR__ . '/uploads/' . basename($_FILES['uploaded_file']['name']);
        if (move_uploaded_file($_FILES['uploaded_file']['tmp_name'], $destination)) {
            echo "Файл успешно загружен.";
        } else {
            echo "Ошибка при перемещении файла.";
        }
    }
} else {
    echo "Ошибка загрузки: " . $_FILES['uploaded_file']['error'];
}
```

### Возможные ошибки в массиве `$_FILES['uploaded_file']['error']` 
- `UPLOAD_ERR_INI_SIZE`: Файл превышает `upload_max_filesize`.
- `UPLOAD_ERR_FORM_SIZE` : Файл превышает `MAX_FILE_SIZE`, заданный в форме.
- `UPLOAD_ERR_PARTIAL`: Файл загружен частично.
- `UPLOAD_ERR_NO_FILE`: Файл не был загружен.