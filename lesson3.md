# Урок 3. Введение в Docker

Задание:

1) запустить контейнер с БД, отличной от mariaDB, используя инструкции на сайте: <https://hub.docker.com/>

если не установлен Docker, то установить     - docker apt install.
посмотреть контейнеры в Docker-e             - docker ps
посмотреть образы в Docker-e                 - docker images
запустить контейнер                          - docker run  ubuntu:latest
запустить интерактивно контейнер             - docker run -it ubuntu:22.10 bash  (запуститься bash)

теперь подключение к БД

docker run --detach --name some-mariadb --env MARIADB_ROOT_PASSWORD=my-secret-pw  mariadb:latest
docker exec -запустить процесс в рамках контейнера
sudo docker exec -it bdda9ed57118 mariadb -u root -p      - подключение к БД  11.4.2-MariaDB-ubu2404 mariadb.org


2) добавить в контейнер hostname такой же, как hostname системы через переменную
  * (Системная переменная $HOSTNAME )
  
 docker run -it -h $HOSTNAME ubuntu:latest 
 echo $HOSTNAME

3) заполнить БД данными через консоль
  
MariaDB [(none)]> SHOW DATABASES;
MariaDB [(none)]> CREATE DATABASE my_DB;
USE my_DB;
CREATE TABLE testlora (i INT);
INSERT INTO testlora (i) VALUES (1), (22), (33), (100);
SELECT * FROM testlora;

(скриншоты прилогаюся)


4) запустить phpmyadmin (в контейнере) и через веб проверить, что все введенные данные доступны

docker run --name my-phpmyadmin -d --link test-mariadb:db -p 8081:80 phpmyadmin/phpmyadmin

Формат сдачи ДЗ: предоставить доказательства выполнения задания посредством ссылки на google-документ с правами на комментирование/редактирование.
Результатом работы будет: текст объяснения, логи выполнения, история команд и скриншоты (важно придерживаться такой последовательности).
В названии работы должны быть указаны ФИ, номер группы и номер урока.
