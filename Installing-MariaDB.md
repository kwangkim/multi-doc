# Installing MariaDB
```sh
# vi /etc/yum.repos.d
[mariadb]
name = MariaDB
baseurl = http://yum.mariadb.org/5.5/centos6-amd64
gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
gpgcheck=1
# yum install MariaDB-server MariaDB-client
# chkconfig mysql on
# chkconfig --list mysql
mysql          	0:off	1:off	2:on	3:on	4:on	5:on	6:off
# service mysql start
Starting MySQL... SUCCESS!
# mysql -uroot
MariaDB [(none)]> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| test               |
+--------------------+
4 rows in set (0.00 sec)
MariaDB [(none)]> quit;
Bye
# 
```

## Setup TokuDB other than InnoDB
* [https://mariadb.com/kb/en/how-to-enable-tokudb-in-mariadb/]
