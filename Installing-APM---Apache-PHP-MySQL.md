# Apache Web Server

## About APM
* Install Apache, then MySQL, then PHP sequentially.
```sh
# yum install httpd
```

## Install MySQL for Apache / Apache2
### Basic Preparation
```sh
# yum install mysql-server
# rpm -qa | grep mysql
mysql-5.1.69-1.el6_4.x86_64
mysql-server-5.1.69-1.el6_4.x86_64
mysql-libs-5.1.69-1.el6_4.x86_64
# cp /usr/share/mysql/my-medium.cnf /etc/my.cnf 
cp: overwrite `/etc/my.cnf'? y
```

### Basic Installation
```sh
# cd /usr/bin; ./mysql_install_db --user=mysql;  // install basic database mysql and testdb
```

### Secure Installation (vs. Basic Installation)
```sh
# /usr/bin/mysql_secure_installation
Enter current password for root (enter for none): 
Change the root password? [Y/n] n
Remove anonymous users? [Y/n] Y
Disallow root login remotely? [Y/n] Y
Remove test database and access to it? [Y/n] Y
Reload privilege tables now? [Y/n] Y
 ... Success!

Cleaning up...
```

### Configuration
```sh
# chkconfig mysqld on
# chkconfig --list mysqld
mysqld         	0:off	1:off	2:on	3:on	4:on	5:on	6:off
# service mysqld start;  // or cd /usr; /usr/bin/mysqld_safe &
Starting mysqld:                                           [  OK  ]
# /usr/bin/mysqladmin -u root password 'new-password'; // or /usr/bin/mysqladmin -u root -h nutch01.myhome.com password 'new-password'
# mysql --version
mysql  Ver 14.14 Distrib 5.1.69, for redhat-linux-gnu (x86_64) using readline 5.1
# mysql -u root -p
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
+--------------------+
```

### Testing MySQL
```sh
# cd /usr/mysql-test; perl mysql-test-run.pl
```

## install PHP for Apache / Apache2
```sh
# // yum info php-gd (graphics library), php-imap (email), 
# yum install php php-devel php-mysql php-odbc php-gd php-imap php-ldap php-xml
# rpm -qa | grep php
php-devel-5.3.3-23.el6_4.x86_64
php-pdo-5.3.3-23.el6_4.x86_64
php-gd-5.3.3-23.el6_4.x86_64
php-cli-5.3.3-23.el6_4.x86_64
php-mysql-5.3.3-23.el6_4.x86_64
php-5.3.3-23.el6_4.x86_64
php-imap-5.3.3-23.el6_4.x86_64
php-common-5.3.3-23.el6_4.x86_64
php-xml-5.3.3-23.el6_4.x86_64
php-odbc-5.3.3-23.el6_4.x86_64
# rpm -ql php-5.3.3-23.el6_4.x86_64
/etc/httpd/conf.d/php.conf
/usr/lib64/httpd/modules/libphp5.so <-- !
/var/lib/php/session
/var/www/icons/php.gif
# vi /etc/httpd/conf/httpd.conf
...
#LoadModule unique_id_module modules/mod_unique_id.so
#

##################################################################
# php (kimduho)
LoadModule php5_module /usr/lib64/httpd/modules/libphp5.so
AddType application/x-httpd-php .html .htm .php .inc
AddType application/x-httpd-php-source .phps
##################################################################
...
#######################################################
# for security reason (kimduho): prevents directory listing
    Options Indexes FollowSymLinks
#######################################################
...
############################################################
# index.php added (kimduho)
DirectoryIndex index.html index.html.var index.php
############################################################
...
# service httpd restart
# vi /var/www/html/test.php
<?php
phpinfo();
?>
# cd ~/; wget http://localhost/test.php
# cat ./test.php; rm -f ./test.php
```
