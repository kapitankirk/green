Установка PostgreSQL думаю смысла особого нет, покажу версию которую поставил. 
root@test2:~# sudo -u postgres psql -c "SELECT version();"
could not change directory to "/root": Permission denied
                                                              version                                                              
-----------------------------------------------------------------------------------------------------------------------------------
 PostgreSQL 14.4 (Ubuntu 14.4-1.pgdg20.04+1) on x86_64-pc-linux-gnu, compiled by gcc (Ubuntu 9.4.0-1ubuntu1~20.04.1) 9.4.0, 64-bit
(1 row)
root@test2:~# sudo -u postgres pg_lsclusters
Ver Cluster Port Status Owner    Data directory              Log file
14  main    5432 online postgres /var/lib/postgresql/14/main /var/log/postgresql/postgresql-14-main.log
root@test2:~# sudo su - postgres
postgres@test2:~$ psql
psql (14.4 (Ubuntu 14.4-1.pgdg20.04+1))
Type "help" for help.

postgres=# \l
                              List of databases
   Name    |  Owner   | Encoding | Collate |  Ctype  |   Access privileges   
-----------+----------+----------+---------+---------+-----------------------
 postgres  | postgres | UTF8     | C.UTF-8 | C.UTF-8 | 
 template0 | postgres | UTF8     | C.UTF-8 | C.UTF-8 | =c/postgres          +
           |          |          |         |         | postgres=CTc/postgres
 template1 | postgres | UTF8     | C.UTF-8 | C.UTF-8 | =c/postgres          +
           |          |          |         |         | postgres=CTc/postgres
(3 rows)

postgres=#  create table test(c1 text); 
CREATE TABLE
postgres=# insert into test values('1');
INSERT 0 1
postgres=# \q
postgres@test2:~$ sudo -u postgres pg_ctlcluster 14 main stop
postgres is not in the sudoers file.  This incident will be reported.
postgres@test2:~$ exit
logout
root@test2:~# sudo -u postgres pg_ctlcluster 14 main stop
Warning: stopping the cluster using pg_ctlcluster will mark the systemd unit as failed. Consider using systemctl:
  sudo systemctl stop postgresql@14-main
root@test2:~# sudo systemctl stop postgresql@14-main
root@test2:~# sudo systemctl status postgresql@14-main
● postgresql@14-main.service - PostgreSQL Cluster 14-main
     Loaded: loaded (/lib/systemd/system/postgresql@.service; enabled-runtime; vendor preset: enabled)
     Active: failed (Result: exit-code) since Mon 2022-06-20 11:07:43 UTC; 45s ago
    Process: 5089 ExecStop=/usr/bin/pg_ctlcluster --skip-systemctl-redirect -m fast 14-main stop (code=exited, status=2)
   Main PID: 3838 (code=exited, status=0/SUCCESS)

