### Введение
`Dockerfile` -  набор инструкций для сборки контейнера. Запуск сборки по команде:
```bash
docker build -t "some_container_name" . #Точка в конце команды - это указание что `Dockerfile` надо искать в текущей папке
```

Важно! По `build` собрался только образ контейнера.  Это только заготовка на основе которой можно быстро запускать один или несколько контейнеров. 
Физически он (для windows 10) хранится в недрах wsl. Список уже собранных образов можно посмотреть по команде
```bash
docker images
```
Физический пусть для windows 10 c wsl2 `\\wsl.localhost\docker-desktop-data\version-pack-data\community\docker\image\overlay2`

После сборки контейнер можно запускать сколько нужно раз.
```bash
docker run "some_container_name"
```


