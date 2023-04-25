Vagrant не является витуальной машиной, но предоставляет удобный средства по их управления. Воспроизводимый набор элементов рабочего окружения, пакетов настроек и пр. который запустится на любой ОС. В документации этот набор называется vagrant вox.  Внутри vagrant вox не сами программы, а только инструкции по их развертке. 

Все команды Vagrant выполняются только в каталоге с Vagrantfile
```
vagrant //показать встроенную справку
```

### Создание виртуальной машины
```
vagrant init // инициализация из файла Vagrantfile и образа указанного там

vagrant init <boxpath> // инициализация из каталога Vagrant
```

### Запуск виртуальной машины
```
vagrant up //запуск и настройка ВМ
vagrant halt //выключение ВМ

vagrant reload //тоже самое что и последовательный up и halt

vagrant provision //заново перенастроить ВМ из конфига

vagrant suspend //приостановка ВМ(с сохранением состояния)
vagrant resume //возобновление ВМ

vagrant ssh  //зайти внутрь ВМ
```

### Управление vagrant box
```
vagrant box list //список установленных коробок 

vagrant status //вывод статус текущей машины
vagrant global-status //стус всех машин

vagrant box add <name> <url> //скачать коробку и программы описанные в нем
vagrant box outdated //проверить и установить обновления
vagrant box remove <name> //удалить коробку
```

#vargant #cheatsheet 