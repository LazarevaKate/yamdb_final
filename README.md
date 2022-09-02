# api_yamdb
api_yamdb

Опиание проекта.

Проет был создан для практики работы в команде. 

### Запустить проект в контейнере

1. Скопировать проект и перейти в корневую директорию:
```
git clone git@github.com:earlinn/infra_sp2.git
cd infra_sp2
```
2. Перейдите в папку infra_sp2/infra и создайте там файл .env с переменными окружения, нужными для работы приложения. 
```
cd infra/

Пример .env-файла:

DB_ENGINE=django.db.backends.postgresql # указываем, что работаем с postgresql
DB_NAME=postgres # имя базы данных
POSTGRES_USER=postgres # логин для подключения к базе данных
POSTGRES_PASSWORD=postgres # пароль для подключения к БД (установите свой)
DB_HOST=db # название сервиса (контейнера)
DB_PORT=5432 # порт для подключения к БД 
```
3. Запускаем docker-compose:
```
docker-compose up -d
```
4. Будут созданы и запущены в фоновом режиме необходимые для работы приложения контейнеры (db, web, nginx). Заполнить базу тестовыми файлами можно при помощи команды:
```
docker-compose exec web python manage.py loaddata fixtures.json
```
6. Затем нужно внутри контейнера web выполнить миграции, создать суперпользователя и собрать статику:
```
docker-compose exec web python manage.py migrate
docker-compose exec web python manage.py createsuperuser
docker-compose exec web python manage.py collectstatic --no-input 
```
5. Теперь проект доступен по адресу http://localhost/.

### В проекте предоставлены следующие возможности:

Подробная документация: http://127.0.0.1:8000/redoc/

Просмотр списка объектов:

GET http://127.0.0.1:8000/api/v1/titles/

Создание нового объекта обсуждения (доступно только админу, суперюзеру):

POST http://127.0.0.1:8000/api/v1/titles/

Просмотр конкретного объекта:

GET http://127.0.0.1:8000/api/v1/titles/1/

Изменение/удаление конкретного объекта (доступно админу, суперюзеру):

PATCH/DELETE http://127.0.0.1:8000/api/v1/titles/1/

Просмотр списка отзывов конкретного объекта (доступно всем):

GET http://127.0.0.1:8000/api/v1/titles/1/reviews/

...

Изменение/удаление отзыва конкретного объекта (доступно автору комментария, модератору, админу, суперюзеру):

PATCH/DELETE http://127.0.0.1:8000/api/v1/titles/1/reviews/1/

...

Просмотр списка комментариев к отдельному отзыву (доступно всем):

GET http://127.0.0.1:8000/api/v1/titles/1/reviews/1/comments/

...

Над проектом работали:

Антон Искров

Антон Третьяков

Екатерина Лазарева