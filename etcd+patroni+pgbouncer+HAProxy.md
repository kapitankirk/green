Создал 4 ноды вручную, 1 нода для управление , 3 ноды для etcd 
с начала не мог понять в чем ошибка почему не создается по скрипту все ноды в GCP(так и не понял) ), и установил etcd вручную на каждый сервер. 

После остановка службы на всех 3 нодах, завершалась с ошибкой. 

root@mytest:~# for i in {1..3}; do gcloud compute ssh node$i --command='systemctl stop etcd' & done;
[16] 2877
[17] 2878
[18] 2879
root@mytest:~# Did you mean zone [us-central1-a] for instance: [node1] (Y/n)?  Did you mean zone [us-central1-a] for instance: [node2] (Y/n)?  Did you mean zone [us-central1-a] for instance: [node3] (Y/n)?  Y
Command 'Yes' not found  (вот здесь ошибка, что зону не может определить)

Зону надо было установить , gcloud config set compute/zone us-central1-a
после этого теперь не спрашивает про зону. 

root@mytest:~# for i in {1..3}; do gcloud compute ssh node$i --command='systemctl stop etcd' & done;
[19] 3178
[20] 3179
[21] 3180
root@mytest:~# 
[19]   Done                    gcloud compute ssh node$i --command='systemctl stop etcd'
[20]   Done                    gcloud compute ssh node$i --command='systemctl stop etcd'
[21]   Done                    gcloud compute ssh node$i --command='systemctl stop etcd'

после добавляю в конфиг настройки

root@mytest:~# for i in {1..3}; do gcloud compute ssh node$i --command='cat > temp.cfg << EOF 
> ETCD_NAME="$(hostname)"
> ETCD_LISTEN_CLIENT_URLS="http://0.0.0.0:2379"
> ETCD_ADVERTISE_CLIENT_URLS="http://$(hostname):2379"
> ETCD_LISTEN_PEER_URLS="http://0.0.0.0:2380"
> ETCD_INITIAL_ADVERTISE_PEER_URLS="http://$(hostname):2380"
> ETCD_INITIAL_CLUSTER_TOKEN="PatroniCluster"
> ETCD_INITIAL_CLUSTER="node1=http://node1:2380,node2=http://node2:2380,node3=http://node3:2380"
> ETCD_INITIAL_CLUSTER_STATE="new"
> ETCD_DATA_DIR="/var/lib/etcd"
> EOF
> cat temp.cfg | sudo tee -a /etc/default/etcd
> ' & done;
[1] 4339
[2] 4340
[3] 4341
root@mytest:~# ETCD_NAME="node1"
ETCD_LISTEN_CLIENT_URLS="http://0.0.0.0:2379"
ETCD_ADVERTISE_CLIENT_URLS="http://node1:2379"
ETCD_LISTEN_PEER_URLS="http://0.0.0.0:2380"
ETCD_INITIAL_ADVERTISE_PEER_URLS="http://node1:2380"
ETCD_INITIAL_CLUSTER_TOKEN="PatroniCluster"
ETCD_INITIAL_CLUSTER="node1=http://node1:2380,node2=http://node2:2380,node3=http://node3:2380"
ETCD_INITIAL_CLUSTER_STATE="new"
ETCD_DATA_DIR="/var/lib/etcd"
ETCD_NAME="node2"
ETCD_LISTEN_CLIENT_URLS="http://0.0.0.0:2379"
ETCD_ADVERTISE_CLIENT_URLS="http://node2:2379"
ETCD_LISTEN_PEER_URLS="http://0.0.0.0:2380"
ETCD_INITIAL_ADVERTISE_PEER_URLS="http://node2:2380"
ETCD_INITIAL_CLUSTER_TOKEN="PatroniCluster"
ETCD_INITIAL_CLUSTER="node1=http://node1:2380,node2=http://node2:2380,node3=http://node3:2380"
ETCD_INITIAL_CLUSTER_STATE="new"
ETCD_DATA_DIR="/var/lib/etcd"
ETCD_NAME="node3"
ETCD_LISTEN_CLIENT_URLS="http://0.0.0.0:2379"
ETCD_ADVERTISE_CLIENT_URLS="http://node3:2379"
ETCD_LISTEN_PEER_URLS="http://0.0.0.0:2380"
ETCD_INITIAL_ADVERTISE_PEER_URLS="http://node3:2380"
ETCD_INITIAL_CLUSTER_TOKEN="PatroniCluster"
ETCD_INITIAL_CLUSTER="node1=http://node1:2380,node2=http://node2:2380,node3=http://node3:2380"
ETCD_INITIAL_CLUSTER_STATE="new"
ETCD_DATA_DIR="/var/lib/etcd"

после добавление конфига , запускаю на всех нодах etcd 

root@mytest:~# for i in {1..3}; do gcloud compute ssh node$i --command='sudo systemctl start etcd' & done;
[1] 6228
[2] 6229
[3] 6230
root@mytest:~# 
[1]   Done                    gcloud compute ssh node$i --command='sudo systemctl start etcd'
[2]-  Done                    gcloud compute ssh node$i --command='sudo systemctl start etcd'
[3]+  Done                    gcloud compute ssh node$i --command='sudo systemctl start etcd'

проверка автозагрузки 
root@node1:~# systemctl is-enabled etcd
enabled

Проверка Кластера:
root@node1:~# etcdctl cluster-health
member 63eee28126d82e8 is healthy: got healthy result from http://node3:2379
member e053bdb80051f99a is healthy: got healthy result from http://node1:2379
member eac43c483bf4b327 is healthy: got healthy result from http://node2:2379
cluster is healthy


