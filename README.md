# Примеры реализации API
Данный репозиторий содержит примеры реализации API для курса СУБД в рамках ["Технопарка"](https://park.mail.ru/pages/index/).

Цель данного репозитория: уменьшить входной порог при реализации курсового проекта (https://github.com/mailcourses/technopark-dbms-init).

## Немного о примерах кода
Каждый пример удовлетворяем следующим требованиям:

 * Он реализует API, описанное в common/swagger.yml;
 * Код генерируемый из Swagger-схемы исключён из репозитория;
 * При доступе к корневой странице отображается Swagger UI для ручной проверки API;
 * Написан файл для формирования Docker-контейнера, который разворачивает реализованный сервис вместе с PostgreSQL 9.5.

## Состав Docker-контейнеров
Docker контейнера организованы по следующему принципу:

 * Приложение:
   * использует и объявляет порт 5000 (http);
 * PostgreSQL:
   * использует и объявляет порт 5342 (http);
   * директории `/etc/postgresql`, `/var/log/postgresql`, `/var/lib/postgresql` объявлены как VOLUME для возможности сохранения БД.

## Как собрать и запустить контейнер
Для сборки контейнера можно выполнить команду вида:
```bash
docker build -t technopark-dbms-init -f Dockerfile.java-spring https://github.com/mailcourses/technopark-dbms-init.git
```
Или команды:
```bash
git clone https://github.com/mailcourses/technopark-dbms-init.git technopark-dbms-init
cd technopark-dbms-init/
docker build -t technopark-dbms-init -f Dockerfile.java-spring .
```

После этого будет создан Docker-образ с именем `technopark-dbms-init` (опция `-t`).

Запустить ранее собранный контейнер можно командой вида:
```bash
docker run -p 5000:5000 --name hello technopark-dbms-init
```
После этого можно получить доступ к запущенному в контейнере приложению по URL: http://localhost:5000/

Получить список запущенных контейнеров можно командой:
```bash
docker ps
```

Остановить контейнер можно командой:
```bash
docker kill hello
```
