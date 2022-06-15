название машины GCP- test- 34.136.180.199
Установка docker на машину-
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt update
sudo apt install docker-ce -y
sudo systemctl start docker
либо sudo systemctl enable docker
дальше установка PostgreSQL в docker из образа 
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
mkdir -p  /var/lib/postgres
sudo docker pull postgres
теперь запускаем контейнер PostgreSQL
docker run --name postgres-pgdocker -e POSTGRES_PASSWORD=Adi99das -e POSTGRES_USER=postgres -e POSTGRES_DB=postgres -d -p 5432:5432 -v /var/lib/postgres:/var/lib/postgresql/data postgres
после этого подключаемся в psql.
psql -h localhost -U postgres -d postgres 
если не подключается , надо установить sudo apt install postgresql-client 
после уже подключился к базе данных Postgres под пользователем postgres. 

root@test:~# psql -h localhost -U postgres -d postgres
Password for user postgres: 
psql (14.3 (Ubuntu 14.3-1.pgdg20.04+1))
Type "help" for help.

postgres=# \l
                                 List of databases
   Name    |  Owner   | Encoding |  Collate   |   Ctype    |   Access privileges   
-----------+----------+----------+------------+------------+-----------------------
 postgres  | postgres | UTF8     | en_US.utf8 | en_US.utf8 | 
 template0 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |          |            |            | postgres=CTc/postgres
 template1 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |          |            |            | postgres=CTc/postgres
(3 rows)
после exit и docker ps
root@test:~# docker ps
CONTAINER ID   IMAGE      COMMAND                  CREATED          STATUS          PORTS                                       NAMES
7a8d2b0cda02   postgres   "docker-entrypoint.s…"   51 minutes ago   Up 51 minutes   0.0.0.0:5432->5432/tcp, :::5432->5432/tcp   postgres-pgdocker
теперь нам нужно развернуть контейнер postgres 
sudo docker run --name postgres-client3 -e POSTGRES_PASSWORD=Adi99das -e POSTGRES_USER=postgres -e POSTGRES_DB=postgres -d -p 5433:5433 -v $HOME/docker/volumes/postgres:/var/lib/postgresql/data2 postgres
проверяем создался ли контейнер. 
root@test:~# docker ps
CONTAINER ID   IMAGE      COMMAND                  CREATED        STATUS         PORTS                                                 NAMES
7f46de0484aa   postgres   "docker-entrypoint.s…"   23 hours ago   Up 9 minutes   5432/tcp, 0.0.0.0:5433->5433/tcp, :::5433->5433/tcp   postgres-client3
7a8d2b0cda02   postgres   "docker-entrypoint.s…"   27 hours ago   Up 9 minutes   0.0.0.0:5432->5432/tcp, :::5432->5432/tcp             postgres-pgdocker
создался контейнер с названием postgre-client3.
но к нему могу подключиться через  docker exec
root@test:~# docker exec -it postgres-client3 psql -U postgres
psql (14.3 (Debian 14.3-1.pgdg110+1))
Type "help" for help.

postgres=# 

но со внешнего именно к этому контейнеру не могу подключиться, создал его с портом 5433. 
в Firewall открыл порты наружу default-allowpg2
Ingress
Apply to all	
IP ranges: 0.0.0.0/0	
tcp:5433
Allow
65534
default
Off
но не доступен. 

а этот 7a8d2b0cda02(postgres-pgdocker) 
так же на инстанс настроил фаервол наружу и он доступен по IP адресу 34.133.197.173 5432 
через PGadmin4 так же подключился к контейнеру , через свою локальную машину. 

с начала чтобы удостовериться что работает доступ из вне, надо создать базу в контейнере и таблицу в postgres-pgdocker 
root@test:~# docker ps
CONTAINER ID   IMAGE      COMMAND                  CREATED          STATUS             PORTS                                                 NAMES
ff22246a5a61   postgres   "docker-entrypoint.s…"   13 minutes ago   Up 13 minutes      5432/tcp                                              client-postgres
7f46de0484aa   postgres   "docker-entrypoint.s…"   34 minutes ago   Up 34 minutes      5432/tcp, 0.0.0.0:5433->5433/tcp, :::5433->5433/tcp   postgres-client3
7a8d2b0cda02   postgres   "docker-entrypoint.s…"   29 hours ago     Up About an hour   0.0.0.0:5432->5432/tcp, :::5432->5432/tcp             postgres-pgdocker
root@test:~# psql -h localhost -U postgres -d postgres
Password for user postgres: 
psql (14.3 (Ubuntu 14.3-1.pgdg20.04+1))
Type "help" for help.

postgres=# \l
                                 List of databases
   Name    |  Owner   | Encoding |  Collate   |   Ctype    |   Access privileges   
-----------+----------+----------+------------+------------+-----------------------
 postgres  | postgres | UTF8     | en_US.utf8 | en_US.utf8 | 
 template0 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |          |            |            | postgres=CTc/postgres
 template1 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |          |            |            | postgres=CTc/postgres
 test2     | postgres | UTF8     | en_US.utf8 | en_US.utf8 | 
(4 rows)

postgres=# create database dimash;
CREATE DATABASE
postgres=# \l
                                 List of databases
   Name    |  Owner   | Encoding |  Collate   |   Ctype    |   Access privileges   
