# Activator with Java Development
## About Activator
* Integrates Akka, Play, Java, etc. using Activator by Typesafe.com
* Server side: play --> run by activator
* Client UI side: bootstrap (+ vs. coffee script, etc.)

## Prerequisites
* Basic Java Development Tools - JDK 1.6+, Ant, Maven: [ref](https://github.com/kimduho/javadev/wiki/Basic-Java-Development-Tools)

## Installation
* Download Typesafe Reactive Platform - activator: from [here](http://downloads.typesafe.com/typesafe-activator/1.2.8/typesafe-activator-1.2.8.zip?_ga=1.163601271.953227967.1408496439)
* Unzip, add and export PATH
* Packages: path tree
 * /work/package/activator/  <-- activator binary, environment (you must add to PATH)
 * /work/package/bootstrap/  <-- bootstrap.js, bootstrap.css

## Development
* Generate new project
 * $ cd /work; activator new; <app_name>; select play + java;
 * or $ activator ui;
* Develop: path tree
 * /work/<app_name>/api/app/views        <-- index html
 * /work/<app_name>/api/app/controllers  <-- java main
 * /work/<app_name>/api/app/models       <-- data, database
 * /work/<app_name>/public/conf/         <-- application.conf (global variables), routes (web service API)
 * /work/<app_name>/public/javascripts/  <-- js ($ cp <path>/bootstrap.js .)
 * /work/<app_name>/public/styles/       <-- css ($ cp <path>/bootstrap.css .)
 * /work/<app_name>/public/images/       <-- favicon.png, etc.
* Run project
 * $ cd /work/<app_name>; activator run;
 * open service port: $ vi /etc/sysconfig/iptables; add port 9000; service iptables restart;
 * http://localhost:9000  <-- project is compiled in real-time (if 1st time or anything is changed)
* Change port to 8000
```sh
# vi /etc/sysconfig/iptables
-A INPUT -m state --state NEW -m tcp -p tcp --dport 8000 -j ACCEPT
# service iptables restart
# ./activator run -Dhttp.port=8000
```

## Reference Links
* [Typesafe.com Platform Getting Started](https://typesafe.com/platform/getstarted)
* [Play Framework with Java](https://www.playframework.com/documentation/2.0/JavaTodoList)
* [Understanding Bootstrap Modals](http://www.sitepoint.com/understanding-bootstrap-modals/)
* [Scala and the Play Framework (Jan 2014)](http://sett.ociweb.com/sett/settJan2014.html)
* [Creating a Modal window with HTML5 and CSS3](http://www.webdesignerdepot.com/2012/10/creating-a-modal-window-with-html5-and-css3/)
