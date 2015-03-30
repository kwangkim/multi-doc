# Managing Httpd Server
## Troubleshooting Services
* (13) Permission Denied
 * Error 13 indicates a filesystem permissions problem. That is, Apache was denied access to a file or directory due to incorrect permissions. It does not, in general, imply a problem in the Apache configuration files.
```sh
$ tail -1 /etc/httpd/logs/error_log
[Mon Mar 30 10:29:24 2015] [error] [client 192.168.xxx.xxx] (13)Permission denied: access to /<path_to>/cake.png denied
$ vi /etc/selinux/config; # this setting will be applied after reboot
#SELINUX=enforcing
SELINUX=permissive
$ setenforce permissive; # this setting will be applied right now
$ getenforce
Permissive
$ wget http://<my_hostname_and_port>/<path_to>/cake.png -O test.png
Saving to: `test.png'

100%[==============================================================================================================================>] 308         --.-K/s   in 0s      

2015-03-30 10:35:45 (29.8 MB/s) - `test.png' saved [308/308]
```
