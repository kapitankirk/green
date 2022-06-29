Welcome to Ubuntu 20.04.4 LTS (GNU/Linux 5.13.0-1033-gcp x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Wed Jun 29 04:12:49 UTC 2022

  System load:  0.73              Processes:             116
  Usage of /:   18.2% of 9.52GB   Users logged in:       0
  Memory usage: 6%                IPv4 address for ens4: 10.128.0.6
  Swap usage:   0%

1 update can be applied immediately.
To see these additional updates run: apt list --upgradable


The list of available updates is more than a week old.
To check for new updates run: sudo apt update


The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

dimash9527@test5:~$ sudo su - root
root@test5:~# apt-get update
Hit:1 http://us-central1.gce.archive.ubuntu.com/ubuntu focal InRelease
Get:2 http://us-central1.gce.archive.ubuntu.com/ubuntu focal-updates InRelease [114 kB]
Get:3 http://us-central1.gce.archive.ubuntu.com/ubuntu focal-backports InRelease [108 kB]
Get:4 http://us-central1.gce.archive.ubuntu.com/ubuntu focal/universe amd64 Packages [8628 kB]
Get:5 http://security.ubuntu.com/ubuntu focal-security InRelease [114 kB]
Get:6 http://us-central1.gce.archive.ubuntu.com/ubuntu focal/universe Translation-en [5124 kB]
Get:7 http://us-central1.gce.archive.ubuntu.com/ubuntu focal/universe amd64 c-n-f Metadata [265 kB]
Get:8 http://us-central1.gce.archive.ubuntu.com/ubuntu focal/multiverse amd64 Packages [144 kB]
Get:9 http://us-central1.gce.archive.ubuntu.com/ubuntu focal/multiverse Translation-en [104 kB]
Get:10 http://us-central1.gce.archive.ubuntu.com/ubuntu focal/multiverse amd64 c-n-f Metadata [9136 B]
Get:11 http://us-central1.gce.archive.ubuntu.com/ubuntu focal-updates/main amd64 Packages [1935 kB]
Get:12 http://us-central1.gce.archive.ubuntu.com/ubuntu focal-updates/main Translation-en [350 kB]
Get:13 http://us-central1.gce.archive.ubuntu.com/ubuntu focal-updates/main amd64 c-n-f Metadata [15.6 kB]
Get:14 http://us-central1.gce.archive.ubuntu.com/ubuntu focal-updates/restricted amd64 Packages [1119 kB]
Get:15 http://us-central1.gce.archive.ubuntu.com/ubuntu focal-updates/restricted Translation-en [159 kB]
Get:16 http://us-central1.gce.archive.ubuntu.com/ubuntu focal-updates/restricted amd64 c-n-f Metadata [592 B]
Get:17 http://us-central1.gce.archive.ubuntu.com/ubuntu focal-updates/universe amd64 Packages [924 kB]
Get:18 http://us-central1.gce.archive.ubuntu.com/ubuntu focal-updates/universe Translation-en [208 kB]
Get:19 http://us-central1.gce.archive.ubuntu.com/ubuntu focal-updates/universe amd64 c-n-f Metadata [20.9 kB]
Get:20 http://us-central1.gce.archive.ubuntu.com/ubuntu focal-updates/multiverse amd64 Packages [24.4 kB]
Get:21 http://us-central1.gce.archive.ubuntu.com/ubuntu focal-updates/multiverse Translation-en [7336 B]
Get:22 http://us-central1.gce.archive.ubuntu.com/ubuntu focal-updates/multiverse amd64 c-n-f Metadata [596 B]
Get:23 http://us-central1.gce.archive.ubuntu.com/ubuntu focal-backports/main amd64 Packages [44.8 kB]
Get:24 http://us-central1.gce.archive.ubuntu.com/ubuntu focal-backports/main Translation-en [11.3 kB]
Get:25 http://us-central1.gce.archive.ubuntu.com/ubuntu focal-backports/main amd64 c-n-f Metadata [976 B]
Get:26 http://us-central1.gce.archive.ubuntu.com/ubuntu focal-backports/restricted amd64 c-n-f Metadata [116 B]
Get:27 http://us-central1.gce.archive.ubuntu.com/ubuntu focal-backports/universe amd64 Packages [23.7 kB]
Get:28 http://us-central1.gce.archive.ubuntu.com/ubuntu focal-backports/universe Translation-en [15.9 kB]
Get:29 http://us-central1.gce.archive.ubuntu.com/ubuntu focal-backports/universe amd64 c-n-f Metadata [860 B]
Get:30 http://us-central1.gce.archive.ubuntu.com/ubuntu focal-backports/multiverse amd64 c-n-f Metadata [116 B]
Get:31 http://security.ubuntu.com/ubuntu focal-security/main amd64 Packages [1583 kB]      
Get:32 http://security.ubuntu.com/ubuntu focal-security/main Translation-en [268 kB]
Get:33 http://security.ubuntu.com/ubuntu focal-security/main amd64 c-n-f Metadata [10.6 kB]
Get:34 http://security.ubuntu.com/ubuntu focal-security/restricted amd64 Packages [1042 kB]
Get:35 http://security.ubuntu.com/ubuntu focal-security/restricted Translation-en [148 kB]
Get:36 http://security.ubuntu.com/ubuntu focal-security/restricted amd64 c-n-f Metadata [572 B]
Get:37 http://security.ubuntu.com/ubuntu focal-security/universe amd64 Packages [708 kB]
Get:38 http://security.ubuntu.com/ubuntu focal-security/universe Translation-en [127 kB]
Get:39 http://security.ubuntu.com/ubuntu focal-security/universe amd64 c-n-f Metadata [14.6 kB]
Get:40 http://security.ubuntu.com/ubuntu focal-security/multiverse amd64 Packages [22.2 kB]
Get:41 http://security.ubuntu.com/ubuntu focal-security/multiverse Translation-en [5376 B]
Get:42 http://security.ubuntu.com/ubuntu focal-security/multiverse amd64 c-n-f Metadata [512 B]
Fetched 23.4 MB in 4s (5694 kB/s)                          
Reading package lists... Done
root@test5:~# apt-get upgrate
E: Invalid operation upgrate
root@test5:~# apt-get upgrade
Reading package lists... Done
Building dependency tree       
Reading state information... Done
Calculating upgrade... Done
The following packages were automatically installed and are no longer required:
  libatasmart4 libblockdev-fs2 libblockdev-loop2 libblockdev-part-err2 libblockdev-part2 libblockdev-swap2
  libblockdev-utils2 libblockdev2 libmm-glib0 libnspr4 libnss3 libnuma1 libparted-fs-resize0 libudisks2-0
  usb-modeswitch usb-modeswitch-data
Use 'apt autoremove' to remove them.
The following packages will be upgraded:
  curl libcurl3-gnutls libcurl4 libmm-glib0 libssl1.1 open-vm-tools openssl ubuntu-advantage-tools
8 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
5 standard security updates
Need to get 4298 kB of archives.
After this operation, 1061 kB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://us-central1.gce.archive.ubuntu.com/ubuntu focal-updates/main amd64 libssl1.1 amd64 1.1.1f-1ubuntu2.15 [1321 kB]
Get:2 http://us-central1.gce.archive.ubuntu.com/ubuntu focal-updates/universe amd64 open-vm-tools amd64 2:11.3.0-2ubuntu0~ubuntu20.04.2 [647 kB]
Get:3 http://us-central1.gce.archive.ubuntu.com/ubuntu focal-updates/main amd64 openssl amd64 1.1.1f-1ubuntu2.15 [623 kB]
Get:4 http://us-central1.gce.archive.ubuntu.com/ubuntu focal-updates/main amd64 ubuntu-advantage-tools amd64 27.9~20.04.1 [876 kB]
Get:5 http://us-central1.gce.archive.ubuntu.com/ubuntu focal-updates/main amd64 curl amd64 7.68.0-1ubuntu2.12 [161 kB]
Get:6 http://us-central1.gce.archive.ubuntu.com/ubuntu focal-updates/main amd64 libcurl4 amd64 7.68.0-1ubuntu2.12 [235 kB]
Get:7 http://us-central1.gce.archive.ubuntu.com/ubuntu focal-updates/main amd64 libcurl3-gnutls amd64 7.68.0-1ubuntu2.12 [232 kB]
Get:8 http://us-central1.gce.archive.ubuntu.com/ubuntu focal-updates/main amd64 libmm-glib0 amd64 1.18.6-1~ubuntu20.04.1 [203 kB]
Fetched 4298 kB in 0s (50.7 MB/s)
Preconfiguring packages ...
(Reading database ... 60915 files and directories currently installed.)
Preparing to unpack .../0-libssl1.1_1.1.1f-1ubuntu2.15_amd64.deb ...
Unpacking libssl1.1:amd64 (1.1.1f-1ubuntu2.15) over (1.1.1f-1ubuntu2.13) ...
Preparing to unpack .../1-open-vm-tools_2%3a11.3.0-2ubuntu0~ubuntu20.04.2_amd64.deb ...
Unpacking open-vm-tools (2:11.3.0-2ubuntu0~ubuntu20.04.2) over (2:11.0.5-4) ...
Preparing to unpack .../2-openssl_1.1.1f-1ubuntu2.15_amd64.deb ...
Unpacking openssl (1.1.1f-1ubuntu2.15) over (1.1.1f-1ubuntu2.13) ...
Preparing to unpack .../3-ubuntu-advantage-tools_27.9~20.04.1_amd64.deb ...
Unpacking ubuntu-advantage-tools (27.9~20.04.1) over (27.8~20.04.1) ...
Preparing to unpack .../4-curl_7.68.0-1ubuntu2.12_amd64.deb ...
Unpacking curl (7.68.0-1ubuntu2.12) over (7.68.0-1ubuntu2.11) ...
Preparing to unpack .../5-libcurl4_7.68.0-1ubuntu2.12_amd64.deb ...
Unpacking libcurl4:amd64 (7.68.0-1ubuntu2.12) over (7.68.0-1ubuntu2.11) ...
Preparing to unpack .../6-libcurl3-gnutls_7.68.0-1ubuntu2.12_amd64.deb ...
Unpacking libcurl3-gnutls:amd64 (7.68.0-1ubuntu2.12) over (7.68.0-1ubuntu2.11) ...
Preparing to unpack .../7-libmm-glib0_1.18.6-1~ubuntu20.04.1_amd64.deb ...
Unpacking libmm-glib0:amd64 (1.18.6-1~ubuntu20.04.1) over (1.16.6-2~20.04.1) ...
Setting up libssl1.1:amd64 (1.1.1f-1ubuntu2.15) ...
Setting up libcurl3-gnutls:amd64 (7.68.0-1ubuntu2.12) ...
Setting up open-vm-tools (2:11.3.0-2ubuntu0~ubuntu20.04.2) ...
Installing new version of config file /etc/vmware-tools/tools.conf.example ...
Installing new version of config file /etc/vmware-tools/vgauth.conf ...
Removing obsolete conffile /etc/vmware-tools/vm-support ...
Setting up libmm-glib0:amd64 (1.18.6-1~ubuntu20.04.1) ...
Setting up libcurl4:amd64 (7.68.0-1ubuntu2.12) ...
Setting up curl (7.68.0-1ubuntu2.12) ...
Setting up ubuntu-advantage-tools (27.9~20.04.1) ...
Installing new version of config file /etc/ubuntu-advantage/uaclient.conf ...
Created symlink /etc/systemd/system/multi-user.target.wants/ubuntu-advantage.service → /lib/systemd/system/ubuntu-advantage.service.
Setting up openssl (1.1.1f-1ubuntu2.15) ...
Processing triggers for systemd (245.4-4ubuntu3.17) ...
Processing triggers for man-db (2.9.1-1) ...
Processing triggers for libc-bin (2.31-0ubuntu9.9) ...
root@test5:~# sudo apt update && sudo apt-mark hold linux-image-5.11.0-1022-gcp && sudo DEBIAN_FRONTEND=noninteractive apt upgrade -y -q && sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list' && wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add - && sudo apt-get update && sudo DEBIAN_FRONTEND=noninteractive apt -y install postgresql-14
Hit:1 http://security.ubuntu.com/ubuntu focal-security InRelease
Hit:2 http://us-central1.gce.archive.ubuntu.com/ubuntu focal InRelease
Hit:3 http://us-central1.gce.archive.ubuntu.com/ubuntu focal-updates InRelease
Hit:4 http://us-central1.gce.archive.ubuntu.com/ubuntu focal-backports InRelease
Reading package lists... Done                        
Building dependency tree       
Reading state information... Done
All packages are up to date.
linux-image-5.11.0-1022-gcp set on hold.
Reading package lists...
Building dependency tree...
Reading state information...
Calculating upgrade...
The following packages were automatically installed and are no longer required:
  libatasmart4 libblockdev-fs2 libblockdev-loop2 libblockdev-part-err2 libblockdev-part2 libblockdev-swap2 libblockdev-utils2 libblockdev2 libmm-glib0 libnspr4 libnss3 libnuma1
  libparted-fs-resize0 libudisks2-0 usb-modeswitch usb-modeswitch-data
Use 'sudo apt autoremove' to remove them.
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
OK
Hit:1 http://us-central1.gce.archive.ubuntu.com/ubuntu focal InRelease
Hit:2 http://us-central1.gce.archive.ubuntu.com/ubuntu focal-updates InRelease                                                  
Hit:3 http://us-central1.gce.archive.ubuntu.com/ubuntu focal-backports InRelease                                                
Hit:4 http://security.ubuntu.com/ubuntu focal-security InRelease                                                                
Get:5 http://apt.postgresql.org/pub/repos/apt focal-pgdg InRelease [91.7 kB]
Get:6 http://apt.postgresql.org/pub/repos/apt focal-pgdg/main amd64 Packages [240 kB]
Fetched 331 kB in 1s (342 kB/s)   
Reading package lists... Done
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:
  libatasmart4 libblockdev-fs2 libblockdev-loop2 libblockdev-part-err2 libblockdev-part2 libblockdev-swap2 libblockdev-utils2 libblockdev2 libmm-glib0 libnspr4 libnss3 libnuma1
  libparted-fs-resize0 libudisks2-0 usb-modeswitch usb-modeswitch-data
Use 'sudo apt autoremove' to remove them.
The following additional packages will be installed:
  libcommon-sense-perl libjson-perl libjson-xs-perl libllvm10 libpq5 libsensors-config libsensors5 libtypes-serialiser-perl pgdg-keyring postgresql-client-14 postgresql-client-common
  postgresql-common ssl-cert sysstat
Suggested packages:
  lm-sensors postgresql-doc-14 openssl-blacklist isag
The following NEW packages will be installed:
  libcommon-sense-perl libjson-perl libjson-xs-perl libllvm10 libpq5 libsensors-config libsensors5 libtypes-serialiser-perl pgdg-keyring postgresql-14 postgresql-client-14
  postgresql-client-common postgresql-common ssl-cert sysstat
0 upgraded, 15 newly installed, 0 to remove and 0 not upgraded.
Need to get 33.9 MB of archives.
After this operation, 137 MB of additional disk space will be used.
Get:1 http://us-central1.gce.archive.ubuntu.com/ubuntu focal/main amd64 libcommon-sense-perl amd64 3.74-2build6 [20.1 kB]
Get:2 http://us-central1.gce.archive.ubuntu.com/ubuntu focal/main amd64 libjson-perl all 4.02000-2 [80.9 kB]
Get:3 http://us-central1.gce.archive.ubuntu.com/ubuntu focal/main amd64 libtypes-serialiser-perl all 1.0-1 [12.1 kB]
Get:4 http://us-central1.gce.archive.ubuntu.com/ubuntu focal/main amd64 libjson-xs-perl amd64 4.020-1build1 [83.7 kB]
Get:5 http://us-central1.gce.archive.ubuntu.com/ubuntu focal/main amd64 libllvm10 amd64 1:10.0.0-4ubuntu1 [15.3 MB]
Get:6 http://apt.postgresql.org/pub/repos/apt focal-pgdg/main amd64 libpq5 amd64 14.4-1.pgdg20.04+1 [172 kB]
Get:7 http://us-central1.gce.archive.ubuntu.com/ubuntu focal-updates/main amd64 libsensors-config all 1:3.6.0-2ubuntu1.1 [6052 B]
Get:8 http://us-central1.gce.archive.ubuntu.com/ubuntu focal-updates/main amd64 libsensors5 amd64 1:3.6.0-2ubuntu1.1 [27.2 kB]
Get:9 http://us-central1.gce.archive.ubuntu.com/ubuntu focal/main amd64 ssl-cert all 1.0.39 [17.0 kB]
Get:10 http://us-central1.gce.archive.ubuntu.com/ubuntu focal-updates/main amd64 sysstat amd64 12.2.0-2ubuntu0.1 [448 kB]
Get:11 http://apt.postgresql.org/pub/repos/apt focal-pgdg/main amd64 pgdg-keyring all 2018.2 [10.7 kB]
Get:12 http://apt.postgresql.org/pub/repos/apt focal-pgdg/main amd64 postgresql-client-common all 241.pgdg20.04+1 [92.1 kB]
Get:13 http://apt.postgresql.org/pub/repos/apt focal-pgdg/main amd64 postgresql-client-14 amd64 14.4-1.pgdg20.04+1 [1623 kB]
Get:14 http://apt.postgresql.org/pub/repos/apt focal-pgdg/main amd64 postgresql-common all 241.pgdg20.04+1 [230 kB]
Get:15 http://apt.postgresql.org/pub/repos/apt focal-pgdg/main amd64 postgresql-14 amd64 14.4-1.pgdg20.04+1 [15.8 MB]
Fetched 33.9 MB in 2s (15.9 MB/s)         
Preconfiguring packages ...
Selecting previously unselected package libcommon-sense-perl.
(Reading database ... 60930 files and directories currently installed.)
Preparing to unpack .../00-libcommon-sense-perl_3.74-2build6_amd64.deb ...
Unpacking libcommon-sense-perl (3.74-2build6) ...
Selecting previously unselected package libjson-perl.
Preparing to unpack .../01-libjson-perl_4.02000-2_all.deb ...
Unpacking libjson-perl (4.02000-2) ...
Selecting previously unselected package libtypes-serialiser-perl.
Preparing to unpack .../02-libtypes-serialiser-perl_1.0-1_all.deb ...
Unpacking libtypes-serialiser-perl (1.0-1) ...
Selecting previously unselected package libjson-xs-perl.
Preparing to unpack .../03-libjson-xs-perl_4.020-1build1_amd64.deb ...
Unpacking libjson-xs-perl (4.020-1build1) ...
Selecting previously unselected package libllvm10:amd64.
Preparing to unpack .../04-libllvm10_1%3a10.0.0-4ubuntu1_amd64.deb ...
Unpacking libllvm10:amd64 (1:10.0.0-4ubuntu1) ...
Selecting previously unselected package libpq5:amd64.
Preparing to unpack .../05-libpq5_14.4-1.pgdg20.04+1_amd64.deb ...
Unpacking libpq5:amd64 (14.4-1.pgdg20.04+1) ...
Selecting previously unselected package libsensors-config.
Preparing to unpack .../06-libsensors-config_1%3a3.6.0-2ubuntu1.1_all.deb ...
Unpacking libsensors-config (1:3.6.0-2ubuntu1.1) ...
Selecting previously unselected package libsensors5:amd64.
Preparing to unpack .../07-libsensors5_1%3a3.6.0-2ubuntu1.1_amd64.deb ...
Unpacking libsensors5:amd64 (1:3.6.0-2ubuntu1.1) ...
Selecting previously unselected package pgdg-keyring.
Preparing to unpack .../08-pgdg-keyring_2018.2_all.deb ...
Unpacking pgdg-keyring (2018.2) ...
Selecting previously unselected package postgresql-client-common.
Preparing to unpack .../09-postgresql-client-common_241.pgdg20.04+1_all.deb ...
Unpacking postgresql-client-common (241.pgdg20.04+1) ...
Selecting previously unselected package postgresql-client-14.
Preparing to unpack .../10-postgresql-client-14_14.4-1.pgdg20.04+1_amd64.deb ...
Unpacking postgresql-client-14 (14.4-1.pgdg20.04+1) ...
Selecting previously unselected package ssl-cert.
Preparing to unpack .../11-ssl-cert_1.0.39_all.deb ...
Unpacking ssl-cert (1.0.39) ...
Selecting previously unselected package postgresql-common.
Preparing to unpack .../12-postgresql-common_241.pgdg20.04+1_all.deb ...
Adding 'diversion of /usr/bin/pg_config to /usr/bin/pg_config.libpq-dev by postgresql-common'
Unpacking postgresql-common (241.pgdg20.04+1) ...
Selecting previously unselected package postgresql-14.
Preparing to unpack .../13-postgresql-14_14.4-1.pgdg20.04+1_amd64.deb ...
Unpacking postgresql-14 (14.4-1.pgdg20.04+1) ...
Selecting previously unselected package sysstat.
Preparing to unpack .../14-sysstat_12.2.0-2ubuntu0.1_amd64.deb ...
Unpacking sysstat (12.2.0-2ubuntu0.1) ...
Setting up pgdg-keyring (2018.2) ...
Removing apt.postgresql.org key from trusted.gpg: OK
Setting up libsensors-config (1:3.6.0-2ubuntu1.1) ...
Setting up libpq5:amd64 (14.4-1.pgdg20.04+1) ...
Setting up libcommon-sense-perl (3.74-2build6) ...
Setting up libllvm10:amd64 (1:10.0.0-4ubuntu1) ...
Setting up ssl-cert (1.0.39) ...
Setting up libsensors5:amd64 (1:3.6.0-2ubuntu1.1) ...
Setting up libtypes-serialiser-perl (1.0-1) ...
Setting up libjson-perl (4.02000-2) ...
Setting up sysstat (12.2.0-2ubuntu0.1) ...

Creating config file /etc/default/sysstat with new version
update-alternatives: using /usr/bin/sar.sysstat to provide /usr/bin/sar (sar) in auto mode
Created symlink /etc/systemd/system/multi-user.target.wants/sysstat.service → /lib/systemd/system/sysstat.service.
Setting up postgresql-client-common (241.pgdg20.04+1) ...
Setting up libjson-xs-perl (4.020-1build1) ...
Setting up postgresql-client-14 (14.4-1.pgdg20.04+1) ...
update-alternatives: using /usr/share/postgresql/14/man/man1/psql.1.gz to provide /usr/share/man/man1/psql.1.gz (psql.1.gz) in auto mode
Setting up postgresql-common (241.pgdg20.04+1) ...
Adding user postgres to group ssl-cert

Creating config file /etc/postgresql-common/createcluster.conf with new version
Building PostgreSQL dictionaries from installed myspell/hunspell packages...
Removing obsolete dictionary files:
Created symlink /etc/systemd/system/multi-user.target.wants/postgresql.service → /lib/systemd/system/postgresql.service.
Setting up postgresql-14 (14.4-1.pgdg20.04+1) ...
Creating new PostgreSQL cluster 14/main ...
/usr/lib/postgresql/14/bin/initdb -D /var/lib/postgresql/14/main --auth-local peer --auth-host scram-sha-256 --no-instructions
The files belonging to this database system will be owned by user "postgres".
This user must also own the server process.

The database cluster will be initialized with locale "C.UTF-8".
The default database encoding has accordingly been set to "UTF8".
The default text search configuration will be set to "english".

Data page checksums are disabled.

fixing permissions on existing directory /var/lib/postgresql/14/main ... ok
creating subdirectories ... ok
selecting dynamic shared memory implementation ... posix
selecting default max_connections ... 100
selecting default shared_buffers ... 128MB
selecting default time zone ... Etc/UTC
creating configuration files ... ok
running bootstrap script ... ok
performing post-bootstrap initialization ... ok
syncing data to disk ... ok
update-alternatives: using /usr/share/postgresql/14/man/man1/postmaster.1.gz to provide /usr/share/man/man1/postmaster.1.gz (postmaster.1.gz) in auto mode
Processing triggers for systemd (245.4-4ubuntu3.17) ...
Processing triggers for man-db (2.9.1-1) ...
Processing triggers for libc-bin (2.31-0ubuntu9.9) ...
root@test5:~# systemctl status postgresql
● postgresql.service - PostgreSQL RDBMS
     Loaded: loaded (/lib/systemd/system/postgresql.service; enabled; vendor preset: enabled)
     Active: active (exited) since Wed 2022-06-29 04:14:57 UTC; 2min 11s ago
   Main PID: 5921 (code=exited, status=0/SUCCESS)
      Tasks: 0 (limit: 4696)
     Memory: 0B
     CGroup: /system.slice/postgresql.service

Jun 29 04:14:57 test5 systemd[1]: Starting PostgreSQL RDBMS...
Jun 29 04:14:57 test5 systemd[1]: Finished PostgreSQL RDBMS.
root@test5:~# sudo sh -c 'echo "deb [arch=amd64] https://repo.postgrespro.ru/pg_probackup/deb/ $(lsb_release -cs) main-$(lsb_release -cs)" > /etc/apt/sources.list.d/pg_probackup.list' && sudo wget -O - https://repo.postgrespro.ru/pg_probackup/keys/GPG-KEY-PG_PROBACKUP | sudo apt-key add - && sudo apt-get update
--2022-06-29 04:38:04--  https://repo.postgrespro.ru/pg_probackup/keys/GPG-KEY-PG_PROBACKUP
Resolving repo.postgrespro.ru (repo.postgrespro.ru)... 213.171.56.11
Connecting to repo.postgrespro.ru (repo.postgrespro.ru)|213.171.56.11|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 3120 (3.0K) [application/octet-stream]
Saving to: ‘STDOUT’

-                                               100%[=======================================================================================================>]   3.05K  --.-KB/s    in 0s      

2022-06-29 04:38:04 (326 MB/s) - written to stdout [3120/3120]

OK
Hit:1 http://us-central1.gce.archive.ubuntu.com/ubuntu focal InRelease
Get:2 http://us-central1.gce.archive.ubuntu.com/ubuntu focal-updates InRelease [114 kB]
Get:3 http://us-central1.gce.archive.ubuntu.com/ubuntu focal-backports InRelease [108 kB]
Get:4 http://security.ubuntu.com/ubuntu focal-security InRelease [114 kB]               
Hit:5 http://apt.postgresql.org/pub/repos/apt focal-pgdg InRelease                                           
Get:6 https://repo.postgrespro.ru/pg_probackup/deb focal InRelease [3322 B]                                  
Get:7 https://repo.postgrespro.ru/pg_probackup/deb focal/main-focal amd64 Packages [1958 B]
Fetched 341 kB in 1s (306 kB/s)     
Reading package lists... Done
root@test5:~# sudo apt-mark hold linux-image-5.11.0-1022-gcp && sudo DEBIAN_FRONTEND=noninteractive apt install pg-probackup-14 pg-probackup-14-dbg postgresql-contrib postgresql-14-pg-checksums -y
linux-image-5.11.0-1022-gcp set on hold.
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:
  libatasmart4 libblockdev-fs2 libblockdev-loop2 libblockdev-part-err2 libblockdev-part2 libblockdev-swap2 libblockdev-utils2 libblockdev2 libmm-glib0 libnspr4 libnss3 libnuma1
  libparted-fs-resize0 libudisks2-0 usb-modeswitch usb-modeswitch-data
Use 'sudo apt autoremove' to remove them.
The following additional packages will be installed:
  pg-checksums-doc
The following NEW packages will be installed:
  pg-checksums-doc pg-probackup-14 pg-probackup-14-dbg postgresql-14-pg-checksums postgresql-contrib
0 upgraded, 5 newly installed, 0 to remove and 0 not upgraded.
Need to get 962 kB of archives.
After this operation, 1396 kB of additional disk space will be used.
Get:1 http://apt.postgresql.org/pub/repos/apt focal-pgdg/main amd64 pg-checksums-doc all 1.1-1.pgdg20.04+1 [7044 B]
Get:2 http://apt.postgresql.org/pub/repos/apt focal-pgdg/main amd64 postgresql-14-pg-checksums amd64 1.1-1.pgdg20.04+1 [35.7 kB]
Get:3 http://apt.postgresql.org/pub/repos/apt focal-pgdg/main amd64 postgresql-contrib all 14+241.pgdg20.04+1 [66.7 kB]
Get:4 https://repo.postgrespro.ru/pg_probackup/deb focal/main-focal amd64 pg-probackup-14 amd64 2.5.5-1.0834e54fc37bd841f11717e07291d59ba92e3333.focal [189 kB]
Get:5 https://repo.postgrespro.ru/pg_probackup/deb focal/main-focal amd64 pg-probackup-14-dbg amd64 2.5.5-1.0834e54fc37bd841f11717e07291d59ba92e3333.focal [663 kB]
Fetched 962 kB in 1s (656 kB/s)          
Selecting previously unselected package pg-checksums-doc.
(Reading database ... 63137 files and directories currently installed.)
Preparing to unpack .../pg-checksums-doc_1.1-1.pgdg20.04+1_all.deb ...
Unpacking pg-checksums-doc (1.1-1.pgdg20.04+1) ...
Selecting previously unselected package pg-probackup-14.
Preparing to unpack .../pg-probackup-14_2.5.5-1.0834e54fc37bd841f11717e07291d59ba92e3333.focal_amd64.deb ...
Unpacking pg-probackup-14 (2.5.5-1.0834e54fc37bd841f11717e07291d59ba92e3333.focal) ...
Selecting previously unselected package pg-probackup-14-dbg.
Preparing to unpack .../pg-probackup-14-dbg_2.5.5-1.0834e54fc37bd841f11717e07291d59ba92e3333.focal_amd64.deb ...
Unpacking pg-probackup-14-dbg (2.5.5-1.0834e54fc37bd841f11717e07291d59ba92e3333.focal) ...
Selecting previously unselected package postgresql-14-pg-checksums.
Preparing to unpack .../postgresql-14-pg-checksums_1.1-1.pgdg20.04+1_amd64.deb ...
Unpacking postgresql-14-pg-checksums (1.1-1.pgdg20.04+1) ...
Selecting previously unselected package postgresql-contrib.
Preparing to unpack .../postgresql-contrib_14+241.pgdg20.04+1_all.deb ...
Unpacking postgresql-contrib (14+241.pgdg20.04+1) ...
Setting up pg-checksums-doc (1.1-1.pgdg20.04+1) ...
Setting up postgresql-14-pg-checksums (1.1-1.pgdg20.04+1) ...
Setting up postgresql-contrib (14+241.pgdg20.04+1) ...
Setting up pg-probackup-14 (2.5.5-1.0834e54fc37bd841f11717e07291d59ba92e3333.focal) ...
Setting up pg-probackup-14-dbg (2.5.5-1.0834e54fc37bd841f11717e07291d59ba92e3333.focal) ...
Processing triggers for man-db (2.9.1-1) ...
root@test5:~# sudo mkdir /home/backups && sudo chmod 777 /home/backups
root@test5:~# echo "BACKUP_PATH=/home/backups/">>~/.bashrc
root@test5:~# echo "export BACKUP_PATH">>~/.bashrc
root@test5:~# cd $HOME
root@test5:~# . .bashrc
root@test5:~# echo $BACKUP_PATH
/home/backups/
root@test5:~# psql
psql: error: connection to server on socket "/var/run/postgresql/.s.PGSQL.5432" failed: FATAL:  role "root" does not exist
root@test5:~# create user backup;

Command 'create' not found, did you mean:

  command 'pcreate' from deb pbuilder-scripts (22)

Try: apt install <deb name>

root@test5:~# ALTER ROLE backup NOSUPERUSER;
ALTER: command not found
root@test5:~# ALTER ROLE backup WITH REPLICATION;
ALTER: command not found
root@test5:~# GRANT USAGE ON SCHEMA pg_catalog TO backup;
GRANT: command not found
root@test5:~# GRANT EXECUTE ON FUNCTION pg_catalog.current_setting(text) TO backup;
-bash: syntax error near unexpected token `('
root@test5:~# GRANT EXECUTE ON FUNCTION pg_catalog.pg_is_in_recovery() TO backup;
-bash: syntax error near unexpected token `('
root@test5:~# GRANT EXECUTE ON FUNCTION pg_catalog.pg_start_backup(text, boolean, boolean) TO backup;
-bash: syntax error near unexpected token `('
root@test5:~# GRANT EXECUTE ON FUNCTION pg_catalog.pg_stop_backup(boolean, boolean) TO backup;
-bash: syntax error near unexpected token `('
root@test5:~# GRANT EXECUTE ON FUNCTION pg_catalog.pg_create_restore_point(text) TO backup;
-bash: syntax error near unexpected token `('
root@test5:~# GRANT EXECUTE ON FUNCTION pg_catalog.pg_switch_wal() TO backup;
-bash: syntax error near unexpected token `('
root@test5:~# GRANT EXECUTE ON FUNCTION pg_catalog.pg_last_wal_replay_lsn() TO backup;
-bash: syntax error near unexpected token `('
root@test5:~# GRANT EXECUTE ON FUNCTION pg_catalog.txid_current() TO backup;
-bash: syntax error near unexpected token `('
root@test5:~# GRANT EXECUTE ON FUNCTION pg_catalog.txid_current_snapshot() TO backup;
-bash: syntax error near unexpected token `('
root@test5:~# GRANT EXECUTE ON FUNCTION pg_catalog.txid_snapshot_xmax(txid_snapshot) TO backup;
-bash: syntax error near unexpected token `('
root@test5:~# GRANT EXECUTE ON FUNCTION pg_catalog.pg_control_checkpoint() TO backup;
-bash: syntax error near unexpected token `('
root@test5:~# 
root@test5:~# exit
logout
dimash9527@test5:~$ sudo su - root
root@test5:~# sudo su postgres
postgres@test5:/root$ psql
could not change directory to "/root": Permission denied
psql (14.4 (Ubuntu 14.4-1.pgdg20.04+1))
Type "help" for help.

postgres=# create user backup;
CREATE ROLE
postgres=# ALTER ROLE backup NOSUPERUSER;
ALTER ROLE
postgres=# ALTER ROLE backup WITH REPLICATION;
ALTER ROLE
postgres=# GRANT USAGE ON SCHEMA pg_catalog TO backup;
GRANT
postgres=# GRANT EXECUTE ON FUNCTION pg_catalog.current_setting(text) TO backup;
GRANT
postgres=# GRANT EXECUTE ON FUNCTION pg_catalog.pg_is_in_recovery() TO backup;
GRANT
postgres=# GRANT EXECUTE ON FUNCTION pg_catalog.pg_start_backup(text, boolean, boolean) TO backup;
GRANT
postgres=# GRANT EXECUTE ON FUNCTION pg_catalog.pg_stop_backup(boolean, boolean) TO backup;
GRANT
postgres=# GRANT EXECUTE ON FUNCTION pg_catalog.pg_create_restore_point(text) TO backup;
GRANT
postgres=# GRANT EXECUTE ON FUNCTION pg_catalog.pg_switch_wal() TO backup;
GRANT
postgres=# GRANT EXECUTE ON FUNCTION pg_catalog.pg_last_wal_replay_lsn() TO backup;
GRANT
postgres=# GRANT EXECUTE ON FUNCTION pg_catalog.txid_current() TO backup;
GRANT
postgres=# GRANT EXECUTE ON FUNCTION pg_catalog.txid_current_snapshot() TO backup;
GRANT
postgres=# GRANT EXECUTE ON FUNCTION pg_catalog.txid_snapshot_xmax(txid_snapshot) TO backup;
GRANT
postgres=# GRANT EXECUTE ON FUNCTION pg_catalog.pg_control_checkpoint() TO backup;
GRANT
postgres=# \q
postgres@test5:/root$ sudo rm -rf /home/backups && sudo mkdir /home/backups && sudo chmod 777 /home/backups
[sudo] password for postgres: 
postgres@test5:/root$  rm -rf /home/backups && sudo mkdir /home/backups && sudo chmod 777 /home/backups
rm: cannot remove '/home/backups': Permission denied
postgres@test5:/root$ exit
exit
root@test5:~# sudo rm -rf /home/backups
root@test5:~# sudo su postgres
postgres@test5:/root$ exit
exit
root@test5:~# sudo mkdir /home/backups && sudo chmod 777 /home/backups
root@test5:~# sudo su postgres
postgres@test5:/root$ echo "BACKUP_PATH=/home/backups/">>~/.bashrc
postgres@test5:/root$ echo "export BACKUP_PATH">>~/.bashrc
postgres@test5:/root$ cd $HOME
postgres@test5:~$ . .bashrc
postgres@test5:~$ echo $BACKUP_PATH
/home/backups/
postgres@test5:~$ pg_probackup-14 init
INFO: Backup catalog '/home/backups' successfully inited
postgres@test5:~$ cd $BACKUP_PATH
postgres@test5:/home/backups$ ls -l 
total 8
drwx------ 2 postgres postgres 4096 Jun 29 04:44 backups
drwx------ 2 postgres postgres 4096 Jun 29 04:44 wal
postgres@test5:/home/backups$ pg_probackup-14 add-instance --instance 'main' -D /var/lib/postgresql/14/main
INFO: Instance 'main' successfully inited
postgres@test5:/home/backups$ psql -c "CREATE DATABASE test;"
CREATE DATABASE
postgres@test5:/home/backups$ psql test -c "create table test(i int);"
CREATE TABLE
postgres@test5:/home/backups$ psql test -c "insert into test values (10), (20), (30);"
INSERT 0 3
postgres@test5:/home/backups$ psql test -c "select * from test;"
 i  
----
 10
 20
 30
(3 rows)

postgres@test5:/home/backups$ pg_probackup-14 backup --instance 'main' -b FULL --stream --temp-slot
INFO: Backup start, pg_probackup version: 2.5.5, instance: main, backup ID: RE82KC, backup mode: FULL, wal mode: STREAM, remote: false, compress-algorithm: none, compress-level: 1
WARNING: This PostgreSQL instance was initialized without data block checksums. pg_probackup have no way to detect data block corruption without them. Reinitialize PGDATA with option '--data-checksums'.
WARNING: Current PostgreSQL role is superuser. It is not recommended to run pg_probackup under superuser.
INFO: wait for pg_start_backup()
INFO: Wait for WAL segment /home/backups/backups/main/RE82KC/database/pg_wal/000000010000000000000002 to be streamed
INFO: PGDATA size: 33MB
INFO: Start transferring data files
INFO: Data files are transferred, time elapsed: 1s
INFO: wait for pg_stop_backup()
INFO: pg_stop backup() successfully executed
INFO: Syncing backup files to disk
INFO: Backup files are synced, time elapsed: 2s
INFO: Validating backup RE82KC
INFO: Backup RE82KC data files are valid
INFO: Backup RE82KC resident size: 65MB
INFO: Backup RE82KC completed
postgres@test5:/home/backups$ pg_ctlcluster 14 main stop
Warning: stopping the cluster using pg_ctlcluster will mark the systemd unit as failed. Consider using systemctl:
  sudo systemctl stop postgresql@14-main
postgres@test5:/home/backups$ /usr/lib/postgresql/14/bin/pg_checksums -D /var/lib/postgresql/14/main --enable
Checksum operation completed
Files scanned:  1224
Blocks scanned: 4256
pg_checksums: syncing data directory
pg_checksums: updating control file
Checksums enabled in cluster
postgres@test5:/home/backups$ pg_ctlcluster 14 main start
Warning: the cluster will not be running as a systemd service. Consider using systemctl:
  sudo systemctl start postgresql@14-main
postgres@test5:/home/backups$ pg_lsclusters
Ver Cluster Port Status Owner    Data directory              Log file
14  main    5432 online postgres /var/lib/postgresql/14/main /var/log/postgresql/postgresql-14-main.log
postgres@test5:/home/backups$ pg_probackup-14 show

BACKUP INSTANCE 'main'
================================================================================================================================
 Instance  Version  ID      Recovery Time           Mode  WAL Mode  TLI  Time  Data   WAL  Zratio  Start LSN  Stop LSN   Status 
================================================================================================================================
 main      14       RE82KC  2022-06-29 04:45:50+00  FULL  STREAM    1/0   10s  33MB  32MB    1.00  0/2000028  0/2002098  OK     
postgres@test5:/home/backups$ psql test -c "insert into test values (4);"
INSERT 0 1
postgres@test5:/home/backups$ pg_probackup-14 backup --instance 'main' -b DELTA --stream --temp-slot -U backup
INFO: Backup start, pg_probackup version: 2.5.5, instance: main, backup ID: RE82MW, backup mode: DELTA, wal mode: STREAM, remote: false, compress-algorithm: none, compress-level: 1
ERROR: could not connect to database postgres: connection to server on socket "/var/run/postgresql/.s.PGSQL.5432" failed: FATAL:  Peer authentication failed for user "backup"

WARNING: Backup RE82MW is running, setting its status to ERROR
postgres@test5:/home/backups$ psql -c "ALTER USER backup PASSWORD 'test123';"
ALTER ROLE
postgres@test5:/home/backups$ pg_probackup-14 backup --instance 'main' -b DELTA --stream --temp-slot -h localhost -U backup -W
INFO: Backup start, pg_probackup version: 2.5.5, instance: main, backup ID: RE82O7, backup mode: DELTA, wal mode: STREAM, remote: false, compress-algorithm: none, compress-level: 1
Password for user backup: 
INFO: wait for pg_start_backup()
WARNING: Backup RE82MW has status: ERROR. Cannot be a parent.
INFO: Parent backup: RE82KC
INFO: Wait for WAL segment /home/backups/backups/main/RE82O7/database/pg_wal/000000010000000000000004 to be streamed
INFO: PGDATA size: 33MB
INFO: Start transferring data files
INFO: Data files are transferred, time elapsed: 0
INFO: wait for pg_stop_backup()
INFO: pg_stop backup() successfully executed
INFO: Syncing backup files to disk
INFO: Backup files are synced, time elapsed: 1s
INFO: Validating backup RE82O7
INFO: Backup RE82O7 data files are valid
INFO: Backup RE82O7 resident size: 37MB
INFO: Backup RE82O7 completed
postgres@test5:/home/backups$ pg_probackup-14 show

BACKUP INSTANCE 'main'
===================================================================================================================================
 Instance  Version  ID      Recovery Time           Mode   WAL Mode  TLI  Time    Data   WAL  Zratio  Start LSN  Stop LSN   Status 
===================================================================================================================================
 main      14       RE82O7  2022-06-29 04:48:15+00  DELTA  STREAM    1/1   10s  5279kB  32MB    1.00  0/4000028  0/4000168  OK     
 main      ----     RE82MW  ----                    DELTA  STREAM    0/1     0       0     0    1.00  0/0        0/0        ERROR  
 main      14       RE82KC  2022-06-29 04:45:50+00  FULL   STREAM    1/0   10s    33MB  32MB    1.00  0/2000028  0/2002098  OK     


 Пробую во второй раз) 

 Welcome to Ubuntu 20.04.4 LTS (GNU/Linux 5.13.0-1033-gcp x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Wed Jun 29 05:12:09 UTC 2022

  System load:  0.0               Processes:             120
  Usage of /:   22.1% of 9.52GB   Users logged in:       1
  Memory usage: 6%                IPv4 address for ens4: 10.128.0.6
  Swap usage:   0%


0 updates can be applied immediately.


*** System restart required ***
Last login: Wed Jun 29 04:12:51 2022 from 35.235.240.1
dimash9527@test5:~$ sudo su - root
root@test5:~# sudo su postgres
postgres@test5:/root$ pg_probackup-14 show
could not change directory to "/root": Permission denied
WARNING: pg_probackup-14: could not find a full path to executable
WARNING: This backup catalog contains no backup instances. Backup instance can be added via 'add-instance' command.
postgres@test5:/root$ pg_ctlcluster
Error: Usage: /usr/bin/pg_ctlcluster <version> <cluster> <action> [-- <pg_ctl options>]
postgres@test5:/root$ pg_probackup-14 show
could not change directory to "/root": Permission denied
WARNING: pg_probackup-14: could not find a full path to executable
WARNING: This backup catalog contains no backup instances. Backup instance can be added via 'add-instance' command.
postgres@test5:/root$ cd $BACKUP_PATH
postgres@test5:/home/backups$ ls -l
total 8
drwx------ 2 postgres postgres 4096 Jun 29 05:02 backups
drwx------ 2 postgres postgres 4096 Jun 29 05:02 wal
postgres@test5:/home/backups$ pg_probackup-14 show
WARNING: This backup catalog contains no backup instances. Backup instance can be added via 'add-instance' command.
postgres@test5:/home/backups$ pg_lsclusters
Ver Cluster Port Status Owner     Data directory               Log file
14  main    5432 online postgres  /var/lib/postgresql/14/main  /var/log/postgresql/postgresql-14-main.log
14  main2   5433 down   <unknown> /var/lib/postgresql/14/main2 /var/log/postgresql/postgresql-14-main2.log
postgres@test5:/home/backups$ mc

Command 'mc' not found, but can be installed with:

apt install mc
Please ask your administrator.

postgres@test5:/home/backups$ exit
exit
root@test5:~# mc

Command 'mc' not found, but can be installed with:

apt install mc

root@test5:~# nano
root@test5:~# apt install mc
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:
  libatasmart4 libblockdev-fs2 libblockdev-loop2 libblockdev-part-err2 libblockdev-part2 libblockdev-swap2 libblockdev-utils2 libblockdev2 libmm-glib0 libnspr4 libnss3 libnuma1
  libparted-fs-resize0 libudisks2-0 usb-modeswitch usb-modeswitch-data
Use 'apt autoremove' to remove them.
The following additional packages will be installed:
  libssh2-1 mc-data unzip
Suggested packages:
  arj catdvi | texlive-binaries dbview djvulibre-bin epub-utils genisoimage gv imagemagick libaspell-dev links | w3m | lynx odt2txt poppler-utils python python-boto python-tz xpdf
  | pdf-viewer zip
The following NEW packages will be installed:
  libssh2-1 mc mc-data unzip
0 upgraded, 4 newly installed, 0 to remove and 0 not upgraded.
Need to get 1986 kB of archives.
After this operation, 8587 kB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://us-central1.gce.archive.ubuntu.com/ubuntu focal/universe amd64 libssh2-1 amd64 1.8.0-2.1build1 [75.4 kB]
Get:2 http://us-central1.gce.archive.ubuntu.com/ubuntu focal/universe amd64 mc-data all 3:4.8.24-2ubuntu1 [1265 kB]
Get:3 http://us-central1.gce.archive.ubuntu.com/ubuntu focal/universe amd64 mc amd64 3:4.8.24-2ubuntu1 [477 kB]
Get:4 http://us-central1.gce.archive.ubuntu.com/ubuntu focal/main amd64 unzip amd64 6.0-25ubuntu1 [169 kB]
Fetched 1986 kB in 0s (30.4 MB/s)
Selecting previously unselected package libssh2-1:amd64.
(Reading database ... 63159 files and directories currently installed.)
Preparing to unpack .../libssh2-1_1.8.0-2.1build1_amd64.deb ...
Unpacking libssh2-1:amd64 (1.8.0-2.1build1) ...
Selecting previously unselected package mc-data.
Preparing to unpack .../mc-data_3%3a4.8.24-2ubuntu1_all.deb ...
Unpacking mc-data (3:4.8.24-2ubuntu1) ...
Selecting previously unselected package mc.
Preparing to unpack .../mc_3%3a4.8.24-2ubuntu1_amd64.deb ...
Unpacking mc (3:4.8.24-2ubuntu1) ...
Selecting previously unselected package unzip.
Preparing to unpack .../unzip_6.0-25ubuntu1_amd64.deb ...
Unpacking unzip (6.0-25ubuntu1) ...
Setting up unzip (6.0-25ubuntu1) ...
Setting up mc-data (3:4.8.24-2ubuntu1) ...
Setting up libssh2-1:amd64 (1.8.0-2.1build1) ...
Setting up mc (3:4.8.24-2ubuntu1) ...
Processing triggers for man-db (2.9.1-1) ...
Processing triggers for mime-support (3.64ubuntu1) ...
Processing triggers for libc-bin (2.31-0ubuntu9.9) ...
root@test5:~# mc

root@test5:~# sudo su postgres
postgres@test5:/root$ pg_probackup-14 init
could not change directory to "/root": Permission denied
WARNING: pg_probackup-14: could not find a full path to executable
ERROR: backup catalog already exist and it's not empty
postgres@test5:/root$ cd $BACKUP_PATH
postgres@test5:/home/backups$ pg_probackup-14 init
ERROR: backup catalog already exist and it's not empty
postgres@test5:/home/backups$ ^C
postgres@test5:/home/backups$ pg_probackup-14 show
WARNING: This backup catalog contains no backup instances. Backup instance can be added via 'add-instance' command.
postgres@test5:/home/backups$ pg_probackup-14 restore --instance 'main' -i 'RE83AT' -D /var/lib/postgresql/14/main2 
WARNING: Failed to access directory "/home/backups/backups/main": No such file or directory
ERROR: Instance 'main' does not exist in this backup catalog
postgres@test5:/home/backups$ ^C
postgres@test5:/home/backups$ pg_probackup-14 restore --instance 'main' -i 'RE83AT' -D /var/lib/postgresql/14/main2 
WARNING: Failed to access directory "/home/backups/backups/main": No such file or directory
ERROR: Instance 'main' does not exist in this backup catalog
postgres@test5:/home/backups$ pg_probackup-14 backup --instance 'main' -b FULL --stream --temp-slot -h localhost -U backup -d test -p 5432
WARNING: Failed to access directory "/home/backups/backups/main": No such file or directory
ERROR: Instance 'main' does not exist in this backup catalog
postgres@test5:/home/backups$ pg_probackup-14 show
WARNING: This backup catalog contains no backup instances. Backup instance can be added via 'add-instance' command.
postgres@test5:/home/backups$ psql -d test
psql (14.4 (Ubuntu 14.4-1.pgdg20.04+1))
Type "help" for help.

test=# RANT USAGE ON SCHEMA pg_catalog TO backup;
ERROR:  syntax error at or near "RANT"
LINE 1: RANT USAGE ON SCHEMA pg_catalog TO backup;
        ^
test=# GRANT EXECUTE ON FUNCTION pg_catalog.current_setting(text) TO backup;
GRANT
test=# GRANT EXECUTE ON FUNCTION pg_catalog.pg_is_in_recovery() TO backup;
GRANT
test=# GRANT EXECUTE ON FUNCTION pg_catalog.pg_start_backup(text, boolean, boolean) TO backup;
GRANT
test=# GRANT EXECUTE ON FUNCTION pg_catalog.pg_stop_backup(boolean, boolean) TO backup;
GRANT
test=# GRANT EXECUTE ON FUNCTION pg_catalog.pg_create_restore_point(text) TO backup;
GRANT
test=# GRANT EXECUTE ON FUNCTION pg_catalog.pg_switch_wal() TO backup;
GRANT
test=# GRANT EXECUTE ON FUNCTION pg_catalog.pg_last_wal_replay_lsn() TO backup;
GRANT
test=# GRANT EXECUTE ON FUNCTION pg_catalog.txid_current() TO backup;
GRANT
test=# GRANT EXECUTE ON FUNCTION pg_catalog.txid_current_snapshot() TO backup;
GRANT
test=# GRANT EXECUTE ON FUNCTION pg_catalog.txid_snapshot_xmax(txid_snapshot) TO backup;
GRANT
test=# GRANT EXECUTE ON FUNCTION pg_catalog.pg_control_checkpoint() TO backup;
GRANT
test=# \q
postgres@test5:/home/backups$ pg_probackup-14 backup --instance 'main' -b DELTA --stream --temp-slot -h localhost -U backup --pgdatabase=test
WARNING: Failed to access directory "/home/backups/backups/main": No such file or directory
ERROR: Instance 'main' does not exist in this backup catalog
postgres@test5:/home/backups$ exit
exit
root@test5:~# sudo chmod 777 /home/backups/backups/main
chmod: cannot access '/home/backups/backups/main': No such file or directory
root@test5:~# sudo chmod 777 /home/backups/backups
root@test5:~# sudo su postgres
postgres@test5:/root$ cd /home/backups
postgres@test5:/home/backups$ ls -l
total 8
drwxrwxrwx 2 postgres postgres 4096 Jun 29 05:02 backups
drwx------ 2 postgres postgres 4096 Jun 29 05:02 wal
postgres@test5:/home/backups$ cd baskups
bash: cd: baskups: No such file or directory
postgres@test5:/home/backups$ cd backups
postgres@test5:/home/backups/backups$ ls -l
total 0
postgres@test5:/home/backups/backups$ exit
exit
root@test5:~# sudo su postgres
postgres@test5:/root$ cd /home/backups
postgres@test5:/home/backups$ exit
exit
root@test5:~# sudo su postgres
postgres@test5:/root$ rm -rf /home/backups
rm: cannot remove '/home/backups': Permission denied
postgres@test5:/root$ exit
exit
root@test5:~# sudo rm -rf /home/backups && sudo mkdir /home/backups && sudo chmod 777 /home/backups
root@test5:~# sudo su postgres
postgres@test5:/root$ echo "BACKUP_PATH=/home/backups/">>~/.bashrc
postgres@test5:/root$ echo "export BACKUP_PATH">>~/.bashrc
postgres@test5:/root$ . .bashrc
bash: .bashrc: Permission denied
postgres@test5:/root$ cd $HOME
postgres@test5:~$ -- cd ~
--: command not found
postgres@test5:~$ cd ~
postgres@test5:~$ . .bashrc
postgres@test5:~$ echo $BACKUP_PATH
/home/backups/
postgres@test5:~$ pg_probackup-14 init
INFO: Backup catalog '/home/backups' successfully inited
postgres@test5:~$ cd $BACKUP_PATH
postgres@test5:/home/backups$ ls -l
total 8
drwx------ 2 postgres postgres 4096 Jun 29 05:30 backups
drwx------ 2 postgres postgres 4096 Jun 29 05:30 wal
postgres@test5:/home/backups$ pg_probackup-14 add-instance --instance 'main' -D /var/lib/postgresql/14/main
INFO: Instance 'main' successfully inited
postgres@test5:/home/backups$ pg_probackup-14 backup --instance 'main' -b FULL --stream --temp-slo
INFO: Backup start, pg_probackup version: 2.5.5, instance: main, backup ID: RE84O2, backup mode: FULL, wal mode: STREAM, remote: false, compress-algorithm: none, compress-level: 1
WARNING: Current PostgreSQL role is superuser. It is not recommended to run pg_probackup under superuser.
INFO: wait for pg_start_backup()
INFO: Wait for WAL segment /home/backups/backups/main/RE84O2/database/pg_wal/000000010000000000000008 to be streamed
INFO: PGDATA size: 33MB
INFO: Start transferring data files
INFO: Data files are transferred, time elapsed: 0
INFO: wait for pg_stop_backup()
INFO: pg_stop backup() successfully executed
INFO: Syncing backup files to disk
INFO: Backup files are synced, time elapsed: 2s
INFO: Validating backup RE84O2
INFO: Backup RE84O2 data files are valid
INFO: Backup RE84O2 resident size: 65MB
INFO: Backup RE84O2 completed
postgres@test5:/home/backups$ cd backups
postgres@test5:/home/backups/backups$ \s
s: command not found
postgres@test5:/home/backups/backups$ ls
main
postgres@test5:/home/backups/backups$ cd main
postgres@test5:/home/backups/backups/main$ ls
RE84O2  pg_probackup.conf
postgres@test5:/home/backups/backups/main$ exit
exit
root@test5:~# sudo su postgres
postgres@test5:/root$ cd /home/backups
postgres@test5:/home/backups$ pg_probackup-14 show

BACKUP INSTANCE 'main'
================================================================================================================================
 Instance  Version  ID      Recovery Time           Mode  WAL Mode  TLI  Time  Data   WAL  Zratio  Start LSN  Stop LSN   Status 
================================================================================================================================
 main      14       RE84O2  2022-06-29 05:31:15+00  FULL  STREAM    1/0    9s  33MB  32MB    1.00  0/8000028  0/8000168  OK     
postgres@test5:/home/backups$ rm -rf /var/lib/postgresql/14/main2
postgres@test5:/home/backups$ pg_probackup-14 restore --instance 'main' -i 'RE84O2' -D /var/lib/postgresql/14/main2 
INFO: Validating backup RE84O2
INFO: Backup RE84O2 data files are valid
INFO: Backup RE84O2 WAL segments are valid
INFO: Backup RE84O2 is valid.
INFO: Restoring the database from backup at 2022-06-29 05:31:14+00
INFO: Start restoring backup files. PGDATA size: 65MB
INFO: Backup files are restored. Transfered bytes: 65MB, time elapsed: 0
INFO: Restore incremental ratio (less is better): 100% (65MB/65MB)
INFO: Syncing restored files to disk
INFO: Restored backup files are synced, time elapsed: 2s
INFO: Restore of backup RE84O2 completed.
postgres@test5:/home/backups$ pg_ctlcluster 14 main2 start
Warning: the cluster will not be running as a systemd service. Consider using systemctl:
  sudo systemctl start postgresql@14-main2
postgres@test5:/home/backups$ pg_lsclusters
Ver Cluster Port Status Owner    Data directory               Log file
14  main    5432 online postgres /var/lib/postgresql/14/main  /var/log/postgresql/postgresql-14-main.log
14  main2   5433 online postgres /var/lib/postgresql/14/main2 /var/log/postgresql/postgresql-14-main2.log
postgres@test5:/home/backups$ psql test -p 5433 -c 'select * from test;'
 i  
----
 10
 20
 30
  4
(4 rows)

создал 2 кластер на порту 5433, и подключился к нему видим что данные есть которые я писал ранее в базе test. 

под нагрузкой бэкап, с начала поставлю pgbench

dimash9527@test5:~$ sudo su - root
root@test5:~# sudo su - postgres
postgres@test5:~$ psql
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
 test      | postgres | UTF8     | C.UTF-8 | C.UTF-8 | 
(4 rows)

postgres=# \q
postgres@test5:~$ pgbench -c 10 -j 2 -t 10000 test
pgbench (14.4 (Ubuntu 14.4-1.pgdg20.04+1))
pgbench: fatal: could not count number of branches: ERROR:  relation "pgbench_branches" does not exist
LINE 1: select count(*) from pgbench_branches
                             ^
pgbench: Perhaps you need to do initialization ("pgbench -i") in database "test"
postgres@test5:~$ pgbench -i -s 50 test
dropping old tables...
NOTICE:  table "pgbench_accounts" does not exist, skipping
NOTICE:  table "pgbench_branches" does not exist, skipping
NOTICE:  table "pgbench_history" does not exist, skipping
NOTICE:  table "pgbench_tellers" does not exist, skipping
creating tables...
generating data (client-side)...
5000000 of 5000000 tuples (100%) done (elapsed 12.21 s, remaining 0.00 s)
vacuuming...
creating primary keys...
done in 25.54 s (drop tables 0.00 s, create tables 0.01 s, client-side generate 12.26 s, vacuum 8.99 s, primary keys 4.28 s).

на одном окне поставил  проверил с начало 10 000 транзакции в секунду без бэкапа. 
postgres@test5:/root$ pgbench -c 10 -j 2 -t 10000 test
pgbench (14.4 (Ubuntu 14.4-1.pgdg20.04+1))
starting vacuum...end.
transaction type: <builtin: TPC-B (sort of)>
scaling factor: 50
query mode: simple
number of clients: 10
number of threads: 2
number of transactions per client: 10000
number of transactions actually processed: 100000/100000
latency average = 5.556 ms
initial connection time = 23.580 ms
tps = 1799.855850 (without initial connection time)

на втором окне проверил теперь одновременно запуском pgbench и full probackup , то есть на одном окне pgbecnh на втором запуск pgprobackup
backup включил full на втором окне. 
postgres@test5:/home/backups$ pg_probackup-14 backup --instance 'main' -b FULL --stream --temp-slot
INFO: Backup start, pg_probackup version: 2.5.5, instance: main, backup ID: RE8EEI, backup mode: FULL, wal mode: STREAM, remote: false, compress-algorithm: none, compress-level: 1
WARNING: Current PostgreSQL role is superuser. It is not recommended to run pg_probackup under superuser.
INFO: wait for pg_start_backup()
INFO: Wait for WAL segment /home/backups/backups/main/RE8EEI/database/pg_wal/000000010000000000000074 to be streamed
INFO: PGDATA size: 791MB
INFO: Start transferring data files
INFO: Data files are transferred, time elapsed: 4s
INFO: wait for pg_stop_backup()
INFO: pg_stop backup() successfully executed
INFO: Syncing backup files to disk
INFO: Backup files are synced, time elapsed: 2s
INFO: Validating backup RE8EEI
INFO: Backup RE8EEI data files are valid
INFO: Backup RE8EEI resident size: 872MB
INFO: Backup RE8EEI completed
на первом окне запустил pgbench. 
postgres@test5:/root$ pgbench -c 10 -j 2 -t 10000 test
pgbench (14.4 (Ubuntu 14.4-1.pgdg20.04+1))
starting vacuum...end.
transaction type: <builtin: TPC-B (sort of)>
scaling factor: 50
query mode: simple
number of clients: 10
number of threads: 2
number of transactions per client: 10000
number of transactions actually processed: 100000/100000
latency average = 6.336 ms
initial connection time = 20.211 ms
tps = 1578.188426 (without initial connection time)

итог, без бэкапа обрабатывает больше 1799,855850 

с нагрузкой pgbecnh и бэкап, 1578.188426 


