Автоматизация оболочки cmd.exe

`help` - вывод список всех команд

### Как создать файл с произвольным именем из bat файла
через перенаправление `>`
`@echo same text>C:\1.txt`

### Как отключить вывод на экран команд при выполнении пакетного файла
`@echo off`

### Комментирование
однострочные
`rem Этот блок устанавливает соединение с удаленным сервером`  
`:: Этот блок проверяет дату изменения файлов`

многострочные, только через оператор безусловного перехода
```
goto start  
-------------------  
Этот пакетный файл предназначен  
для автоматизации рутинных операций,  
выполняемых ночью для синхронизации  
содержимого корпоративного ftp-сервера  
с ftp-серверами филиалов  
-------------------  
Пакетный файл написан 01/01/2004  
Последнее исправление внесено 10/02/2004  
------------------- 
И т.д.  
:start
```

### Что означает `%*` ?
при использовании команды `call` все параметры  с которыми был вызван bat будут передаватся в `call`.

### Проблема с кодировкой?
Проверить в какой кодировке файл. Добавить в файл
```
chcp
pause
```
тогда выведется в какой кодировке интерпретируется файл. 866 означает OEM 866

#windows #автоматизация #скрипты 
