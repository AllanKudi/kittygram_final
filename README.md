#  FULLSTACK-проект KITTYGRAM

## Что за проект?

Это как instagram, но только для котиков! Здесь вы можете поделиться фотографией своего пушистого друга и посмотреть на любимцев других пользователей!

## Что здесь можно делать?

- Создавать профиль, чтобы начать делиться котиками!
- Добавлять пушистых друзей.
- Удалять пушистых друзей.
- Загружать фотографии своих котиков.
- Указывать возраст\цвет\достижения своих питомцев!
- Остальное пока еще в разработке!

## Как пользоваться?

- Всё очень просто! А вот и детальная инструкция по запуску проекта:

# Скачиваем все необходимое для работы докера. Команды для терминала linux ubuntu:
```
sudo apt update
sudo apt install curl
curl -fSL https://get.docker.com -o get-docker.sh
sudo sh ./get-docker.sh
sudo apt-get install docker-compose-plugin
```
# Скачиваем проект и заходим в него:
```
cd kittygram_final/
```
# Создаем и заполняем файл .env по одноименному экземпляру .env.example.

# Запускаем наши контейнеры:
```
sudo docker compose -f docker-compose.production.yml pull
sudo docker compose -f docker-compose.production.yml down
sudo docker compose -f docker-compose.production.yml up -d
sudo docker compose -f docker-compose.production.yml exec backend python manage.py migrate
sudo docker compose -f docker-compose.production.yml exec backend python manage.py collectstatic
sudo docker compose -f docker-compose.production.yml exec backend cp -r /app/collect_static/. /static_backend/static/
```
# Создаем суперпользователя для админки:
```
sudo docker compose -f docker-compose.production.yml exec backend python manage.py createsuperuser
```
- Для работы с собственным сайтом неободимо настроить NGINX!

# Как его установить? Смотрим!
```
sudo apt install nginx -y
sudo systemctl start nginx
sudo ufw allow 'Nginx Full'
sudo ufw allow OpenSSH
sudo ufw enable
sudo nano /etc/nginx/sites-enabled/default
```
# Вносим в конфигурационный файл следующую информацию:
```
server {
    listen 80;
    server_name example.com (ваш домен!);
    
    location / {
        proxy_set_header HOST $host;
        proxy_pass http://127.0.0.1:9000; (можно заменить порт на другой!)

    }
}
```
# Проверяем на очепятки и презагружаем NGINX:
```
sudo nginx -t
sudo systemctl start nginx
```
- И вжух - все работает! Без магии!
## Технологии, которые были применены в проекте:

Python 3.9
Django REST
JS
Node.js
Nginx
Docker
PostgreSQL

## Автор проекта:

Alexandra Kudinova