Jun 20 11:01:20 test2 systemd[1]: Starting PostgreSQL Cluster 14-main...
Jun 20 11:01:23 test2 systemd[1]: Started PostgreSQL Cluster 14-main.
Jun 20 11:07:43 test2 postgresql@14-main[5089]: Cluster is not running.
Jun 20 11:07:43 test2 systemd[1]: postgresql@14-main.service: Control process exited, code=exited, status=2/INVALIDARGUMENT
Jun 20 11:07:43 test2 systemd[1]: postgresql@14-main.service: Failed with result 'exit-code'.
Монтирование диска к инстансу. 
root@test2:~# sudo parted -l | grep Error
Error: /dev/sdb: unrecognised disk label
root@test2:~# lsblk
NAME    MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
loop0     7:0    0  55.5M  1 loop /snap/core18/2409
loop1     7:1    0  61.9M  1 loop /snap/core20/1518
loop2     7:2    0 297.2M  1 loop /snap/google-cloud-cli/42
loop3     7:3    0  67.8M  1 loop /snap/lxd/22753
loop4     7:4    0    47M  1 loop /snap/snapd/16010
sda       8:0    0    10G  0 disk 
├─sda1    8:1    0   9.9G  0 part /
├─sda14   8:14   0     4M  0 part 
└─sda15   8:15   0   106M  0 part /boot/efi
sdb       8:16   0    10G  0 disk 
root@test2:~# lsblk
NAME    MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
loop0     7:0    0  55.5M  1 loop /snap/core18/2409
loop1     7:1    0  61.9M  1 loop /snap/core20/1518
loop2     7:2    0 297.2M  1 loop /snap/google-cloud-cli/42
loop3     7:3    0  67.8M  1 loop /snap/lxd/22753
loop4     7:4    0    47M  1 loop /snap/snapd/16010
sda       8:0    0    10G  0 disk 
├─sda1    8:1    0   9.9G  0 part /
├─sda14   8:14   0     4M  0 part 
└─sda15   8:15   0   106M  0 part /boot/efi
sdb       8:16   0    10G  0 disk 
root@test2:~# sudo parted -l | grep Error
Error: /dev/sdb: unrecognised disk label
root@test2:~# lsblk
NAME    MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
loop0     7:0    0  55.5M  1 loop /snap/core18/2409
loop1     7:1    0  61.9M  1 loop /snap/core20/1518
loop2     7:2    0 297.2M  1 loop /snap/google-cloud-cli/42
loop3     7:3    0  67.8M  1 loop /snap/lxd/22753
loop4     7:4    0    47M  1 loop /snap/snapd/16010
sda       8:0    0    10G  0 disk 
├─sda1    8:1    0   9.9G  0 part /
├─sda14   8:14   0     4M  0 part 
└─sda15   8:15   0   106M  0 part /boot/efi
sdb       8:16   0    10G  0 disk 
root@test2:~# sudo parted /dev/sdb mklabel gpt
Information: You may need to update /etc/fstab.

root@test2:~# lsblk
NAME    MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
loop0     7:0    0  55.5M  1 loop /snap/core18/2409
loop1     7:1    0  61.9M  1 loop /snap/core20/1518
loop2     7:2    0 297.2M  1 loop /snap/google-cloud-cli/42
loop3     7:3    0  67.8M  1 loop /snap/lxd/22753
loop4     7:4    0    47M  1 loop /snap/snapd/16010
sda       8:0    0    10G  0 disk 
├─sda1    8:1    0   9.9G  0 part /
├─sda14   8:14   0     4M  0 part 
└─sda15   8:15   0   106M  0 part /boot/efi
sdb       8:16   0    10G  0 disk 
root@test2:~# sudo parted -a opt /dev/sdb mkpart primary ext4 0% 100%
Information: You may need to update /etc/fstab.

root@test2:~# lsblk                                                       
NAME    MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
loop0     7:0    0  55.5M  1 loop /snap/core18/2409
loop1     7:1    0  61.9M  1 loop /snap/core20/1518
loop2     7:2    0 297.2M  1 loop /snap/google-cloud-cli/42
loop3     7:3    0  67.8M  1 loop /snap/lxd/22753
loop4     7:4    0    47M  1 loop /snap/snapd/16010
sda       8:0    0    10G  0 disk 
├─sda1    8:1    0   9.9G  0 part /
├─sda14   8:14   0     4M  0 part 
└─sda15   8:15   0   106M  0 part /boot/efi
sdb       8:16   0    10G  0 disk 
└─sdb1    8:17   0    10G  0 part 
root@test2:~# sudo mkfs.ext4 -L datapartition /dev/sdb1
mke2fs 1.45.5 (07-Jan-2020)
Discarding device blocks: done                            
Creating filesystem with 2620928 4k blocks and 655360 inodes
Filesystem UUID: da3c06ef-9535-4c45-aab1-7e56a5ef448d
Superblock backups stored on blocks: 
        32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632

