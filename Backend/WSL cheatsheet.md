Хранение файлов
```
\\wsl.localhost\Ubuntu\home\ilya\speech-analytic\portal\front
```

Другие команды:
```cmd
wsl --list --online   # список дистрибутивов Linux, доступных через windows store
wsl -l -o   

wsl --list --verbose  # список установленных дистрибутивов
#удобно чтобы проверить что версии wsl переключились на v2

wsl --set-default <Distribution Name>   #  установка дистрибутива по умолчанию

wsl --update    # обновление WSL

wsl --shutdown   #принудителььное выключение

wsl --status   # состояние WSL
#Пример ответа
Распределение по умолчанию: Ubuntu-20.04
Версия по умолчанию: 2

wsl --version   #версии WSL
#Пример ответа
Версия WSL: 2.4.13.0
Версия ядра: 5.15.167.4-1
Версия WSLg: 1.0.65
Версия MSRDC: 1.2.5716
Версия Direct3D: 1.611.1-81528511
Версия DXCore: 10.0.26100.1-240331-1435.ge-release
Версия Windows: 10.0.26100.3775
```


Запуск WSL2 GUI приложений
```bash
sudo apt update && sudo apt upgrade

#установка текстового редактора gnome
sudo snap install gnome-text-editor

#запуск
gnome-text-editor ~/.bashrc

#установка firefox
sudo apt install firefox

#запуск
firefox
```


[Остальная дока](https://learn.microsoft.com/ru-ru/windows/wsl/basic-commands)