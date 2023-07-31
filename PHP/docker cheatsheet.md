Все команды выполняются в папке с файлом `docker-compose.yml`

`docker-compose build` собрать проект
`docker-compose up -d`  запустить проект
`docker-compose down` остановить проект
`docker-compose logs -f [service name]` посмотреть логи сервиса
`docker-compose ps` вывести список контейнеров
`docker-compose exec [service name] [command]` выполнить команду в контейнере
`docker-compose images` список образов