Allocating group tables: done                            
Writing inode tables: done                            
Creating journal (16384 blocks): done
Writing superblocks and filesystem accounting information: done 

root@test2:~# sudo lsblk --fs
NAME    FSTYPE   LABEL           UUID                                 FSAVAIL FSUSE% MOUNTPOINT
loop0   squashfs                                                            0   100% /snap/core18/2409
loop1   squashfs                                                            0   100% /snap/core20/1518
loop2   squashfs                                                            0   100% /snap/google-cloud-cli/42
loop3   squashfs                                                            0   100% /snap/lxd/22753
loop4   squashfs                                                            0   100% /snap/snapd/16010
sda                                                                                  
├─sda1  ext4     cloudimg-rootfs 764302ac-b482-4bdc-9f49-c724891de3dc    7.4G    22% /
├─sda14                                                                              
└─sda15 vfat     UEFI            15F1-B015                              99.2M     5% /boot/efi
sdb                                                                                  
└─sdb1  ext4     datapartition   da3c06ef-9535-4c45-aab1-7e56a5ef448d                
root@test2:~# sudo mkdir -p /mnt/data
root@test2:~# sudo nano /etc/fstab
root@test2:~# man fstab
root@test2:~# man ext4
root@test2:~# 
root@test2:~# sudo mount -a
root@test2:~# sudo nano /etc/fstab
root@test2:~# sudo mount -a
root@test2:~# df -h -x tmpfs -x devtmpfs
Filesystem      Size  Used Avail Use% Mounted on
/dev/root       9.6G  2.1G  7.5G  22% /
/dev/loop0       56M   56M     0 100% /snap/core18/2409
/dev/loop1       62M   62M     0 100% /snap/core20/1518
/dev/loop2      298M  298M     0 100% /snap/google-cloud-cli/42
/dev/loop3       68M   68M     0 100% /snap/lxd/22753
/dev/loop4       47M   47M     0 100% /snap/snapd/16010
/dev/sda15      105M  5.2M  100M   5% /boot/efi
/dev/sdb1       9.8G   37M  9.3G   1% /mnt/data

после ребута. 

