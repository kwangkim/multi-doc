# Apache Web Server

## About
```
# yum install httpd
```

## install php for Apache2
```
# yum install php
# rpm -qa | grep php
php-cli-5.3.3-22.el6.x86_64
php-5.3.3-22.el6.x86_64
php-common-5.3.3-22.el6.x86_64
# rpm -ql php-5.3.3-22.el6.x86_64
/etc/httpd/conf.d/php.conf
**/usr/lib64/httpd/modules/libphp5.so**
/var/lib/php/session
/var/www/icons/php.gif
# vi /etc/httpd/conf/httpd.conf
...
#LoadModule unique_id_module modules/mod_unique_id.so
#

##################################################################
# php (kimduho)
LoadModule php5_module /usr/lib64/httpd/modules/libphp5.so
AddType application/x-httpd-php .php .html
##################################################################
...
#######################################################
# for security reason (kimduho)
#   Options Indexes FollowSymLinks
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
