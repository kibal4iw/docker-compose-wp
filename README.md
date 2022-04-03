# Docker Compose For Local Development

Простая сборка Docker Compose для локальной разработки, например под WordPress.

### Состав

Данная сборка в себя включает

- MariaDB
- Nginx
- PHP
- phpMyAdmin

### Требования

**Docker** и **Docker Compose**

### Дефолтные настройки

Доступ к БД (MariaDB). Изменить можно в docker-compose.yml

```
user = local_db
database = local_db
password = 123456
root password = 123456
```

Доступ к phpMyAdmin через браузер

```
http://localhost:8081/
```

Доступ к php-приложению через браузер

```
http://localhost:8080/
```

### Как использовать

Склонировать репозиторий

```
git clone https://github.com/kibal4iw/docker-compose-wp.git
```

Для запуска вашего веб-сайта (или веб-приложения) просто положить файлы рядом с `docker-compose.yml`

Если вам при старте проекта нужно залить стартовые даныне в БД, откройте папку `/docker/configs/db/mariadb` и замените файл `dump.sql` на нужный вам с сохранением названия

#### Инициализация контейнеров

Перейдите в терминаре(или в IDE) в папку с `docker-compose.yml` и выполните команду для инициализация и сборки контейнеров

```
docker-compose up
```

Если все хорошо, то приложение будет доступно по адресу `http://localhost:8080/` и PhpMyAdmin `http://localhost:8081/`

В данном случае, в консоли вы будете видить все запросы к вашим контейнерам, также будут видны все ошибки вашего приложения.


#### Запуск контейнеров

Вы можете запустить контейнеры с помощью команды `up` в режиме демона (добавив `-d` в качестве аргумента) или с помощью команды `start`:

```
docker-compose start
```

### Остановка контейнеров

```
docker-compose stop
```

### Удаление контейнеров

Чтобы остановить и удалить все контейнеры, используйте команду down:

```
docker-compose down
```

Используйте `-v`, если вам нужно удалить том базы данных, который используется для сохранения БД:

```
docker-compose down -v
```

### PHP

В папке docker/configs/php есть несолько версий php.
- 7.4-apache
- 7.4-fpm

Если вам нужен nginx, то он работает в связке с 7.4-fpm

Если нужен просто apache, то использовать 7.4-apache. Заменить в docker-compose.yml

```
php:
    build: ./docker/configs/php/7.4-fpm
    volumes:
      - ./:/var/www/html/
    working_dir: /var/www/html/
    depends_on:
      - db
    links:
      - db
    container_name: proj-php
    networks:
      - proj-network
```

на

```
php:
    build: ./docker/configs/php/7.4-apache
    volumes:
      - ./:/var/www/html/
    working_dir: /var/www/html/
    depends_on:
      - db
    links:
      - db
    container_name: proj-php
    networks:
      - proj-network
    ports:
      - 8080:80
```

и удалить секцию с nginx
