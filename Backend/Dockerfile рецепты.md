Минимальный `Dockerfile`
```
FROM alpine
```

Минимальный `docker-compose.yaml`
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