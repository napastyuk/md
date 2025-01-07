#php/файлы #php/сеть 

На  примере формы для загрузки аватарки. На клиенте:

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
	$new_path = __DIR__ . '/' . $filename; //новый путь это папка с именем картинки , которая находится там же где и выполняемый скрипт
	move_uploaded_file($current_path, $new_path); //перемщаем из временной папки в постоянную
?>
```