Патрони
dimash9527@mytest:~$ sudo su - root
root@mytest:~# for i in {1..3}; do gcloud beta compute --project=postgres-27011995 instances create pgsql$i --zone=us-central1-a --machine-type=e2-small --subnet=default --network-tier=PREMIUM --maintenance-policy=MIGRATE --service-account=444352908086-compute@developer.gserviceaccount.com --scopes=https://www.googleapis.com/auth/cloud-platform --image-family=ubuntu-2004-lts --image-project=ubuntu-os-cloud --boot-disk-size=10GB --boot-disk-type=pd-ssd --boot-disk-device-name=pgsql$i --no-shielded-secure-boot --shielded-vtpm --shielded-integrity-monitoring --reservation-affinity=any & done;
[1] 1135
[2] 1136
[3] 1137
root@mytest:~# 
root@mytest:~# Created [https://www.googleapis.com/compute/beta/projects/postgres-27011995/zones/us-central1-a/instances/pgsql2].
NAME    ZONE           MACHINE_TYPE  PREEMPTIBLE  INTERNAL_IP  EXTERNAL_IP     STATUS
pgsql2  us-central1-a  e2-small                   10.128.0.14  34.170.190.183  RUNNING
Created [https://www.googleapis.com/compute/beta/projects/postgres-27011995/zones/us-central1-a/instances/pgsql1].
Created [https://www.googleapis.com/compute/beta/projects/postgres-27011995/zones/us-central1-a/instances/pgsql3].
NAME    ZONE           MACHINE_TYPE  PREEMPTIBLE  INTERNAL_IP  EXTERNAL_IP     STATUS
pgsql1  us-central1-a  e2-small                   10.128.0.12  34.122.153.239  RUNNING
NAME    ZONE           MACHINE_TYPE  PREEMPTIBLE  INTERNAL_IP  EXTERNAL_IP    STATUS
pgsql3  us-central1-a  e2-small                   10.128.0.13  34.170.213.80  RUNNING

[1]   Done                    gcloud beta compute --project=postgres-27011995 instances create pgsql$i --zone=us-central1-a --machine-type=e2-small --subnet=default --network-tier=PREMIUM --maintenance-policy=MIGRATE --service-account=444352908086-compute@developer.gserviceaccount.com --scopes=https://www.googleapis.com/auth/cloud-platform --image-family=ubuntu-2004-lts --image-project=ubuntu-os-cloud --boot-disk-size=10GB --boot-disk-type=pd-ssd --boot-disk-device-name=pgsql$i --no-shielded-secure-boot --shielded-vtpm --shielded-integrity-monitoring --reservation-affinity=any
[2]-  Done                    gcloud beta compute --project=postgres-27011995 instances create pgsql$i --zone=us-central1-a --machine-type=e2-small --subnet=default --network-tier=PREMIUM --maintenance-policy=MIGRATE --service-account=444352908086-compute@developer.gserviceaccount.com --scopes=https://www.googleapis.com/auth/cloud-platform --image-family=ubuntu-2004-lts --image-project=ubuntu-os-cloud --boot-disk-size=10GB --boot-disk-type=pd-ssd --boot-disk-device-name=pgsql$i --no-shielded-secure-boot --shielded-vtpm --shielded-integrity-monitoring --reservation-affinity=any
[3]+  Done                    gcloud beta compute --project=postgres-27011995 instances create pgsql$i --zone=us-central1-a --machine-type=e2-small --subnet=default --network-tier=PREMIUM --maintenance-policy=MIGRATE --service-account=444352908086-compute@developer.gserviceaccount.com --scopes=https://www.googleapis.com/auth/cloud-platform --image-family=ubuntu-2004-lts --image-project=ubuntu-os-cloud --boot-disk-size=10GB --boot-disk-type=pd-ssd --boot-disk-device-name=pgsql$i --no-shielded-secure-boot --shielded-vtpm --shielded-integrity-monitoring --reservation-affinity=any

постгрес установил 
[1]   Done                    gcloud compute ssh pgsql$i --command='sudo apt update && sudo apt upgrade -y -q && echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" | sudo tee -a /etc/apt/sources.list.d/pgdg.list && wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add - && sudo apt-get update && sudo apt -y install postgresql-14'
[2]-  Done                    gcloud compute ssh pgsql$i --command='sudo apt update && sudo apt upgrade -y -q && echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" | sudo tee -a /etc/apt/sources.list.d/pgdg.list && wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add - && sudo apt-get update && sudo apt -y install postgresql-14'
[3]+  Done                    gcloud compute ssh pgsql$i --command='sudo apt update && sudo apt upgrade -y -q && echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" | sudo tee -a /etc/apt/sources.list.d/pgdg.list && wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add - && sudo apt-get update && sudo apt -y install postgresql-14'

проверка работает ли кластер 
root@mytest:~# for i in {1..3}; do gcloud compute ssh pgsql$i --command='hostname; pg_lsclusters' & done;
[1] 1348
[2] 1349
[3] 1350
root@mytest:~# pgsql3
pgsql2
Ver Cluster Port Status Owner    Data directory              Log file
14  main    5432 online postgres /var/lib/postgresql/14/main /var/log/postgresql/postgresql-14-main.log
Ver Cluster Port Status Owner    Data directory              Log file
14  main    5432 online postgres /var/lib/postgresql/14/main /var/log/postgresql/postgresql-14-main.log
pgsql1
Ver Cluster Port Status Owner    Data directory              Log file
14  main    5432 online postgres /var/lib/postgresql/14/main /var/log/postgresql/postgresql-14-main.log

[1]   Done                    gcloud compute ssh pgsql$i --command='hostname; pg_lsclusters'
[2]-  Done                    gcloud compute ssh pgsql$i --command='hostname; pg_lsclusters'
[3]+  Done                    gcloud compute ssh pgsql$i --command='hostname; pg_lsclusters'

проверка доступности по сети. 
dimash9527@node1:~$ sudo su - root
root@node1:~# ping pgsql1
PING pgsql1.us-central1-a.c.postgres-27011995.internal (10.128.0.12) 56(84) bytes of data.
64 bytes from pgsql1.us-central1-a.c.postgres-27011995.internal (10.128.0.12): icmp_seq=1 ttl=64 time=1.55 ms
64 bytes from pgsql1.us-central1-a.c.postgres-27011995.internal (10.128.0.12): icmp_seq=2 ttl=64 time=0.294 ms
64 bytes from pgsql1.us-central1-a.c.postgres-27011995.internal (10.128.0.12): icmp_seq=3 ttl=64 time=0.363 ms
64 bytes from pgsql1.us-central1-a.c.postgres-27011995.internal (10.128.0.12): icmp_seq=4 ttl=64 time=0.252 ms

root@pgsql1:~# ping node1
PING node1.us-central1-a.c.postgres-27011995.internal (10.128.0.8) 56(84) bytes of data.
64 bytes from node1.us-central1-a.c.postgres-27011995.internal (10.128.0.8): icmp_seq=1 ttl=64 time=1.55 ms
64 bytes from node1.us-central1-a.c.postgres-27011995.internal (10.128.0.8): icmp_seq=2 ttl=64 time=0.263 ms

питон на первой ноде 

dimash9527@pgsql1:~$ sudo pip3 install psycopg2-binary
Collecting psycopg2-binary
  Downloading psycopg2_binary-2.9.3-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (3.0 MB)
     |████████████████████████████████| 3.0 MB 5.3 MB/s 
Installing collected packages: psycopg2-binary
Successfully installed psycopg2-binary-2.9.3

dimash9527@pgsql1:~$ sudo systemctl stop postgresql@14-main
dimash9527@pgsql1:~$ sudo -u postgres pg_dropcluster 14 main 
Warning: systemd was not informed about the removed cluster yet. Operations like "service postgresql start" might fail. To fix, run:
  sudo systemctl daemon-reload


  dimash9527@pgsql1:~$ pg_lsclusters
Ver Cluster Port Status Owner Data directory Log file

включаем старт сервиса
sudo nano /etc/systemd/system/patroni.service

добавлю туда конфиг: 
[Unit]
Description=High availability PostgreSQL Cluster
After=syslog.target network.target
[Service]
Type=simple
User=postgres
Group=postgres
ExecStart=/usr/local/bin/patroni /etc/patroni.yml
KillMode=process
TimeoutSec=30
Restart=no
[Install]
WantedBy=multi-user.target

конфиг кластера патрони. 

scope: patroni
name:pgsql1
restapi:
  listen: 10.128.0.12:8008
  connect_address: 10.166.0.12:8008
etcd:
  hosts: node1.us-central1-a.c.postgres-27011995.internal:2379,node2.us-central1-a.c.postgres-27011995.internal:2379,node3.us-central1-a.c.postgres-27011995.internal.internal:2379
bootstrap:
  dcs:
    ttl: 30
    loop_wait: 10
    retry_timeout: 10
    maximum_lag_on_failover: 1048576
    postgresql:
      use_pg_rewind: true
      parameters:
  initdb: 
  - encoding: UTF8
  - data-checksums
  pg_hba: 
  - host replication replicator 10.0.0.0/8 md5
  - host all all 10.0.0.0/8 md5
  users:
    admin:
      password: Adi99das
      options:
        - createrole
        - createdb
postgresql:
  listen: 127.0.0.1, 10.128.0.12:5432
  connect_address: 10.128.0.12:5432
  data_dir: /var/lib/postgresql/14/main
  bin_dir: /usr/lib/postgresql/14/bin
  pgpass: /tmp/pgpass0
  authentication:
    replication:
      username: replicator
      password: rep-pass_321
    superuser:
      username: postgres
      password: Adi99das
    rewind:  
      username: rewind_user
      password: rewind_password_321
  parameters:
    unix_socket_directories: '.'
tags:
    nofailover: false
    noloadbalance: false
    clonefrom: false
    nosync: false

    обновляю параметры etcd , добавлю полное название.
    
    root@mytest:~# for i in {1..3}; do gcloud compute ssh node$i --command='cat > temp2.cfg << EOF 
> ETCD_ADVERTISE_CLIENT_URLS="http://$(hostname).us-central1-a.c.postgres-27011995.internal:2379"
> EOF
> cat temp2.cfg | sudo tee -a /etc/default/etcd
> ' & done;
[1] 2678
[2] 2679
[3] 2680
root@mytest:~# ETCD_ADVERTISE_CLIENT_URLS="http://node3.us-central1-a.c.postgres-27011995.internal:2379"
ETCD_ADVERTISE_CLIENT_URLS="http://node1.us-central1-a.c.postgres-27011995.internal:2379"
ETCD_ADVERTISE_CLIENT_URLS="http://node2.us-central1-a.c.postgres-27011995.internal:2379"

[1]   Done                    gcloud compute ssh node$i --command='cat > temp2.cfg << EOF 
ETCD_ADVERTISE_CLIENT_URLS="http://$(hostname).us-central1-a.c.postgres-27011995.internal:2379"
EOF
cat temp2.cfg | sudo tee -a /etc/default/etcd
'
[2]-  Done                    gcloud compute ssh node$i --command='cat > temp2.cfg << EOF 
ETCD_ADVERTISE_CLIENT_URLS="http://$(hostname).us-central1-a.c.postgres-27011995.internal:2379"
EOF
cat temp2.cfg | sudo tee -a /etc/default/etcd
'
[3]+  Done                    gcloud compute ssh node$i --command='cat > temp2.cfg << EOF 
ETCD_ADVERTISE_CLIENT_URLS="http://$(hostname).us-central1-a.c.postgres-27011995.internal:2379"
EOF
cat temp2.cfg | sudo tee -a /etc/default/etcd
'

включаю службы. 

root@mytest:~# for i in {1..3}; do gcloud compute ssh node$i --command='sudo systemctl start etcd' & done;
[1] 2770
[2] 2771
[3] 2772
root@mytest:~# 
[1]   Done                    gcloud compute ssh node$i --command='sudo systemctl start etcd'
[2]-  Done                    gcloud compute ssh node$i --command='sudo systemctl start etcd'
[3]+  Done                    gcloud compute ssh node$i --command='sudo systemctl start etcd'

root@pgsql1:~# sudo -u postgres patroni /etc/patroni.yml
2022-07-19 08:41:48,670 INFO: Selected new etcd server http://node3.us-central1-a.c.postgres-27011995.internal:2379
2022-07-19 08:41:48,682 INFO: No PostgreSQL configuration items changed, nothing to reload.
2022-07-19 08:41:48,696 INFO: Lock owner: None; I am pgsql1
2022-07-19 08:41:48,705 INFO: trying to bootstrap a new cluster
could not change directory to "/root": Permission denied
The files belonging to this database system will be owned by user "postgres".
This user must also own the server process.

The database cluster will be initialized with locale "C.UTF-8".
The default text search configuration will be set to "english".

Data page checksums are enabled.

creating directory /var/lib/postgresql/14/main ... ok
creating subdirectories ... ok
selecting dynamic shared memory implementation ... posix
selecting default max_connections ... 100
selecting default shared_buffers ... 128MB
selecting default time zone ... Etc/UTC
creating configuration files ... ok
running bootstrap script ... ok
performing post-bootstrap initialization ... ok
syncing data to disk ... ok

initdb: warning: enabling "trust" authentication for local connections
You can change this by editing pg_hba.conf or using the option -A, or
--auth-local and --auth-host, the next time you run initdb.

Success. You can now start the database server using:

    /usr/lib/postgresql/14/bin/pg_ctl -D /var/lib/postgresql/14/main -l logfile start

    root@pgsql1:~# sudo patronictl -c /etc/patroni.yml list
+--------+------+------+-------+----+-----------+
| Member | Host | Role | State | TL | Lag in MB |
+ Cluster: patroni (initializing) --+-----------+
+--------+------+------+-------+----+-----------+
root@pgsql1:~# sudo systemctl start patroni
root@pgsql1:~# sudo patronictl -c /etc/patroni.yml list
+--------+-------------+--------+---------+----+-----------+
| Member | Host        | Role   | State   | TL | Lag in MB |
+ Cluster: patroni (7122001137243157900) -+----+-----------+
| pgsql1 | 10.128.0.12 | Leader | running |  2 |           |
+--------+-------------+--------+---------+----+-----------+

установка на две другие ноды pgsql2-pgsql3.

Successfully built ydiff python-etcd
Installing collected packages: python-dateutil, wcwidth, prettytable, ydiff, psutil, dnspython, python-etcd, patroni
Successfully installed dnspython-2.2.1 patroni-2.1.4 prettytable-3.3.0 psutil-5.9.1 python-dateutil-2.8.2 python-etcd-0.4.5 wcwidth-0.2.5 ydiff-1.2
Successfully installed dnspython-2.2.1 patroni-2.1.4 prettytable-3.3.0 psutil-5.9.1 python-dateutil-2.8.2 python-etcd-0.4.5 wcwidth-0.2.5 ydiff-1.2

[1]-  Done                    gcloud compute ssh pgsql$i --command='sudo apt install -y python3 python3-pip git mc && sudo pip3 install psycopg2-binary && sudo systemctl stop postgresql@14-main && sudo -u postgres pg_dropcluster 14 main && sudo pip3 install patroni[etcd] && sudo ln -s /usr/local/bin/patroni /bin/patroni'
[2]+  Done                    gcloud compute ssh pgsql$i --command='sudo apt install -y python3 python3-pip git mc && sudo pip3 install psycopg2-binary && sudo systemctl stop postgresql@14-main && sudo -u postgres pg_dropcluster 14 main && sudo pip3 install patroni[etcd] && sudo ln -s /usr/local/bin/patroni /bin/patroni


dimash9527@mytest:~$ sudo su - root
root@mytest:~# for i in {2..3}; do gcloud compute ssh pgsql$i --command='cat > temp.cfg << EOF 
> [Unit]
> Description=High availability PostgreSQL Cluster
> After=syslog.target network.target
> [Service]
> Type=simple
> User=postgres
> Group=postgres
> ExecStart=/usr/local/bin/patroni /etc/patroni.yml
> KillMode=process
> TimeoutSec=30
> Restart=no
> [Install]
> WantedBy=multi-user.target
> EOF
> cat temp.cfg | sudo tee -a /etc/systemd/system/patroni.service
> ' & done;
[1] 4350
[2] 4351
root@mytest:~# [Unit]
Description=High availability PostgreSQL Cluster
After=syslog.target network.target
[Service]
Type=simple
User=postgres
Group=postgres
ExecStart=/usr/local/bin/patroni /etc/patroni.yml
KillMode=process
TimeoutSec=30
Restart=no
[Install]
WantedBy=multi-user.target
[Unit]
Description=High availability PostgreSQL Cluster
After=syslog.target network.target
[Service]
Type=simple
User=postgres
Group=postgres
ExecStart=/usr/local/bin/patroni /etc/patroni.yml
KillMode=process
TimeoutSec=30
Restart=no
[Install]
WantedBy=multi-user.target

[1]-  Done                    gcloud compute ssh pgsql$i --command='cat > temp.cfg << EOF 
[Unit]
Description=High availability PostgreSQL Cluster
After=syslog.target network.target
[Service]
Type=simple
User=postgres
Group=postgres
ExecStart=/usr/local/bin/patroni /etc/patroni.yml
KillMode=process
TimeoutSec=30
Restart=no
[Install]
WantedBy=multi-user.target
EOF
cat temp.cfg | sudo tee -a /etc/systemd/system/patroni.service
'
[2]+  Done                    gcloud compute ssh pgsql$i --command='cat > temp.cfg << EOF 
[Unit]
Description=High availability PostgreSQL Cluster
After=syslog.target network.target
[Service]
Type=simple
User=postgres
Group=postgres
ExecStart=/usr/local/bin/patroni /etc/patroni.yml
KillMode=process
TimeoutSec=30
Restart=no
[Install]
WantedBy=multi-user.target
EOF
ca

Добавляю конфиг настроек кластера 
root@mytest:~# scope: patroni
name: pgsql3
restapi:
  listen: 10.128.0.13:8008
  connect_address: 10.128.0.13:8008
etcd:
  hosts: node1.us-central1-a.c.postgres-27011995.internal:2379,node2.us-central1-a.c.postgres-27011995.internal:2379,node3.us-central1-a.c.postgres-27011995.internal:2379
bootstrap:
  dcs:
    ttl: 30
    loop_wait: 10
    retry_timeout: 10
    maximum_lag_on_failover: 1048576
    postgresql:
      use_pg_rewind: true
      parameters:
  initdb: 
  - encoding: UTF8
  - data-checksums
  pg_hba: 
  - host replication replicator 10.0.0.0/8 md5
  - host all all 10.0.0.0/8 md5
  users:
    admin:
      password: Adi99das
      options:
        - createrole
        - createdb
postgresql:
  listen: 127.0.0.1, 10.128.0.13:5432
  connect_address: 10.128.0.13:5432
  data_dir: /var/lib/postgresql/14/main
  bin_dir: /usr/lib/postgresql/14/bin
  pgpass: /tmp/pgpass0
  authentication:
    replication:
      username: replicator
      password: rep-pass_321
    superuser:
      username: postgres
      password: Adi99das
    rewind:  
      username: rewind_user
      password: rewind_password_321
  parameters:
    unix_socket_directories: .
tags:
    nofailover: false
    noloadbalance: false
    clonefrom: false
    nosync: false
scope: patroni
name: pgsql2
restapi:
  listen: 10.128.0.14:8008
  connect_address: 10.128.0.14:8008
etcd:
  hosts: node1.us-central1-a.c.postgres-27011995.internal:2379,node2.us-central1-a.c.postgres-27011995.internal:2379,node3.us-central1-a.c.postgres-27011995.internal:2379
bootstrap:
  dcs:
    ttl: 30
    loop_wait: 10
    retry_timeout: 10
    maximum_lag_on_failover: 1048576
    postgresql:
      use_pg_rewind: true
      parameters:
  initdb: 
  - encoding: UTF8
  - data-checksums
  pg_hba: 
  - host replication replicator 10.0.0.0/8 md5
  - host all all 10.0.0.0/8 md5
  users:
    admin:
      password: Adi99das
      options:
        - createrole
        - createdb
postgresql:
  listen: 127.0.0.1, 10.128.0.14:5432
  connect_address: 10.128.0.14:5432
  data_dir: /var/lib/postgresql/14/main
  bin_dir: /usr/lib/postgresql/14/bin
  pgpass: /tmp/pgpass0
  authentication:
    replication:
      username: replicator
      password: rep-pass_321
    superuser:
      username: postgres
      password: Adi99das
    rewind:  
      username: rewind_user
      password: rewind_password_321
  parameters:
    unix_socket_directories: .
tags:
    nofailover: false
    noloadbalance: false
    clonefrom: false
    nosync: false

[1]-  Done                    gcloud compute ssh pgsql$i --command='cat > temp2.cfg << EOF 
scope: patroni
name: $(hostname)
restapi:
  listen: $(hostname -I | tr -d " "):8008
  connect_address: $(hostname -I | tr -d " "):8008
etcd:
  hosts: node1.us-central1-a.c.postgres-27011995.internal:2379,node2.us-central1-a.c.postgres-27011995.internal:2379,node3.us-central1-a.c.postgres-27011995.internal:2379
bootstrap:
  dcs:
    ttl: 30
    loop_wait: 10
    retry_timeout: 10
    maximum_lag_on_failover: 1048576
    postgresql:
      use_pg_rewind: true
      parameters:
  initdb: 
  - encoding: UTF8
  - data-checksums
  pg_hba: 
  - host replication replicator 10.0.0.0/8 md5
  - host all all 10.0.0.0/8 md5
  users:
    admin:
      password: Adi99das
      options:
        - createrole
        - createdb
postgresql:
  listen: 127.0.0.1, $(hostname -I | tr -d " "):5432
  connect_address: $(hostname -I | tr -d " "):5432
  data_dir: /var/lib/postgresql/14/main
  bin_dir: /usr/lib/postgresql/14/bin
  pgpass: /tmp/pgpass0
  authentication:
    replication:
      username: replicator
      password: rep-pass_321
    superuser:
      username: postgres
      password: Adi99das
    rewind:  
      username: rewind_user
      password: rewind_password_321
  parameters:
    unix_socket_directories: '.'
tags:
    nofailover: false
    noloadbalance: false
    clonefrom: false
    nosync: false
EOF
cat temp2.cfg | sudo tee -a /etc/patroni.yml
'
[2]+  Done                    gcloud compute ssh pgsql$i --command='cat > temp2.cfg << EOF 
scope: patroni
name: $(hostname)
restapi:
  listen: $(hostname -I | tr -d " "):8008
  connect_address: $(hostname -I | tr -d " "):8008
etcd:
  hosts: node1.us-central1-a.c.postgres-27011995.internal:2379,node2.us-central1-a.c.postgres-27011995.internal:2379,node3.us-central1-a.c.postgres-27011995.internal:2379
bootstrap:
  dcs:
    ttl: 30
    loop_wait: 10
    retry_timeout: 10
    maximum_lag_on_failover: 1048576
    postgresql:
      use_pg_rewind: true
      parameters:
  initdb: 
  - encoding: UTF8
  - data-checksums
  pg_hba: 
  - host replication replicator 10.0.0.0/8 md5
  - host all all 10.0.0.0/8 md5
  users:
    admin:
      password: Adi99das
      options:
        - createrole
        - createdb
postgresql:
  listen: 127.0.0.1, $(hostname -I | tr -d " "):5432
  connect_address: $(hostname -I | tr -d " "):5432
  data_dir: /var/lib/postgresql/14/main
  bin_dir: /usr/lib/postgresql/14/bin
  pgpass: /tmp/pgpass0
  authentication:
    replication:
      username: replicator
      password: rep-pass_321
    superuser:
      username: postgres
      password: Adi99das
    rewind:  
      username: rewind_user
      password: rewind_password_321
  parameters:
    unix_socket_directories: '.'
tags:
    nofailover: false
    noloadbalance: false
    clonefrom: false
    nosync: false
EOF
cat temp2.cfg | sudo tee -a /etc/patroni.yml
'


НЕ поднимались реплики, а именно статус stopped был. 
root@pgsql1:~# sudo patronictl -c /etc/patroni.yml list
+--------+-------------+---------+---------+----+-----------+
| Member | Host        | Role    | State   | TL | Lag in MB |
+ Cluster: patroni (7122001137243157900) --+----+-----------+
| pgsql1 | 10.128.0.12 | Replica | running | 16 |         0 |
| pgsql2 | 10.128.0.14 | Leader  | running | 16 |           |
| pgsql3 | 10.128.0.13 | Replica | running | 16 |         0 |
+--------+-------------+---------+---------+----+-----------+
root@pgsql1:~# systemctl status patroni
● patroni.service - High availability PostgreSQL Cluster
     Loaded: loaded (/etc/systemd/system/patroni.service; enabled; vendor preset: enabled)
     Active: active (running) since Wed 2022-07-20 08:25:26 UTC; 1min 16s ago
   Main PID: 7253 (patroni)
      Tasks: 12 (limit: 2359)
     Memory: 62.5M
     CGroup: /system.slice/patroni.service
             ├─7253 /usr/bin/python3 /usr/local/bin/patroni /etc/patroni.yml
             ├─7268 /usr/lib/postgresql/14/bin/postgres -D /var/lib/postgresql/14/main --config-file=/var/lib/postgresql/14/main/postgresql.conf --listen_addresses=127.0.0.1, 10.128.0.12 --port=5432 --cluster_name=patroni --wal_level=replic>
             ├─7270 postgres: patroni: startup recovering 000000100000000000000004
             ├─7273 postgres: patroni: checkpointer
             ├─7274 postgres: patroni: background writer
             ├─7275 postgres: patroni: stats collector
             ├─7277 postgres: patroni: postgres postgres 127.0.0.1(39386) idle
             └─7293 postgres: patroni: walreceiver streaming 0/40001F0

Jul 20 08:26:39 pgsql1 patroni[7253]:   File "/usr/local/lib/python3.8/dist-packages/patroni/postgresql/rewind.py", line 68, in check_leader_is_not_in_recovery
Jul 20 08:26:39 pgsql1 patroni[7253]:     with get_connection_cursor(connect_timeout=3, options='-c statement_timeout=2000', **conn_kwargs) as cur:
Jul 20 08:26:39 pgsql1 patroni[7253]:   File "/usr/lib/python3.8/contextlib.py", line 113, in __enter__
Jul 20 08:26:39 pgsql1 patroni[7253]:     return next(self.gen)
Jul 20 08:26:39 pgsql1 patroni[7253]:   File "/usr/local/lib/python3.8/dist-packages/patroni/postgresql/connection.py", line 44, in get_connection_cursor
Jul 20 08:26:39 pgsql1 patroni[7253]:     conn = psycopg.connect(**kwargs)
Jul 20 08:26:39 pgsql1 patroni[7253]:   File "/usr/local/lib/python3.8/dist-packages/psycopg2/__init__.py", line 122, in connect
Jul 20 08:26:39 pgsql1 patroni[7253]:     conn = _connect(dsn, connection_factory=connection_factory, **kwasync)
Jul 20 08:26:39 pgsql1 patroni[7253]: psycopg2.OperationalError: connection to server at "10.128.0.14", port 5432 failed: FATAL:  role "rewind_user" does not exist
Jul 20 08:26:39 pgsql1 patroni[7253]: 2022-07-20 08:26:39,906 INFO: no action. I am (pgsql1), a secondary, and following a leader (pgsql2)

root@pgsql1:~# psql -U postgres -h10.128.0.14
psql (14.4 (Ubuntu 14.4-1.pgdg20.04+1))
Type "help" for help.

postgres=# create user rewind_user;
CREATE ROLE
postgres=# \password rewind_user
Enter new password for user "rewind_user": 
Enter it again: 
postgres=# \q
root@pgsql1:~# psql -U postgres -hlocalhost
psql (14.4 (Ubuntu 14.4-1.pgdg20.04+1))
Type "help" for help.

postgres=# \q
root@pgsql1:~# systemctl status patroni
● patroni.service - High availability PostgreSQL Cluster
     Loaded: loaded (/etc/systemd/system/patroni.service; enabled; vendor preset: enabled)
     Active: active (running) since Wed 2022-07-20 08:25:26 UTC; 3min 35s ago
   Main PID: 7253 (patroni)
      Tasks: 12 (limit: 2359)
     Memory: 63.5M
     CGroup: /system.slice/patroni.service
             ├─7253 /usr/bin/python3 /usr/local/bin/patroni /etc/patroni.yml
             ├─7268 /usr/lib/postgresql/14/bin/postgres -D /var/lib/postgresql/14/main --config-file=/var/lib/postgresql/14/main/postgresql.conf --listen_addresses=127.0.0.1, 10.128.0.12 --port=5432 --cluster_name=patroni --wal_level=replic>
             ├─7270 postgres: patroni: startup recovering 000000100000000000000004
             ├─7273 postgres: patroni: checkpointer
             ├─7274 postgres: patroni: background writer
             ├─7275 postgres: patroni: stats collector
             ├─7277 postgres: patroni: postgres postgres 127.0.0.1(39386) idle
             └─7293 postgres: patroni: walreceiver streaming 0/40011F8

Jul 20 08:27:59 pgsql1 patroni[7253]: 2022-07-20 08:27:59,906 INFO: no action. I am (pgsql1), a secondary, and following a leader (pgsql2)
Jul 20 08:28:09 pgsql1 patroni[7253]: 2022-07-20 08:28:09,892 INFO: Lock owner: pgsql2; I am pgsql1
Jul 20 08:28:09 pgsql1 patroni[7253]: 2022-07-20 08:28:09,893 INFO: Local timeline=16 lsn=0/4001058
Jul 20 08:28:09 pgsql1 patroni[7253]: 2022-07-20 08:28:09,925 INFO: master_timeline=16
Jul 20 08:28:09 pgsql1 patroni[7253]: 2022-07-20 08:28:09,931 INFO: no action. I am (pgsql1), a secondary, and following a leader (pgsql2)
Jul 20 08:28:19 pgsql1 patroni[7253]: 2022-07-20 08:28:19,897 INFO: no action. I am (pgsql1), a secondary, and following a leader (pgsql2)
Jul 20 08:28:29 pgsql1 patroni[7253]: 2022-07-20 08:28:29,899 INFO: no action. I am (pgsql1), a secondary, and following a leader (pgsql2)
Jul 20 08:28:39 pgsql1 patroni[7253]: 2022-07-20 08:28:39,899 INFO: no action. I am (pgsql1), a secondary, and following a leader (pgsql2)
Jul 20 08:28:49 pgsql1 patroni[7253]: 2022-07-20 08:28:49,896 INFO: no action. I am (pgsql1), a secondary, and following a leader (pgsql2)
Jul 20 08:28:59 pgsql1 patroni[7253]: 2022-07-20 08:28:59,896 INFO: no action. I am (pgsql1), a secondary, and following a leader (pgsql2)

и почему то роли, автоматом не создались , создал вручную после этого заработал кластер. 

root@pgsql1:~# sudo patronictl -c /etc/patroni.yml list
+--------+-------------+---------+---------+----+-----------+
| Member | Host        | Role    | State   | TL | Lag in MB |
+ Cluster: patroni (7122001137243157900) --+----+-----------+
| pgsql1 | 10.128.0.12 | Replica | running | 16 |         0 |
| pgsql2 | 10.128.0.14 | Leader  | running | 16 |           |
| pgsql3 | 10.128.0.13 | Replica | running | 16 |         0 |

И Лидер стал pgsql2


Изменил параметры кластера.

root@pgsql2:~# sudo patronictl -c /etc/patroni.yml edit-config
--- 
+++ 
@@ -2,7 +2,8 @@
 max_connections: 150
 maximum_lag_on_failover: 1048576
 postgresql:
+  parameters:
-  parameters: max_connections:150
+     max_connections: 150
   use_pg_rewind: true
 retry_timeout: 10
 ttl: 30

Apply these changes? [y/N]: y
Configuration changed
root@pgsql2:~# systemctl restart patroni
root@pgsql2:~# sudo -u postgres psql -h localhost
could not change directory to "/root": Permission denied
psql (14.4 (Ubuntu 14.4-1.pgdg20.04+1))
Type "help" for help.

postgres=# show max_connections;
 max_connections 
-----------------
 150
(1 row)


проверка отказаустойчивости кластера. 



root@pgsql1:~# sudo patronictl -c /etc/patroni.yml list
+--------+-------------+---------+---------+----+-----------+-----------------+
| Member | Host        | Role    | State   | TL | Lag in MB | Pending restart |
+ Cluster: patroni (7122001137243157900) --+----+-----------+-----------------+
| pgsql1 | 10.128.0.12 | Leader  | running | 18 |           | *               |
| pgsql2 | 10.128.0.14 | Replica | running | 18 |         0 |                 |
| pgsql3 | 10.128.0.13 | Replica | running | 18 |         0 |                 |
+--------+-------------+---------+---------+----+-----------+-----------------+
root@pgsql1:~# systemctl stop patroni

root@pgsql1:~# sudo patronictl -c /etc/patroni.yml list
+--------+-------------+---------+---------+----+-----------+-----------------+
| Member | Host        | Role    | State   | TL | Lag in MB | Pending restart |
+ Cluster: patroni (7122001137243157900) --+----+-----------+-----------------+
| pgsql1 | 10.128.0.12 | Replica | stopped |    |   unknown | *               |
| pgsql2 | 10.128.0.14 | Replica | running | 18 |         0 |                 |
| pgsql3 | 10.128.0.13 | Leader  | running | 19 |           |                 |

Видим что с начала pgsql1 был лидером, после остановки стал лидер pgsql3. 


PG-Probackup

root@pgsql3:~# sudo rm -rf /home/backups && sudo mkdir /home/backups && sudo chmod 777 /home/backups
root@pgsql3:~# echo "BACKUP_PATH=/home/backups/">>~/.bashrc
root@pgsql3:~# 
root@pgsql3:~# echo "export BACKUP_PATH">>~/.bashrc
root@pgsql3:~# cd $HOME
root@pgsql3:~# . .bashrc
root@pgsql3:~# echo $BACKUP_PATH
/home/backups/
root@pgsql3:~# pg_probackup-14 init
INFO: Backup catalog '/home/backups' successfully inited
root@pgsql3:~# cd $BACKUP_PATH
root@pgsql3:/home/backups# ls -l
total 8
drwx------ 2 root root 4096 Jul 20 09:16 backups
drwx------ 2 root root 4096 Jul 20 09:16 wal



root@pgsql3:~# pg_probackup-14 backup --instance 'main' -b FULL --stream --temp-slot -h localhost -U backup -d test -p 5432
INFO: Backup start, pg_probackup version: 2.5.5, instance: main, backup ID: RFBC2J, backup mode: FULL, wal mode: STREAM, remote: false, compress-algorithm: none, compress-level: 1
INFO: wait for pg_start_backup()
INFO: Wait for WAL segment /home/backups/backups/main/RFBC2J/database/pg_wal/000000130000000000000005 to be streamed
WARNING: Skip hidden file: '/var/lib/postgresql/14/main/.s.PGSQL.5432.lock'
WARNING: Skip hidden file: '/var/lib/postgresql/14/main/.s.PGSQL.5432'
INFO: PGDATA size: 34MB
INFO: Start transferring data files
INFO: Data files are transferred, time elapsed: 0
INFO: wait for pg_stop_backup()
INFO: pg_stop backup() successfully executed
INFO: Syncing backup files to disk
INFO: Backup files are synced, time elapsed: 2s
INFO: Validating backup RFBC2J
INFO: Backup RFBC2J data files are valid
INFO: Backup RFBC2J resident size: 50MB
INFO: Backup RFBC2J completed
root@pgsql3:~# pg_probackup-14 show

BACKUP INSTANCE 'main'
=================================================================================================================================
 Instance  Version  ID      Recovery Time           Mode  WAL Mode  TLI   Time  Data   WAL  Zratio  Start LSN  Stop LSN   Status 
=================================================================================================================================
 main      14       RFBC2J  2022-07-20 09:37:33+00  FULL  STREAM    19/0   13s  34MB  16MB    1.00  0/5000028  0/5009CC8  OK     
 main      ----     RFBBOE  ----                    FULL  STREAM    0/0      0     0     0    1.00  0/0        0/0        ERROR  
 main      ----     RFBBLH  ----                    FULL  STREAM    0/0      0     0     0    1.00  0/0        0/0        ERROR  
 main      ----     RFBBAC  ----                    FULL  STREAM    0/0      0     0     0    1.00  0/0        0/0        ERROR  
root@pgsql3:~# pg_probackup-14 backup --instance 'main' -b DELTA --stream --temp-slot -h localhost -U backup -d test -p 5432
INFO: Backup start, pg_probackup version: 2.5.5, instance: main, backup ID: RFBC3I, backup mode: DELTA, wal mode: STREAM, remote: false, compress-algorithm: none, compress-level: 1
INFO: wait for pg_start_backup()
INFO: Parent backup: RFBC2J
INFO: Wait for WAL segment /home/backups/backups/main/RFBC3I/database/pg_wal/000000130000000000000007 to be streamed
WARNING: Skip hidden file: '/var/lib/postgresql/14/main/.s.PGSQL.5432.lock'
WARNING: Skip hidden file: '/var/lib/postgresql/14/main/.s.PGSQL.5432'
INFO: PGDATA size: 34MB
INFO: Start transferring data files
INFO: Data files are transferred, time elapsed: 0
INFO: wait for pg_stop_backup()
INFO: pg_stop backup() successfully executed
INFO: Syncing backup files to disk
INFO: Backup files are synced, time elapsed: 0
INFO: Validating backup RFBC3I
INFO: Backup RFBC3I data files are valid
INFO: Backup RFBC3I resident size: 32MB
INFO: Backup RFBC3I completed
root@pgsql3:~# pg_probackup-14 show

BACKUP INSTANCE 'main'
====================================================================================================================================
 Instance  Version  ID      Recovery Time           Mode   WAL Mode  TLI    Time   Data   WAL  Zratio  Start LSN  Stop LSN   Status 
====================================================================================================================================
 main      14       RFBC3I  2022-07-20 09:38:07+00  DELTA  STREAM    19/19    8s  200kB  32MB    1.00  0/7000028  0/7000168  OK     
 main      14       RFBC2J  2022-07-20 09:37:33+00  FULL   STREAM    19/0    13s   34MB  16MB    1.00  0/5000028  0/5009CC8  OK     
 main      ----     RFBBOE  ----                    FULL   STREAM    0/0       0      0     0    1.00  0/0        0/0        ERROR  
 main      ----     RFBBLH  ----                    FULL   STREAM    0/0       0      0     0    1.00  0/0        0/0        ERROR  
 main      ----     RFBBAC  ----                    FULL   STREAM    0/0       0      0     0    1.00  0/0        0/0        ERROR  


дальше pg_bouncer установку показывать смысла нет, настроил с первого раза. 

psql (14.4 (Ubuntu 14.4-1.pgdg20.04+1))
Type "help" for help.

postgres=# select usename,passwd from pg_shadow;
   usename   |                                                                passwd                                                                 
-------------+---------------------------------------------------------------------------------------------------------------------------------------
 postgres    | SCRAM-SHA-256$4096:RxwCOH5yjzSO1KhD2VI3sA==$Knbfi5CISSSL/z2ozl7lJSB9ujb/Srka1piTk551jgY=:vK82Bkax02Cn4yeQ4M+ll8WCC+E13U76tjjPd6Y2hZ8=
 replicator  | SCRAM-SHA-256$4096:dnpNd14XSS2zWGLOUH03Ug==$L9iwUWHCaSmhEe2XcVOOMjgooThcf15+SEfKngrk22w=:ba+x3fypT7q9pzCJRv6shs5/YOBla+/uEdI8xWMeco8=
 rewind_user | SCRAM-SHA-256$4096:sTcQHH/7qENEAAxgcuvizg==$a/Z9NxsuxG4d4EkdjVLU6FJE9hEh0wSHwWl/YO9yxj8=:JRvex0PP7PlWPJ6lxuuT3ctkrR3yJC9Gz7auWK6Yn3c=
 backup      | SCRAM-SHA-256$4096:U8imsdfFNkFMFnQCTC9Vpw==$nhrlhNU1rboCcAXvSWfuZV+cheFH0p8sSnWOZ4y/3Os=:2htxwh+bm3A5Ib7aWgWXTI2NzgcUULgKLJjnhM8NcXo=
(4 rows)

postgres=# \q
root@pgsql3:~# sudo nano /etc/pgbouncer/pgbouncer.ini
root@pgsql3:~# sudo nano /etc/pgbouncer/userlist.txt
root@pgsql3:~# systemctl restart pgbouncer
root@pgsql3:~# systemctl status pgbouncer
● pgbouncer.service - pgbouncer PostgreSQL connection pooler
     Loaded: loaded (/lib/systemd/system/pgbouncer.service; enabled; vendor preset: enabled)
     Active: active (running) since Wed 2022-07-20 16:55:45 UTC; 11s ago
   Main PID: 1216 (pgbouncer)
      Tasks: 2 (limit: 2359)
     Memory: 1.1M
     CGroup: /system.slice/pgbouncer.service
             └─1216 /usr/sbin/pgbouncer /etc/pgbouncer/pgbouncer.ini

Jul 20 16:55:45 pgsql3 systemd[1]: Starting pgbouncer PostgreSQL connection pooler...
Jul 20 16:55:45 pgsql3 pgbouncer[1216]: kernel file descriptor limit: 1024 (hard: 524288); max_client_conn: 100, max expected fd use: 152
Jul 20 16:55:45 pgsql3 pgbouncer[1216]: listening on 0.0.0.0:6432
Jul 20 16:55:45 pgsql3 pgbouncer[1216]: listening on [::]:6432
Jul 20 16:55:45 pgsql3 pgbouncer[1216]: listening on unix:/tmp/.s.PGSQL.6432
Jul 20 16:55:45 pgsql3 pgbouncer[1216]: process up: PgBouncer 1.17.0, libevent 2.1.11-stable (epoll), adns: c-ares 1.15.0, tls: OpenSSL 1.1.1f  31 Mar 2020
Jul 20 16:55:45 pgsql3 systemd[1]: Started pgbouncer PostgreSQL connection pooler.
root@pgsql3:~# sudo -u postgres psql -p 6432 -h127.0.0.1 test
could not change directory to "/root": Permission denied
Password for user postgres: 
psql (14.4 (Ubuntu 14.4-1.pgdg20.04+1))
Type "help" for help.

test=# 

проверили работает. 

дальше проверяем 

root@pgsql3:~# sudo -u postgres psql -p 6432 -h127.0.0.1 test
could not change directory to "/root": Permission denied
Password for user postgres: 
psql (14.4 (Ubuntu 14.4-1.pgdg20.04+1))
Type "help" for help.

test=# \l
                              List of databases
   Name    |  Owner   | Encoding | Collate |  Ctype  |   Access privileges   
-----------+----------+----------+---------+---------+-----------------------
 postgres  | postgres | UTF8     | C.UTF-8 | C.UTF-8 | 
 template0 | postgres | UTF8     | C.UTF-8 | C.UTF-8 | =c/postgres          +
           |          |          |         |         | postgres=CTc/postgres
 template1 | postgres | UTF8     | C.UTF-8 | C.UTF-8 | =c/postgres          +
           |          |          |         |         | postgres=CTc/postgres
 test      | postgres | UTF8     | C.UTF-8 | C.UTF-8 | 
(4 rows)

test=# create database pgbouncer;
CREATE DATABASE
создал базу в мастере. 
проверяю в реплике. 

root@pgsql1:~# sudo -u postgres psql -p 6432 -h 127.0.0.1 test
could not change directory to "/root": Permission denied
Password for user postgres: 
psql (14.4 (Ubuntu 14.4-1.pgdg20.04+1))
Type "help" for help.

test=# \l
                              List of databases
   Name    |  Owner   | Encoding | Collate |  Ctype  |   Access privileges   
-----------+----------+----------+---------+---------+-----------------------
 postgres  | postgres | UTF8     | C.UTF-8 | C.UTF-8 | 
 template0 | postgres | UTF8     | C.UTF-8 | C.UTF-8 | =c/postgres          +
           |          |          |         |         | postgres=CTc/postgres
 template1 | postgres | UTF8     | C.UTF-8 | C.UTF-8 | =c/postgres          +
           |          |          |         |         | postgres=CTc/postgres
 test      | postgres | UTF8     | C.UTF-8 | C.UTF-8 | 
(4 rows)

test=# create database pgbouncer;
ERROR:  cannot execute CREATE DATABASE in a read-only transaction
test=# \l
                              List of databases
   Name    |  Owner   | Encoding | Collate |  Ctype  |   Access privileges   
-----------+----------+----------+---------+---------+-----------------------
 pgbouncer | postgres | UTF8     | C.UTF-8 | C.UTF-8 | 
 postgres  | postgres | UTF8     | C.UTF-8 | C.UTF-8 | 
 template0 | postgres | UTF8     | C.UTF-8 | C.UTF-8 | =c/postgres          +
           |          |          |         |         | postgres=CTc/postgres
 template1 | postgres | UTF8     | C.UTF-8 | C.UTF-8 | =c/postgres          +
           |          |          |         |         | postgres=CTc/postgres
 test      | postgres | UTF8     | C.UTF-8 | C.UTF-8 | 
(5 rows)

видим что сервер реплика, и база тоже создалась тут. 

админка pg_bouncer 

root@pgsql3:~# sudo -u postgres psql -p 6432 pgbouncer -h localhost
could not change directory to "/root": Permission denied
Password for user postgres: 
psql (14.4 (Ubuntu 14.4-1.pgdg20.04+1), server 1.17.0/bouncer)
Type "help" for help.

pgbouncer=# show databases;
   name    |   host    | port | database  | force_user | pool_size | min_pool_size | reserve_pool | pool_mode | max_connections | current_connections | paused | disabled 
-----------+-----------+------+-----------+------------+-----------+---------------+--------------+-----------+-----------------+---------------------+--------+----------
 pgbouncer |           | 6432 | pgbouncer | pgbouncer  |         2 |             0 |            0 | statement |               0 |                   0 |      0 |        0
 test      | 127.0.0.1 | 5432 | test      |            |        20 |             0 |            0 |           |               0 |                   1 |      0 |        0
(2 rows)


HA PROXY 

dimash9527@mytest:~$ ERROR: (gcloud.beta.compute.instances.create) Could not fetch resource:
 - Quota 'IN_USE_ADDRESSES' exceeded.  Limit: 8.0 in region us-central1.

Created [https://www.googleapis.com/compute/beta/projects/postgres-27011995/zones/us-central1-a/instances/proxy2].
NAME    ZONE           MACHINE_TYPE  PREEMPTIBLE  INTERNAL_IP  EXTERNAL_IP   STATUS
proxy2  us-central1-a  e2-small                   10.128.0.15  34.66.205.61  RUNNING

[1]-  Exit 1                  gcloud beta compute --project=postgres-27011995 instances create proxy$i --zone=us-central1-a --machine-type=e2-small --subnet=default --network-tier=PREMIUM --maintenance-policy=MIGRATE --service-account=444352908086-compute@developer.gserviceaccount.com --scopes=https://www.googleapis.com/auth/cloud-platform --image-family=ubuntu-2004-lts --image-project=ubuntu-os-cloud --boot-disk-size=10GB --boot-disk-type=pd-ssd --boot-disk-device-name=pgsql$i --no-shielded-secure-boot --shielded-vtpm --shielded-integrity-monitoring --reservation-affinity=any
[2]+  Done                    gcloud beta compute --project=postgres-27011995 instances create proxy$i --zone=us-central1-a --machine-type=e2-small --subnet=default --network-tier=PREMIUM --maintenance-policy=MIGRATE --service-account=444352908086-compute@developer.gserviceaccount.com --scopes=https://www.googleapis.com/auth/cloud-platform --image-family=ubuntu-2004-lts --image-project=ubuntu-os-cloud --boot-disk-size=10GB --boot-disk-type=pd-ssd --boot-disk-device-name=pgsql$i --no-shielded-secure-boot --shielded-vtpm --shielded-integrity-monitoring --reservation-affinity=any


root@proxy2:~# curl -v 10.128.0.13:8008/master
*   Trying 10.128.0.13:8008...
* TCP_NODELAY set
* Connected to 10.128.0.13 (10.128.0.13) port 8008 (#0)
> GET /master HTTP/1.1
> Host: 10.128.0.13:8008
> User-Agent: curl/7.68.0
> Accept: */*
> 
* Mark bundle as not supporting multiuse
* HTTP 1.0, assume close after body
< HTTP/1.0 200 OK
< Server: BaseHTTP/0.6 Python/3.8.10
< Date: Wed, 20 Jul 2022 17:49:11 GMT
< Content-Type: application/json
< 
* Closing connection 0
{"state": "running", "postmaster_start_time": "2022-07-20 16:10:09.033335+00:00", "role": "master", "server_version": 140004, "xlog": {"location": 134222752}, "timeline": 20, "replication": [{"usename": "replicator", "application_name": "pgsql2", "client_addr": "10.128.0.14", "state": "streaming", "sync_state": "async", "sync_priority": 0}, {"usename": "replicator", "application_name": "pgsql1", "client_addr": "10.128.0.12", "state": "streaming", "sync_state": "async", "sync_priority": 0}], "dcs_last_seen": 1658339343, "database_system_identifier": "7122001137243157900", "patroni": {"version": "2.1.4", "scope": "patroni"}}root@proxy2:~# 

root@proxy2:~# psql -p 6432 -d test -h 10.128.0.13 -U postgres
Password for user postgres: 
psql (12.11 (Ubuntu 12.11-0ubuntu0.20.04.1), server 14.4 (Ubuntu 14.4-1.pgdg20.04+1))
WARNING: psql major version 12, server major version 14.
         Some psql features might not work.
Type "help" for help.

test=# \l
                              List of databases
   Name    |  Owner   | Encoding | Collate |  Ctype  |   Access privileges   
-----------+----------+----------+---------+---------+-----------------------
 pgbouncer | postgres | UTF8     | C.UTF-8 | C.UTF-8 | 
 postgres  | postgres | UTF8     | C.UTF-8 | C.UTF-8 | 
 template0 | postgres | UTF8     | C.UTF-8 | C.UTF-8 | =c/postgres          +
           |          |          |         |         | postgres=CTc/postgres
 template1 | postgres | UTF8     | C.UTF-8 | C.UTF-8 | =c/postgres          +
           |          |          |         |         | postgres=CTc/postgres
 test      | postgres | UTF8     | C.UTF-8 | C.UTF-8 | 
(5 rows)

test=# create database haproxy;
CREATE DATABASE





root@proxy2:~# sudo systemctl status haproxy.service
● haproxy.service - HAProxy Load Balancer
     Loaded: loaded (/lib/systemd/system/haproxy.service; enabled; vendor preset: enabled)
     Active: active (running) since Wed 2022-07-20 18:08:55 UTC; 9s ago
       Docs: man:haproxy(1)
             file:/usr/share/doc/haproxy/configuration.txt.gz
   Main PID: 5523 (haproxy)
      Tasks: 3 (limit: 2359)
     Memory: 72.5M
     CGroup: /system.slice/haproxy.service
             ├─5523 /usr/sbin/haproxy -x /run/haproxy/admin.sock -Ws -f /etc/haproxy/haproxy.cfg -p /run/hapro>
             └─5526 /usr/sbin/haproxy -Ws -f /etc/haproxy/haproxy.cfg -p /run/haproxy.pid -S /run/haproxy-mast>

Jul 20 18:08:55 proxy2 systemd[1]: Starting HAProxy Load Balancer...
Jul 20 18:08:55 proxy2 haproxy[5523]: [NOTICE]   (5523) : haproxy version is 2.5.7-1ppa1~focal
Jul 20 18:08:55 proxy2 haproxy[5523]: [NOTICE]   (5523) : path to executable is /usr/sbin/haproxy
Jul 20 18:08:55 proxy2 haproxy[5523]: [WARNING]  (5523) : config : parsing [/etc/haproxy/haproxy.cfg:23] : 'op>
Jul 20 18:08:55 proxy2 haproxy[5523]: [WARNING]  (5523) : config : parsing [/etc/haproxy/haproxy.cfg:23] : 'op>
Jul 20 18:08:55 proxy2 haproxy[5523]: [WARNING]  (5523) : config : proxy 'postgres_read' uses http-check rules>
Jul 20 18:08:55 proxy2 haproxy[5523]: [NOTICE]   (5523) : New worker (5526) forked
Jul 20 18:08:55 proxy2 haproxy[5523]: [NOTICE]   (5523) : Loading success.
Jul 20 18:08:55 proxy2 systemd[1]: Started HAProxy Load Balancer.

root@proxy2:~# sudo cat /var/log/haproxy.log
Jul 20 18:08:55 proxy2 haproxy[2298]: [NOTICE]   (2298) : haproxy version is 2.5.7-1ppa1~focal
Jul 20 18:08:55 proxy2 haproxy[2298]: [NOTICE]   (2298) : path to executable is /usr/sbin/haproxy
Jul 20 18:08:55 proxy2 haproxy[2298]: [WARNING]  (2298) : Exiting Master process...
Jul 20 18:08:55 proxy2 haproxy[2298]: [ALERT]    (2298) : Current worker (2300) exited with code 143 (Terminated)
Jul 20 18:08:55 proxy2 haproxy[2298]: [WARNING]  (2298) : All workers exited. Exiting... (0)
Jul 20 18:08:55 proxy2 haproxy[5523]: [NOTICE]   (5523) : haproxy version is 2.5.7-1ppa1~focal
Jul 20 18:08:55 proxy2 haproxy[5523]: [NOTICE]   (5523) : path to executable is /usr/sbin/haproxy
Jul 20 18:08:55 proxy2 haproxy[5523]: [WARNING]  (5523) : config : parsing [/etc/haproxy/haproxy.cfg:23] : 'option httplog' not usable with proxy 'postgres_write' (needs 'mode http'). Falling back to 'option tcplog'.
Jul 20 18:08:55 proxy2 haproxy[5523]: [WARNING]  (5523) : config : parsing [/etc/haproxy/haproxy.cfg:23] : 'option httplog' not usable with proxy 'postgres_read' (needs 'mode http'). Falling back to 'option tcplog'.
Jul 20 18:08:55 proxy2 haproxy[5523]: [WARNING]  (5523) : config : proxy 'postgres_read' uses http-check rules without 'option httpchk', so the rules are ignored.
Jul 20 18:08:55 proxy2 haproxy[5523]: [NOTICE]   (5523) : New worker (5526) forked
Jul 20 18:08:55 proxy2 haproxy[5523]: [NOTICE]   (5523) : Loading success.
Jul 20 18:09:05 proxy2 haproxy[5526]: [WARNING]  (5526) : Server postgres_write/pgsql1 is DOWN, reason: Layer4 timeout, check duration: 10002ms. 2 active and 0 backup servers left. 0 sessions active, 0 requeued, 0 remaining in queue.

root@proxy2:~# psql -h localhost -d test -U postgres -p 5432
Password for user postgres: 
psql (12.11 (Ubuntu 12.11-0ubuntu0.20.04.1), server 14.4 (Ubuntu 14.4-1.pgdg20.04+1))
WARNING: psql major version 12, server major version 14.
         Some psql features might not work.
Type "help" for help.

test=# \l
                              List of databases
   Name    |  Owner   | Encoding | Collate |  Ctype  |   Access privileges   
-----------+----------+----------+---------+---------+-----------------------
 haproxy   | postgres | UTF8     | C.UTF-8 | C.UTF-8 | 
 pgbouncer | postgres | UTF8     | C.UTF-8 | C.UTF-8 | 
 postgres  | postgres | UTF8     | C.UTF-8 | C.UTF-8 | 
 template0 | postgres | UTF8     | C.UTF-8 | C.UTF-8 | =c/postgres          +
           |          |          |         |         | postgres=CTc/postgres
 template1 | postgres | UTF8     | C.UTF-8 | C.UTF-8 | =c/postgres          +
           |          |          |         |         | postgres=CTc/postgres
 test      | postgres | UTF8     | C.UTF-8 | C.UTF-8 | 
(6 rows)

все работает) 

