Docker compose - управление несколькими контейнерами сразу
Выполняются папке с файлом `docker-compose.yaml`
```bash
docker-compose build # сборка проекта из одного или нескольких контейнеров

docker-compose up -d # запуск проекта синхронно -d в фоне (detached mode)

docker-compose images # список образов которые используются в запущенных контейнерах

docker-compose ps -a # список контейнеров, ключ а по аналогии с docker ps

docker-compose exec [service name] [command] # выполнить команду в контейнере(по аналогии с командой docker)

docker-compose stop

docker-compose down # остановка проекта и удаление контейнеров

docker-compose down --rmi all --volumes # остановить и удалить контейнера(containers), образа(images) и хранилища(volums) связанные с данным docker-compose
```

Отдельно volums можно проверить и удалить вот этой командой
```bash
docker volume ls -f dangling=true # вывести список
docker volume prune # удаление
```


### Минимальный `docker-compose.yaml`
```json
version: '3'

services:
  nginx:
    build:
      context: ./nginx
      dockerfile: Dockerfile
    image: myapp/nginx
    container_name: nginx_otus
    ports:
      - "80:80"
    volumes:
       - ./code:/data/mysite.local
    networks:
      - app-network

networks:
  app-network:
    driver: bridge
```

### Разные volumes
- **Для кода** в PHP и Nginx – bind mount чтобы быстро синхронизировать папки во время разработки
```yaml
    volumes:
       - ./code:/data/mysite.local
```
- **Для БД** – named volume чтобы данные не терялись даже при пересоздании контейнеров
```yaml
#в корне
volumes: 
	db_data:

# и одновременно внутри контейнера с бд
db:
	volumes: 
		- db_data:/var/lib/mysql
```


### Ошибки
```bash
$ docker-compose up -d
time="2025-07-15T23:24:46+03:00" level=warning msg="C:\\projects\\otus\\final_work\\investor-portfolio\\docker-compose.yml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion"
unable to get image 'php:7-alpine': error during connect: Get "http://%2F%2F.%2Fpipe%2FdockerDesktopLinuxEngine/v1.48/images/php:7-alpine/json": open //./pipe/dockerDesktopLinuxEngine: The system cannot find the file specified.
```

Забыл запустить Docker-desktop