# Docker Compose For Local Development

Простая сборка Docker Compose для локальной разработки, например под WordPress

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
http://localhost:8082/
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

Скопируйте ваше приложение в папку /web/

Если вам при старте проекта нужно залить стартовые даныне в БД, откройте папку `/docker/db/mariadb` и замените файл `dump.sql` на нужный вам с сохранением названия

#### Инициализация контейнеров  

Перейдите в терминаре(или в IDE) в папку с `docker-compose.yml` и выполните команду для инициализация и сборки контейнеров

```
docker-compose up
```

Если все хорошо, то приложение будет доступно по адресу `http://localhost:8080/`

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