![Build Status](https://github.com/almaz-gazizov/kittygram_final/actions/workflows/main.yml/badge.svg)

#  Kittygram

Kittygram — это сайт для публикации фотографий своих питомцев.

### Стек используемых технологий:

Ubuntu Server, MacOS, Python, JavaScript, Node.js, Django, Docker, PostgreSQL, Git.

## Как развернуть проект

### Клонирование репозитория

1. Клонируйте репозиторий на свой компьютер:
```
git clone git@github.com:almaz-gazizov/kittygram_final.git
```

2. Создайте файл .env и заполните его своими данными.
```
# Имя пользователя БД
POSTGRES_USER=

# Пароль к БД
POSTGRES_PASSWORD=

# Имя базы данных
POSTGRES_DB=

# Имя Хоста
DB_HOST=

# Порт соединения к БД
DB_PORT=

# Секретный ключ
SECRET_KEY=

# Список разрешённых хостов
ALLOWED_HOSTS=

# Режим отладки
DEBUG=
```

### Деплой на сервере

1. Создайте на сервере директорию kittygram:
```
sudo mkdir kittygram
```

2. Установите docker compose на сервер:
```
sudo apt update
sudo apt install curl
curl -fSL https://get.docker.com -o get-docker.sh
sudo sh ./get-docker.sh
sudo apt-get install docker-compose-plugin
```

3. В директорию kittygram/ скопируйте файлы docker-compose.production.yml и .env

4. На сервере в редакторе nano откройте файл конфигурации Nginx:
```
sudo nano /etc/nginx/sites-enabled/default
```

5. Измените настройки location в секции server:
```
location / {
    proxy_set_header Host $http_host;
    proxy_pass http://127.0.0.1:9000;
}
```

6. Проверьте работоспособность файла конфигурации Nginx, и если ошибок нет, перезапустите Nginx:
```
sudo nginx -t
```
```
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```
```
sudo service nginx reload
```

### CI/CD Workfow

Чтобы адаптировать файл workflow, добавьте секреты в GitHub Actions:
```
# имя пользователя в DockerHub
DOCKER_USERNAME                

# пароль пользователя в DockerHub
DOCKER_PASSWORD

# IP-адрес вашего сервера
HOST

# имя пользователя
USER

# Содержимое текстового файла с закрытым SSH-ключом
SSH_KEY

# кодовая фраза для ssh-ключа
SSH_PASSPHRASE

# ID своего телеграм-аккаунт (узнать свой ID можно у телеграм-бота @userinfobot)
TELEGRAM_TO

# токен вашего бота (получить токен можно у телеграм-бота @BotFather)
TELEGRAM_TOKEN
```

### Автор

Алмаз Газизов