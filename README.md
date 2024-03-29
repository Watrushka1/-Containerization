## Задание 1:Развернуть и запустить контейнер с любым вашим образом(сайт на CMS, образ ОС, образ базы данных, что угодно). Использовать строго Compose
Создаём файл **docker-compose.yaml**, который будет использоваться для запуска двух связанных сервисов - phpmyadmin и mysql. Эти сервисы будут работать вместе, а для управления БД будет использоваться веб-интерфейс phpMyAdmin
```
vi docker-compose.yml
```
Содержимое файла:
```
version: '3'

services:
  phpmyadmin:
    image: phpmyadmin/phpmyadmin
    ports:
      - "8080:80"
    environment:
      PMA_HOST: mysql

  mysql:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: Unforgiven
    volumes:
      - ./data:/var/lib/mysql
```
Сервис **phpmyadmin** использует образ phpmyadmin/phpmyadmin и пробрасывает порт 80 контейнера на порт 8080 хоста. Также задается переменная окружения PMA_HOST со значением mysql, которая указывает на имя сервиса mysql внутри сети Docker.

Сервис **mysql** использует образ mysql:5.7 и задает переменную окружения MYSQL_ROOT_PASSWORD со значением Unforgiven. Также задается том ./data:/var/lib/mysql, который монтируется внутрь контейнера и используется для хранения данных базы данных.

Осталось запустить сервисы с помощью команды
```
docker-compose up -d
```
```
docker ps
CONTAINER ID   IMAGE                   COMMAND                  CREATED             STATUS          PORTS                                   NAMES
39a50e49f2da   mysql:5.7               "docker-entrypoint.s…"   About an hour ago   Up 6 seconds    3306/tcp, 33060/tcp                     container_hw5_mysql_1
4fbbd943250a   phpmyadmin/phpmyadmin   "/docker-entrypoint.…"   About an hour ago   Up 6 seconds    0.0.0.0:8080->80/tcp, :::8080->80/tcp   container_hw5_phpmyadmin_1
```
![phpMyAdmin](https://github.com/Watrushka1/-Containerization/blob/main/phpmyadmin.png)

