Чтобы запустить локально полноценную виртуалку с PHP нам нужно:
1. Программа которая управляет виртуальными машинами. Скачиваем и устанавливаем  [VirtualBox](https://www.virtualbox.org/)
2. Далее нам нужна Linux OC с набором нужных пакетов, идентичных тех которые будут на сервере. Чтобы не устанавливать все вручную обычно пользуются готовыми образами, где все уже настроено. Плюс было бы неплохо получить версионирование не только кода, но и набора пакетов в внутри виртуальной ОС. Всю эту магию делает [Vagrant](https://developer.hashicorp.com/vagrant/downloads?product_intent=vagrant), скачиваем и устанавливаем. 
3. У Вагранта в облаке много разных образов, разной степени проработаности. Для обучения обычно используют образ для Laravel - [Homestead](https://app.vagrantup.com/laravel/boxes/homestead) (пока не скачиваем), в котором уже накручена автоматизация по первоначальной настроке. На вход Homested надо подать только минимальный конфиг в файле Homestead.yaml. Есть 2 способа запуска скрипта Homestead. Через composer и через init-скрипт.  Composer на хостовую ОС нет смысла устанавливать, он будет у нас в виртуалке.  При использовании init-скрипта, все последующие операции с виртуалкой надо будет запускать в папке самого homestead, поэтому сделаем путь покороче.
4. Итого нам нужно начать со Homestead. Он распространяется как набор скриптов на github. Идем и скачиваем: 
```cmd
git clone https://github.com/laravel/homestead.git hs
cd hs
git checkout release
```
5. Запускаем Homestead, чтобы получить конфиг для Vagrant
```cmd
init.bat
```
6. Теперь у нас есть 2 файла которые определют окружение проекта: `Homestead.yaml` и `Vagrantfile`.  Пропишем в  Homestead.yaml пути где будет лежать код проекта
```yaml
folders:
    - map: D:\php\code
      to: /home/vagrant/code
      
sites:
    - map: homestead.test
      to: /home/vagrant/code/public
```
Дока по опциям https://laravel.com/docs/10.x/homestead#configuring-homestead
7. Теперь можно запускать генерацию виртуальной машины. Первый шаг это скачивание из образа OC из облака Vagrant поэтому сначала стоит разобратся с VPN, который будет заворачивать весь системный трафик, не только браузер. Если есть прокси с хорошей скоростью можно поставить на Vagrant плагин для прокси
```bash
vagrant plugin install vagrant-proxyconf
export https_proxy='http://login:password@ip:port/' 
export VAGRANT_HTTP_PROXY=${http_proxy} 
export VAGRANT_NO_PROXY="127.0.0.1"
```
Переменные с адресом прокси будут жить только до закрытия консоли, но это не страшно, запуск собранной виртуалки без доступа к облаку проходит нормально
```
//запуск ВМ, если ее еще нет, скачается и соберётся при первом запуске команы
vagrant up
```
8. Еще раз про что произойдет после запуска команы `up` 

TODO: расписать про версионирование и запуск образов вместо самой виртуалки


9. Подключение к запущенной виртуалке через VS code, плагин Remote SSH
```yaml
Host Homestead
    HostName 127.0.0.1
    Port 2222
    IdentityFile /d/php/Homestead/.vagrant/machines/homestead/virtualbox/privat_key
    User vagrant
```
10. Прочие команы для Vagrant
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

//удалить ВМ по имени и версии
vagrant box remove laravel/homestead --box-version=0
```

#php #vargant