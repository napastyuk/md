Ссылка на документацию
https://wordpress.org/support/article/changing-file-permissions/

```
chown www-data:www-data -R *
find . -type d -exec chmod 755 {} \;
find . -type f -exec chmod 644 {} \;
chmod 440 wp-config.php

#если склонил не под тем пользователем, то дополнительно 
chown www-data:www-data .gitignore 
chown www-data:www-data .htaccess 
chown www-data:www-data -R .git

для установки нужен find . -type d -exec chmod 767 {} \;
```

Вариант если не хватате стандартных разрешений
https://wordpress.org/support/article/changing-file-permissions/#using-the-command-line