Welcome to Ubuntu 20.04.4 LTS (GNU/Linux 5.13.0-1031-gcp x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Mon Jun 20 12:00:30 UTC 2022

  System load:  0.11              Processes:             119
  Usage of /:   21.8% of 9.52GB   Users logged in:       0
  Memory usage: 5%                IPv4 address for ens4: 10.128.0.3
  Swap usage:   0%


12 updates can be applied immediately.
7 of these updates are standard security updates.

To see these additional updates run: apt list --upgradable


Last login: Mon Jun 20 10:31:06 2022 from 35.235.244.34
dimash9527@test2:~$ sudo su - root
root@test2:~# df -h -x tmpfs -x devtmpfs
Filesystem      Size  Used Avail Use% Mounted on
/dev/root       9.6G  2.1G  7.5G  22% /
/dev/loop0       56M   56M     0 100% /snap/core18/2409
/dev/loop1       62M   62M     0 100% /snap/core20/1518
/dev/loop2      298M  298M     0 100% /snap/google-cloud-cli/42
/dev/loop3       68M   68M     0 100% /snap/lxd/22753
/dev/loop4       47M   47M     0 100% /snap/snapd/16010
/dev/sdb1       9.8G   37M  9.3G   1% /mnt/data
/dev/sda15      105M  5.2M  100M   5% /boot/efi

видимо что диск /dev/sdb1 монтирован на /mnt/data

root@test2:~# systemctl start postgresql-14
Failed to start postgresql-14.service: Unit postgresql-14.service not found.
root@test2:~# systemctl start postgresql
root@test2:~# systemctl status postgresql
● postgresql.service - PostgreSQL RDBMS
     Loaded: loaded (/lib/systemd/system/postgresql.service; enabled; vendor preset: enabled)
     Active: active (exited) since Mon 2022-06-20 11:57:29 UTC; 16h ago
   Main PID: 815 (code=exited, status=0/SUCCESS)
      Tasks: 0 (limit: 4696)
     Memory: 0B
     CGroup: /system.slice/postgresql.service

Jun 20 11:57:27 test2 systemd[1]: Starting PostgreSQL RDBMS...
Jun 20 11:57:29 test2 systemd[1]: Finished PostgreSQL RDBMS.
root@test2:~# sudo su - postgres psql
/usr/bin/psql: line 19: use: command not found
/usr/bin/psql: line 20: use: command not found
/usr/bin/psql: line 21: use: command not found
/usr/bin/psql: line 22: use: command not found
/usr/bin/psql: psql: line 24: syntax error near unexpected token `$version,'
/usr/bin/psql: psql: line 24: `my ($version, $cluster);'
root@test2:~# su - postgres
postgres@test2:~$ psql
psql: error: connection to server on socket "/var/run/postgresql/.s.PGSQL.5432" failed: No such file or directory
        Is the server running locally and accepting connections on that socket?
postgres@test2:~$ 

Службу получилось запустить , но не может зайти в psql. видимо конфигурационный файлик поменять. 

Зашёл в /etc/postgresql/14/main postgresql.conf  поменял местоположение директории на /mnt/data/14/main
после этого ребутнул службу postgresql
и снизу вот результат , что данные в таблице есть и psql работает. 


root@test2:~# netstat -tunlp
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 127.0.0.53:53           0.0.0.0:*               LISTEN      538/systemd-resolve 
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      814/sshd: /usr/sbin 
tcp6       0      0 :::22                   :::*                    LISTEN      814/sshd: /usr/sbin 
udp        0      0 127.0.0.53:53           0.0.0.0:*                           538/systemd-resolve 
udp        0      0 10.128.0.3:68           0.0.0.0:*                           534/systemd-network 
udp        0      0 127.0.0.1:323           0.0.0.0:*                           585/chronyd         
udp6       0      0 ::1:323                 :::*                                585/chronyd         
root@test2:~# mc

root@test2:~# systemctl restart postgresql
root@test2:~# systemctl status postgresql
● postgresql.service - PostgreSQL RDBMS
     Loaded: loaded (/lib/systemd/system/postgresql.service; enabled; vendor preset: enabled)
     Active: active (exited) since Tue 2022-06-21 04:32:50 UTC; 6s ago
    Process: 5469 ExecStart=/bin/true (code=exited, status=0/SUCCESS)
   Main PID: 5469 (code=exited, status=0/SUCCESS)

Jun 21 04:32:50 test2 systemd[1]: Starting PostgreSQL RDBMS...
Jun 21 04:32:50 test2 systemd[1]: Finished PostgreSQL RDBMS.
root@test2:~# ^C
root@test2:~# netstat -tunlp
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 127.0.0.53:53           0.0.0.0:*               LISTEN      538/systemd-resolve 
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      814/sshd: /usr/sbin 
tcp        0      0 127.0.0.1:5432          0.0.0.0:*               LISTEN      5451/postgres       
tcp6       0      0 :::22                   :::*                    LISTEN      814/sshd: /usr/sbin 
udp        0      0 127.0.0.53:53           0.0.0.0:*                           538/systemd-resolve 
udp        0      0 10.128.0.3:68           0.0.0.0:*                           534/systemd-network 
udp        0      0 127.0.0.1:323           0.0.0.0:*                           585/chronyd         
udp6       0      0 ::1:323                 :::*                                585/chronyd         
root@test2:~# ^C
root@test2:~# su - postgres
postgres@test2:~$ psql
psql (14.4 (Ubuntu 14.4-1.pgdg20.04+1))
Type "help" for help.

postgres=# select * from test;
 c1 
----
 1
(1 row)

postgres=# 

