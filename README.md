#  Проект: Kittygram
Kittygram — платформа для обмена фотографиями домашних животных, для настоящих любителей кошек. Здесь пользователи могут делиться фотографиями своих пушистых друзей и наслаждаться снимками котов, добавленными другими участниками сообщества. Пользователь заполняет информацию о его имени, годе рождения и цвете. Также есть возможность загрузить фотографию питомца и указать его достижения.

[![Main Kittygram workflow](https://github.com/kostoyanskaya/kittygram_final/actions/workflows/main.yml/badge.svg?branch=main)](https://github.com/kostoyanskaya/kittygram_final/actions/workflows/main.yml)

### Основные возможности:
- Создание профиля питомца: Пользователи могут добавить информацию о своих кошках, включая имя, год рождения и цвет.
- Загрузка фотографий: Возможность делиться любимыми снимками своих питомцев с другими пользователями.
- Просмотр фотографий: Пользователи могут просматривать фотографии кошек, загруженные другими участниками.
- Достижения питомцев: Возможность указывать достижения питомцев из списка или добавлять новые, если необходимо.
- Авторизация: Защищенный доступ к функциям платформы для зарегистрированных пользователей.


### В проекте используются следующие технологии и библиотеки:

- Django - основной фреймворк для разработки веб-приложений.
- Django REST Framework - для построения API.
- Djoser - для управления аутентификацией и регистрацией пользователей.
- Webcolors - для работы с цветами.
- Pillow - библиотека для обработки изображений.
- pytest - для тестирования.
- PostgreSQL - в качестве базы данных.
- Gunicorn - WSGI HTTP сервер для запуска приложения.


## Установка проекта на удаленном сервере:

1. Выполнить вход на удаленный сервер.

2. Выполните на сервере команды для установки Docker и Docker Compose для Linux

```
sudo apt update
sudo apt install curl
curl -fSL https://get.docker.com -o get-docker.sh
sudo sh ./get-docker.sh
sudo apt install docker-compose-plugin 
```

3. Создайте папку kittygram

```
sudo mkdir kittygram
```

4. Переход в директорию kittygram

```
cd kittygram/
```

5. Нужно создать фаил docker-compose.production.yml и скопировать  содержимое 
docker-compose.production.yml проекта

```
sudo touch docker-compose.production.yml
sudo nano docker-compose.production.yml
```

6. Нужно создать фаил .env

```
sudo touch .env
sudo nano .env
```
7. Заполнить по примеру

```
POSTGRES_DB=kittygram
POSTGRES_USER=kittygram_user
POSTGRES_PASSWORD=kittygram_password
DB_NAME=kittygram
DB_HOST=db
DB_PORT=5432
```

8. Добавить домен сайта в файл конфигурации Nginx и проверить конфигурацию, выполнить перезагрузку.
```
sudo nano /etc/nginx/sites-enabled/default
sudo nginx -t
sudo service nginx reload
```

9. Выполнить команды:

```
sudo docker compose -f docker-compose.production.yml pull
sudo docker compose -f docker-compose.production.yml down
sudo docker compose -f docker-compose.production.yml up -d
sudo docker compose -f docker-compose.production.yml exec backend python manage.py migrate
sudo docker compose -f docker-compose.production.yml exec backend python manage.py collectstatic
sudo docker compose -f docker-compose.production.yml exec backend cp -r /app/collected_static/. /backend_static/static/
```


## Автор
#### [_Виктория_](https://github.com/kostoyanskaya/)
