# Apache Web Server

## About APM
* Install Apache, then MySQL, then PHP sequentially.
```sh
# yum install httpd
```

## Install Httpd
* for CentOS 7.0
```sh
# setenforce Permissive
# yum install httpd
# rm -rf /etc/httpd/conf.d/welcome.conf
# vi /etc/httpd/conf/httpd.conf
...
ServerAdmin root@myservername.com
ServerName myservername.com:80
AllowOverride All
DirectoryIndex index.html index.cgi index.php

# security reason: server's response header should be simple "Apache", not including version
ServerSignature Off
ServerTokens Prod

KeepAlive On
# systemctl start httpd
# systemctl enable httpd
ln -s '/usr/lib/systemd/system/httpd.service' '/etc/systemd/system/multi-user.target.wants/httpd.service'
# service httpd status
Redirecting to /bin/systemctl status  httpd.service
httpd.service - The Apache HTTP Server
   Loaded: loaded (/usr/lib/systemd/system/httpd.service; enabled)
...
# ps -ef | grep httpd | grep -v grep
root     21937     1  0 19:51 ?        00:00:00 /usr/sbin/httpd -DFOREGROUND
apache   21938 21937  0 19:51 ?        00:00:00 /usr/sbin/httpd -DFOREGROUND
apache   21939 21937  0 19:51 ?        00:00:00 /usr/sbin/httpd -DFOREGROUND
apache   21940 21937  0 19:51 ?        00:00:00 /usr/sbin/httpd -DFOREGROUND
apache   21941 21937  0 19:51 ?        00:00:00 /usr/sbin/httpd -DFOREGROUND
apache   21942 21937  0 19:51 ?        00:00:00 /usr/sbin/httpd -DFOREGROUND
# yum install iptables-services
# systemctl enable iptables
ln -s '/usr/lib/systemd/system/iptables.service' '/etc/systemd/system/basic.target.wants/iptables.service'
# systemctl start iptables
# iptables -A INPUT -m state --state NEW -p tcp --dport 80 -j ACCEPT
# service iptables save
iptables: Saving firewall rules to /etc/sysconfig/iptables:[  OK  ]
# vi /etc/sysconfig/iptables
# systemctl status firewalld
# systemctl stop firewalld
# systemctl disable firewalld
rm '/etc/systemd/system/basic.target.wants/firewalld.service'
rm '/etc/systemd/system/dbus-org.fedoraproject.FirewallD1.service'
# service iptables status
# service iptables restart
Redirecting to /bin/systemctl restart  iptables.service
```
* Virtual Server Hosting by port
```sh
# vi /etc/httpd/conf/httpd.conf
#NameVirtualHost *:80
NameVirtualHost <myhostname>:80
NameVirtualHost <myhostname>:8080

<VirtualHost *:80>
    ServerAdmin root@<myhostname>
    DocumentRoot /var/www/html
    ServerName <myhostname>
</VirtualHost>

<VirtualHost *:8080>
    ServerAdmin root@<myhostname>
    DocumentRoot /var/www/html/<2nd_path>
    ServerName <myhostname>
</VirtualHost>
# vi /etc/sysconfig/iptables
...
*filter
:INPUT ACCEPT [0:0]
:FORWARD ACCEPT [0:0]
:OUTPUT ACCEPT [0:0]
...
-A INPUT -p tcp -m state --state NEW -m tcp --dport 80 -j ACCEPT
-A INPUT -p tcp -m state --state NEW -m tcp --dport 8080 -j ACCEPT
COMMIT
# service iptables restart
# service httpd restart
# wget http://<myhostname>:80/
# wget http://<myhostname>:8080/
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
* new method
```sh
# wget http://repo.mysql.com/mysql-community-release-el6-5.noarch.rpm
# yum install ./mysql-community-release-el6-5.noarch.rpm
# yum install mysql-server
# cp /usr/share/mysql/my-medium.cnf /etc/my.cnf 
cp: overwrite `/etc/my.cnf'? y
```
* binding to specific address
```sh
# vi /etc/my.cnf
[mysqld]
...
max_allowed_packet=32M
bind-address=<external_ip_address_of_mysql_server>
# service mysqld restart
# check my ip address at: http://www.whatismyip.com/
# mysql -u root -p
mysql> 
```

### Basic Installation
```sh
# cd /usr/bin; ./mysql_install_db --user=mysql;  // install basic database mysql and testdb
```

### Secure Installation (vs. Basic Installation)
#### prerequisites
* DO NOT forget to run mysqld using mysql_safe before following the below step
```sh
mysqld_safe &
```

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
# vi /erc/php.ini; # // form tag를 이용해서 MySQL에 데이터를 입력하면 값이 공백으로 들어가지 않도록 함
register_globals = On
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