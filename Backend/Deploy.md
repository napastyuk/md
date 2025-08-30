Деплой github проекта на vds/vps
0. Подключаемся
```
ssh username@your-vds-ip
```

1. Установи Docker и Docker Compose на VDS
```shell
# Установи Docker
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh

# Установи docker-compose plugin
sudo apt install docker-compose-plugin -y

# проверка
docker -v
docker compose version
```

2. Если сервер только развернутый надо настроить там ssh ключи
```shell
ssh-keygen -t ed25519 -C "your-email@example.com"

# Пароль можешь задать или оставить пустым — как тебе удобнее
# Проверяем что получилось, и у нас теперь есть  ключи

cd ~/.ssh
ls -la

#что-нибудь такое
-rw------- 1 root root  411 Jul 27 15:41 id_ed25519
-rw-r--r-- 1 root root  101 Jul 27 15:41 id_ed25519.pub

# открываем ПУБЛИЧНЫЙ (.pub) ключ , его содержимое нам понадобится далее
cat ~/.ssh/id_ed25519.pub
```

3. Добавляем ключ в Github
- Зайди в GitHub → [Settings → SSH and GPG keys](https://github.com/settings/keys)
- Нажми **"New SSH key"**
- Назови ключ, например: `VPS Server`
- Вставь туда содержимое файла `id_ed25519.pub`
- Сохрани и проверь доступ c сервера на github
```shell
ssh -T git@github.com

# Hi napastyuk! You've successfully authenticated, but GitHub does not provide shell access.
```

4. Если проект в публичной репе, копировать можно напрямую с github
```shell
sudo apt update
sudo apt install git -y

# проверка
git -v
```

3. Копирование проекта на сервер
```shell
git clone https://github.com/твой-username/твой-проект.git
cd твой-проект
```

4. Создаем или копируем .env если он используется в проекте
```
cp .env.example .env
# или сразу
nano .env
```

5. Запускаем развертывание
```shell
docker compose up -d
```

6. Проверка что все развернулось и 
```shell
# проверка что контейнера запустились
docker ps

# просмотр логов контейнера
docker compose logs -f app

#проверка базы
docker compose exec db psql -U admin -d mydatabase -c '\dt'
```

7. Если понадобилось внести правки по быстрому
```
# например в файле docker-compose.yaml
scp docker-compose.yaml root@195.133.194.43:/root/investor-portfolio/docker-compose.yaml

или всю папку целиком
scp -r ./ root@195.133.194.43:/root/investor-portfolio/
```

Либо через git