### стандартный путь для конфигов на сервере
`/etc/nginx/conf.d/`

### Перезагрузка конфигов
`nginx -t && nginx -s reload`

### Генерация сертификатов 
`https certbot -d <доменное имя>`

### Добавление базовой авторизации
   auth_basic "Private Property";
   auth_basic_user_file /etc/nginx/.htpasswd;
