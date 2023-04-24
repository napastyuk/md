установка: https://laravel.com/docs/10.x/homestead#introduction
1. скачать и установить дистрибутив
2. `git clone https://github.com/laravel/homestead.git ~/Homestead`
3. ` cd ~/Homestead/`
4. `git checkout release`
5. запустить `init.bat`




```
vagrant plugin install vagrant-proxyconf

export https_proxy='http://login:password@ip:port/' 
export VAGRANT_HTTP_PROXY=${http_proxy} 
export VAGRANT_NO_PROXY="127.0.0.1"
```

VS code ssh config
```
Host Homestead
    HostName 127.0.0.1
    Port 2222
    IdentityFile /d/php/Homestead/.vagrant/machines/homestead/virtualbox/privat_key
    User vagrant
```

```
//запуск ВМ
vagrant up

//остановка ВМ
vagrant halt

//зайти в ВМ
vagrant ssh

//перезагрузить ВМ
vagrant reload

//удалить ВМ
vagrant destroy
```



#php #vargant



