```dockerfile
FROM php:8.2-fpm

WORKDIR /var/www

# Установим системные зависимости и PHP-расширения
RUN apt-get update && apt-get install -y \
    curl \
    git \
    unzip \
    libzip-dev \
    libonig-dev \
    libcurl4-openssl-dev \
    && docker-php-ext-install mbstring zip

# Копирование и установка composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
COPY composer.json composer.lock ./
RUN composer install --no-plugins --no-scripts

CMD ["php-fpm"]
```

**Системные пакеты (apt-get install):**

| Пакет                  | Зачем нужен                                                                                         |
| ---------------------- | --------------------------------------------------------------------------------------------------- |
| `curl`                 | для скачивания данных через HTTP (например, composer может использовать curl)                       |
| `git`                  | чтобы composer мог скачать зависимости из исходников через `git clone` (fallback, если нет dist)    |
| `unzip`                | чтобы composer мог распаковывать `.zip`-архивы при скачивании пакетов                               |
| `libzip-dev`           | библиотека-заголовки для сборки PHP-расширения `zip` (обязательна для `docker-php-ext-install zip`) |
| `libonig-dev`          | библиотека для поддержки регулярных выражений (необходима для `mbstring`)                           |
| `libcurl4-openssl-dev` | для поддержки `curl` внутри PHP (если понадобится расширение `curl`, но здесь пока не ставим)       |

**PHP-расширения (docker-php-ext-install):**

|Расширение|Зачем нужно|
|---|---|
|`mbstring`|для работы с многобайтовыми строками (например, UTF-8 → кириллица, emoji)|
|`zip`|чтобы PHP мог обрабатывать `.zip`-архивы (используется некоторыми библиотеками)|
