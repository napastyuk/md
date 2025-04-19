## 1. Запуск на один раз из cmd
```bash
mkdir C:\docker\postgres_data  # создаем папку в которой БД будет хранить фалы

docker run --name postgres-container `  
  -e POSTGRES_USER=admin `
  -e POSTGRES_PASSWORD=secret `
  -e POSTGRES_DB=mydb `
  -v C:\docker\postgres_data:/var/lib/postgresql/data `
  -p 5432:5432 `
  -d postgres   # скачиваем и запускаем образ

docker ps  # проверяем что все нормально скачалось и запустилось

psql -h localhost -U admin -d mydb  # подключаемся к базе

docker stop postgres-container #остановить конейнер

docker start postgres-container #запустить снова

docker rm -f postgres-container #удалить конейнер

Remove-Item -Recurse -Force C:\docker\postgres_data #удалить данные
```


## 2. Запуск через docker file
Много телодвижений но большая гибкость
Dockerfile
```Dockerfile
FROM postgres:16

ENV POSTGRES_USER=admin
ENV POSTGRES_PASSWORD=secret
ENV POSTGRES_DB=mydb

# Копируем SQL-скрипт, если нужен
COPY init.sql /docker-entrypoint-initdb.d/
```

init.sql
```sql
CREATE TABLE IF NOT EXISTS users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(100) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

сборка
```bash
docker build -t custom-postgres .
```

запуск
```
docker run --name pg-dockerfile-container `
  -v C:\docker\pg_data:/var/lib/postgresql/data `
  -p 5432:5432 `
  -d custom-postgres

```


## 3. Через Docker-compose
Самый удобный. Создаем файлик docker-compose и запускаем его через `docker-compose up -d` . И все работает.
```yaml
services:
  postgres:
    image: postgres
    container_name: postgres_container
    environment:
      POSTGRES_USER: admin
      POSTGRES_PASSWORD: secret
      POSTGRES_DB: mydb
    ports:
      - "5432:5432"
    volumes:
      - pg_data:/var/lib/postgresql/data

volumes:
  pg_data:
```

Важный момент! Подключатся к такому контейнеру из под windows очень неудобно. Потому что порт 5432 может быть уже занят postgres, которая запущена внутри WSL. Погасить WSL не выйдет, потому что сам docker работает на WSL. Нужно или процесс postgress внутри WSL-Ubuntu или гасить именно Ubuntu без WSL или просто прописать в конфиге выше порты `"6432:5432"` и подключается к `6432`.  Это будет именно порт наружу. Для соседних контейнерах порт по прежнему будет `5432`


Полезные команды
```
docker-compose up -d  #запуск

docker-compose down  #остановка
docker-compose down -v #остановка и удаление volume

docker-compose restart  #перезапуск

docker-compose logs -f  #просмотр логов
```

подробнее про [Docker compose](Docker%20compose.md)