-----------+----------+----------+------------+------------+-----------------------
 dimash    | postgres | UTF8     | en_US.utf8 | en_US.utf8 | 
 postgres  | postgres | UTF8     | en_US.utf8 | en_US.utf8 | 
 template0 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |          |            |            | postgres=CTc/postgres
 template1 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |          |            |            | postgres=CTc/postgres
 test2     | postgres | UTF8     | en_US.utf8 | en_US.utf8 | 
(5 rows)

postgres=# create table cities (name varchar(80));
CREATE TABLE
postgres=# insert into cities values ('ALMATY');
INSERT 0 1
postgres=# select * from cities;
  name  
--------
 ALMATY
(1 row)
дальше заходим на локальную свою машину и оттуда подключаюсь к контейнеру из вне сети GCP
rgbrandsadmin@linuxtestdimash:~$ psql -h 34.133.197.173 -U postgres -d postgres
Пароль пользователя postgres:
psql (14.2, сервер 14.3 (Debian 14.3-1.pgdg110+1))
Введите "help", чтобы получить справку.

postgres=# \l
                                 Список баз данных
    Имя    | Владелец | Кодировка | LC_COLLATE |  LC_CTYPE  |     Права доступа
-----------+----------+-----------+------------+------------+-----------------------
 dimash    | postgres | UTF8      | en_US.utf8 | en_US.utf8 |
 postgres  | postgres | UTF8      | en_US.utf8 | en_US.utf8 |
 template0 | postgres | UTF8      | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |           |            |            | postgres=CTc/postgres
 template1 | postgres | UTF8      | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |           |            |            | postgres=CTc/postgres
 test2     | postgres | UTF8      | en_US.utf8 | en_US.utf8 |
(5 строк)

postgres=# select * from cities;
  name
--------
 ALMATY
(1 строка)

postgres=#

как видим , из вне подключился и увидили данные которые ранее добавили. 

теперь, удаляю контейнер postgres-pgdocker на машине которая на GCP и заново создаю проверяю остались ли данные. 
root@test:~# docker ps
CONTAINER ID   IMAGE      COMMAND                  CREATED          STATUS          PORTS                                                 NAMES
ff22246a5a61   postgres   "docker-entrypoint.s…"   30 minutes ago   Up 30 minutes   5432/tcp                                              client-postgres
7f46de0484aa   postgres   "docker-entrypoint.s…"   34 minutes ago   Up 34 minutes   5432/tcp, 0.0.0.0:5433->5433/tcp, :::5433->5433/tcp   postgres-client3
7a8d2b0cda02   postgres   "docker-entrypoint.s…"   29 hours ago     Up 2 hours      0.0.0.0:5432->5432/tcp, :::5432->5432/tcp             postgres-pgdocker
root@test:~# docker stop 7a8d2b0cda02
7a8d2b0cda02
root@test:~# docker rm 7a8d2b0cda02
7a8d2b0cda02
root@test:~# docker run --name postgres-pgdocker -e POSTGRES_PASSWORD=Adi99das -e POSTGRES_USER=postgres -e POSTGRES_DB=postgres -d -p 5432:5432 -v /var/lib/postgres:/var/lib/postgresql/data postgres
1cadbe59490f3da933902a70668a66ed5c879782f243700081a757763b2418ce
root@test:~# docker ps
CONTAINER ID   IMAGE      COMMAND                  CREATED          STATUS          PORTS                                                 NAMES
1cadbe59490f   postgres   "docker-entrypoint.s…"   8 seconds ago    Up 8 seconds    0.0.0.0:5432->5432/tcp, :::5432->5432/tcp             postgres-pgdocker
ff22246a5a61   postgres   "docker-entrypoint.s…"   31 minutes ago   Up 31 minutes   5432/tcp                                              client-postgres
7f46de0484aa   postgres   "docker-entrypoint.s…"   34 minutes ago   Up 34 minutes   5432/tcp, 0.0.0.0:5433->5433/tcp, :::5433->5433/tcp   postgres-client3
root@test:~# psql -h localhost -U postgres -d postgres
Password for user postgres: 
psql (14.3 (Ubuntu 14.3-1.pgdg20.04+1))
Type "help" for help.

postgres=# \l
                                 List of databases
   Name    |  Owner   | Encoding |  Collate   |   Ctype    |   Access privileges   
-----------+----------+----------+------------+------------+-----------------------
 dimash    | postgres | UTF8     | en_US.utf8 | en_US.utf8 | 
 postgres  | postgres | UTF8     | en_US.utf8 | en_US.utf8 | 
 template0 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |          |            |            | postgres=CTc/postgres
 template1 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |          |            |            | postgres=CTc/postgres
 test2     | postgres | UTF8     | en_US.utf8 | en_US.utf8 | 
(5 rows)

postgres=# select * from cities;
  name  
--------
 ALMATY
(1 row)

postgres=# 

узнаю, что после добавление данных и удаление контейнера и после создание такого же, данные остались на месте.

в общем цель домашнего задание сделал.
Цель:
развернуть ВМ в GCP/ЯО/Аналоги
установить туда докер
установить PostgreSQL в Docker контейнере
настроить контейнер для внешнего подключения

не сделал: 
развернуть контейнер с клиентом postgres 
так как не понял как это сделать, сделал по другому как выше описал.