# Play Framework

## About
```
tbd
```

## Architecture
### Play v2.1
* Web Server
 * Internal Web Server: JBoss netty web server
 * External Apache Web Server: can be distributed as a package of war files

## HTTP Server Configurations
* [ref](http://www.playframework.com/documentation/2.0/HTTPServer)

### Set-up a front-end HTTP server
* You can easily deploy your application as a stand-alone server by setting the application HTTP port to 80:
```sh
# may need root permissions to bind a process on port 80!
$ start -Dhttp.port=80
```
 * Variation: a front-end HTTP server + Play HTTP servers (load balance, scalability, fault tolerance)

### Set-up with Apache
```xml
LoadModule proxy_module modules/mod_proxy.so
…
<VirtualHost *:80>
  ProxyPreserveHost On
  ServerName www.loadbalancedapp.com
  ProxyPass  /excluded !
  ProxyPass / http://127.0.0.1:9000/
  ProxyPassReverse / http://127.0.0.1:9000/
</VirtualHost>
```

### Advanced proxy settings
* When using an HTTP frontal server, request addresses are seen as coming from the HTTP server. In a usual set-up, where you both have the Play app and the proxy running on the same machine, the Play app will see the requests coming from 127.0.0.1.
* Proxy servers can add a specific header to the request to tell the proxied application where the request came from. Most web servers will add an X-Forwarded-For header with the remote client IP address as first argument. If you enable the forward support in the XForwardedSupport configuration, Play will change the request.remoteAddress from the proxy’s IP to the client’s IP. You have to list the IP addresses of your proxy servers for this to work.
* However, the host header is untouched, it’ll remain issued by the proxy. If you use Apache 2.x, you can add a directive like:
```xml
ProxyPreserveHost on
```
* The host: header will be the original host request header issued by the client. By combining theses two techniques, your app will appear to be directly exposed.
* If you don’t want this play app to occupy the whole root, add an exclusion directive to the proxy config:
```xml
ProxyPass /excluded !
```

### Apache as a front proxy settings
* The basic idea is to run two Play instances of your web application and let the front-end proxy load-balance them. In case one is not available, it will forward all the requests to the available one.
* Let’s start the same Play application two times: one on port 9999 and one on port 9998.
```sh
$ start -Dhttp.port=9998
$ start -Dhttp.port=9999
```
* Now, let’s configure our Apache web server to have a load balancer:
```xml
<VirtualHost mysuperwebapp.com:80>
  ServerName mysuperwebapp.com
  <Location /balancer-manager>
    SetHandler balancer-manager
    Order Deny,Allow
    Deny from all
    Allow from .mysuperwebapp.com
  </Location>
  <Proxy balancer://mycluster>
    BalancerMember http://localhost:9999
    BalancerMember http://localhost:9998 status=+H
  </Proxy>
  <Proxy *>
    Order Allow,Deny
    Allow From All
  </Proxy>
  ProxyPreserveHost On
  ProxyPass /balancer-manager !
  ProxyPass / balancer://mycluster/
  ProxyPassReverse / http://localhost:9999/
  ProxyPassReverse / http://localhost:9998/
</VirtualHost>
```
* The important part is balancer://mycluster. This declares a load balancer. The +H option means that the second Play application is on stand-by. But you can also instruct it to load-balance.
* Apache also provides a way to view the status of your cluster. Simply point your browser to /balancer-manager to view the current status of your clusters.
* Because Play is completely stateless you don’t have to manage sessions between the 2 clusters. You can actually easily scale to more than 2 Play instances.

### Set-up with lighttpd
* much easier to configure than Apache, if you need virtual hosting or load balancing
```sh
# vi /etc/lighttpd/lighttpd.conf
server.modules = (
    "mod_access",
    "mod_proxy",
    "mod_accesslog" 
)
…
$HTTP["host"] =~ "www.myapp.com" {
    proxy.balance = "round-robin" proxy.server = ( "/" =>
        ( ( "host" => "127.0.0.1", "port" => 9000 ) ) )
}
 
$HTTP["host"] =~ "www.loadbalancedapp.com" {
    proxy.balance = "round-robin" proxy.server = ( "/" => ( 
        ( "host" => "127.0.0.1", "port" => 9001 ), 
        ( "host" => "127.0.0.1", "port" => 9002 ) ) 
    )
}
```

# Install Play
## Prerequisites
* JDK v6 or later
  * JDK v1.7.0 preferred
```sh
# echo $JAVA_HOME
/usr/java/jdk1.7.0_25
# java -version
java version "1.7.0_25"
Java(TM) SE Runtime Environment (build 1.7.0_25-b15)
Java HotSpot(TM) 64-Bit Server VM (build 23.25-b01, mixed mode)
# javac -version
javac 1.7.0_25
```

## Download and Install
* Download
```sh
# wget http://downloads.typesafe.com/play/2.1.3/play-2.1.3.zip
# unzip ./play-2.1.3.zip; mv play-2.1.3 /usr/;
```
* Build
```sh
# cd /usr/play-2.1.3/; cd framework/; ./build;
> publish-local
```
* Add Path
```sh
vi /etc/bashrc
...
export PATH=$PATH:/usr/play-2.1.3
```
* Check play
```sh
# which play
/usr/play-2.1.3/play
# play help
```
* Add Iptables rule
```sh
# vi /etc/sysconfig/iptables
...
*filter
...
-A INPUT -m state --state NEW -m tcp -p tcp --dport 9000 -j ACCEPT
...
# service iptables restart
```

## Sample Hello World Application
```sh
# cd /usr/play-2.1.3/samples/java/helloworld;
# play run
http://localhost:9000/
```

# Develop Play Application
* Create new Play Application
```sh
# cd ~/; play new test-app
The new application will be created in /root/test-app

What is the application name? [test-app]
> test-app

Which template do you want to use for this new application? 

  1             - Create a simple Scala application
  2             - Create a simple Java application

> 2
OK, application test-app is created.

Have fun!
```
* Run the newly created Play Server Application (development mode)
  * Ctrl+D will quit the Play Application
```sh
# cd ~/test-app/; play run
[info] Loading project definition from /root/test-app/project
[info] Set current project to test-app (in build file:/root/test-app/)

[info] Updating {file:/root/test-app/}test-app...
[info] Resolving org.hibernate.javax.persistence#hibernate-jpa-2.0-api;1.0.1.Fin                                                                                [info] Done updating.                                                        
--- (Running the application from SBT, auto-reloading is enabled) ---

[info] play - Listening for HTTP on /0:0:0:0:0:0:0:0:9000

(Server started, use Ctrl+D to stop and go back to the console...)

[info] Compiling 4 Scala sources and 2 Java sources to /root/test-app/target/scala-2.10/classes...
[info] play - Application started (Dev)

--- (RELOAD) ---

[info] play - Application started (Dev)
```
* Run the application on the Web
  * Localhost can be substituted by the real web url (e.g. 192.168.0.69): [http://localhost:9000/](http://localhost:9000/)
* Play Production mode Start
  * Ctrl+D will stop the console, but the process will run in background mode continuously
  * RUNNING_PID is the running pid of the Play Application
  * See logs/application.log for running Play log
  * Ctrl+C will kill both JVMs: the Play console and the forked Play server
```sh
# cd ~/test-app/; play start;
Ctrl+D
```
* Staging the Play Application:
  * If you don’t have Play installed on the server, use the Scala build tool sbt: "sbt clean compile stage;"
```sh
# cd ~/test-app/; play clean compile stage
# target/start;
```
* Creating a standalone version of the Play Application
  * Build a binary version of the application and deploy it to the server without any dependencies on Play itself:
```sh
# cd ~/test-app/; play dist
[info] Loading project definition from /root/test-app/project
[info] Set current project to test-app (in build file:/root/test-app/)
[info] Wrote /root/test-app/target/scala-2.10/test-app_2.10-1.0-SNAPSHOT.pom

Your application is ready in /root/test-app/dist/test-app-1.0-SNAPSHOT.zip

[success] Total time: 2 s, completed Sep 9, 2013 5:42:56 PM
```
  * Or include application configuration file like this:
```sh
# play -Dconfig.file=/root/test-app/conf/application.conf dist
[info] Loading project definition from /root/test-app/project
[info] Set current project to test-app (in build file:/root/test-app/)
[info] Wrote /root/test-app/target/scala-2.10/test-app_2.10-1.0-SNAPSHOT.pom

Your application is ready in /root/test-app/dist/test-app-1.0-SNAPSHOT.zip

[success] Total time: 2 s, completed Sep 9, 2013 5:49:05 PM
```
  * Run the packed application:
```sh
# cp ~/test-app/dist/test-app-1.0-SNAPSHOT.zip ~/dest/to/;
# cd ~/dest/to/; unzip ./test-app-1.0-SNAPSHOT.zip; cd test-app-1.0-SNAPSHOT/;
# chmod a+x start/; ./start
# Ctrl+C
```
  * Or you can make the program running in the background:
```sh
# Ctrl+Z
# bg; exit;
# ssh <dest-server>;
# cd ~/dest/to/test-app-1.0-SNAPSHOT/; cat RUNNING_PID;
6069
# kill -9 6069; rm -rf RUNNING_PID;
```
  * ZIP file's structure will be like this:
```sh
test-app-1.0-SNAPSHOT
 └ lib
    └ *.jar
 └ start
```
  * Publishing to a Maven (or Ivy) repository: [link](http://www.playframework.com/documentation/2.0/ProductionDist)
* Consult the Play documentation:
  * Valid for development mode - [http://localhost:9000/@documentation](http://localhost:9000/@documentation)

# Play Framework Java JSON Handling
* [http://www.playframework.com/documentation/2.1.3/JavaJsonRequests]

# Play Framework Java Documentation
* [http://www.playframework.com/documentation/2.1.3/JavaHome]

# Play Framework Example Project
* Java TODO List Project (by Play): [http://www.playframework.com/documentation/2.1.3/JavaTodoList]
* Blog Project: [http://iam1492.tistory.com/23]