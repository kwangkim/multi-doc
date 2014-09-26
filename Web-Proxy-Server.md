# Web Proxy Server
## HAProxy
* Install and Configurations
```sh
# yum install haproxy
# chkconfig haproxy on
# chkconfig --list haproxy
haproxy        	0:off	1:off	2:on	3:on	4:on	5:on	6:off
# cp /etc/haproxy/haproxy.cfg /etc/haproxy/haproxy.cfg.org
# vi /etc/haproxy/haproxy.cfg
#---------------------------------------------------------------------
# main frontend which proxys to the backends
#---------------------------------------------------------------------
listen  MyApp 10.234.5.175:8090
    mode http
    option httpclose
    option forwardfor
    server MyApp01 127.0.0.1:8081 maxconn 32
```
* Start and Stop
```sh
# service haproxy start
# service haproxy restart
# ps -ef | grep haproxy
haproxy  19745     1  0 04:51 ?        00:00:01 /usr/sbin/haproxy -D -f /etc/haproxy/haproxy.cfg -p /var/run/haproxy.pid
# service haproxy stop
```