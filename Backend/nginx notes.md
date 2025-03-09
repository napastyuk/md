### стандартный путь для конфигов на сервере
`/etc/nginx/conf.d/`

### Стандартный путь для логов
```
Access logs (/var/log/nginx/access.log)
Error logs (/var/log/nginx/error.log)
```


### Проверка корректности конфигов
`nginx -s reload`
### Перезагрузка конфигов
`nginx -t && nginx -s reload`
### Генерация сертификатов 
`https certbot -d <доменное имя>`
### Добавление базовой авторизации
```
auth_basic "Private Property";
auth_basic_user_file /etc/nginx/.htpasswd;
```


#сети #devops #nginx  #cheatsheet 
