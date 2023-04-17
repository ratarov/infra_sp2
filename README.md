## API for YaMDB
### Описание
**Командный проект. API для сервиса отзывов YaMDB**
### Используемые технологии:
![image](https://img.shields.io/badge/Python-FFD43B?style=for-the-badge&logo=python&logoColor=blue)
![image](https://img.shields.io/badge/SQLite-07405E?style=for-the-badge&logo=sqlite&logoColor=white)
![image](https://img.shields.io/badge/Django-092E20?style=for-the-badge&logo=django&logoColor=green)
![image](https://img.shields.io/badge/django%20rest-ff1709?style=for-the-badge&logo=django&logoColor=white)
![image](https://img.shields.io/badge/VSCode-0078D4?style=for-the-badge&logo=visual%20studio%20code&logoColor=white)
![image](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)
![image](https://img.shields.io/badge/Docker-2CA5E0?style=for-the-badge&logo=docker&logoColor=white)
![image](https://img.shields.io/badge/Nginx-009639?style=for-the-badge&logo=nginx&logoColor=white)

### Установка
**Запуск проекта из контейнера Docker:**
```
Клонируйте репозиторий:
git clone https://github.com/ratarov/infra_sp2
```
```
Убедитесь, что у Вас установлен Docker версии не ниже 19.03.0
docker --version
```
```
Перейдите в директорию с файлом docker-compose.yaml и запустите сборку
cd infra_sp2/infra
docker-compose up -d
Для пересборки контейнера используйте
docker-compose up -d --build
```
```
Создайте и примените миграции, создайте суперпользователя и соберите статику
docker-compose exec web python manage.py makemigrations reviews
docker-compose exec web python manage.py migrate
docker-compose exec web python manage.py createsuperuser
docker-compose exec web python manage.py collectstatic --no-input
```
**Импорт данных в базу данных:**
```
docker-compose exec web python manage.py loaddata fixtures.json
или
docker-compose exec web python manage.py fill_db_from_csv
```
**Шаблон наполнения файла .env**
```
DB_ENGINE=django.db.backends.postgresql
DB_NAME=postgres
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
DB_HOST=db
DB_PORT=5432
```
### Документация API:
```
Все эндпоинты, а так же их параметры доступны по адресу: 
http://127.0.0.1:8000/redoc/
```

### Примеры запросов к API:
```
POST api/v1/categories/
http://127.0.0.1:8000/api/v1/categories/

Payload
{
  "name": "string",
  "slug": "string"
}

Response sample
201
{
  "name": "string",
  "slug": "string"
}

Response sample
400
{
  "field_name": [
    "string"
  ]
}
```
```
POST api/v1/auth/signup/
http://127.0.0.1:8000/api/v1/auth/signup/


Payload
{
  "email": "user@example.com",
  "username": "string"
}

Response sample
200
{
  "email": "string",
  "username": "string"
}

Response sample
400
{
  "field_name": [
    "string"
  ]
}

```
```
PATCH api/v1/users/{username}/
http://127.0.0.1:8000/api/v1/users/{username}/

Payload
{
  "username": "string",
  "email": "user@example.com",
  "first_name": "string",
  "last_name": "string",
  "bio": "string",
  "role": "user"
}

Response sample
200
{
  "username": "string",
  "email": "user@example.com",
  "first_name": "string",
  "last_name": "string",
  "bio": "string",
  "role": "user"
}

Response sample
400
{
  "field_name": [
    "string"
  ]
}
```
##### Авторы:
Авторизация и аутентификация, права доступа, пользователи - Дмитрий Опушнев.
https://github.com/DmitriyOpushnev/

Модели, view для произведений, категорий, жанров, импорт данных из csv файлов - Руслан Атаров.
https://github.com/ratarov

Модели, view для отзывов, комментариев, рейтингов - Андрей Кирилов.
https://github.com/Oktut