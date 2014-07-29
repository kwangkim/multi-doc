# Squirrel-SQL
* open source freeware
 * SQuirreL SQL Client is a graphical SQL client written in Java that will allow you to view the structure of a JDBC compliant database, browse the data in tables, issue SQL commands etc.
 * License: GPLv2, LGPLv2
 * [site](http://www.squirrelsql.org/)
* preparations
 * installation of VNC: [here](https://github.com/kimduho/linux/wiki/Linux-VNC-Server-Client-Configurations)
 * installation of java and ant: [here](https://github.com/kimduho/javadev/wiki/Basic-Java-Development-Tools), install IBM's Java SDK 7 instead of Oracle's (needs an IBM ID)
```sh
# export JAVA_HOME=/opt/ibm/java-x86_64-71
# export CLASSPATH=$JAVA_HOME/lib
# export PATH=$JAVA_HOME/bin:$PATH
# which java
# java -version
java version "1.7.0"
Java(TM) SE Runtime Environment (build pxa6470_27sr1-20140411_01(SR1))
IBM J9 VM (build 2.7, JRE 1.7.0 Linux amd64-64 Compressed References 20140410_195893 (JIT enabled, AOT enabled)
J9VM - R27_Java727_SR1_20140410_1931_B195893
JIT  - tr.r13.java_20140410_61421
GC   - R27_Java727_SR1_20140410_1931_B195893_CMPRSS
J9CL - 20140410_195893)
JCL - 20140409_01 based on Oracle 7u55-b13
# ant -version
Apache Ant version 1.7.1 compiled on August 24 2010
```
* installation - by source
```sh
# git clone git://git.code.sf.net/p/squirrel-sql/git squirrel-sql-git
# cd ./squirrel-sql-git/archive/squirrel; ./configure; ./build
# java -jar squirrel-sql-<version>-install.jar
```
* installation - by binary
 * binary will be installed on /usr/local/squirrel-sql-3.5.3
 * select [v] MySQL, Oracle, PostgreSQL, Optional Translation - Korean
 * after installation, delete the installation path /usr/squirrel-sql;
 * execute by Desktop Icon: SQuirreL SQL Client
```sh
# wget http://downloads.sourceforge.net/project/squirrel-sql/1-stable/3.5.3/squirrel-sql-3.5.3-standard.jar?r=http%3A%2F%2Fsquirrel-sql.sourceforge.net%2F&ts=1406609125&use_mirror=superb-dca2
# mkdir -p /usr/squirrel-sql; mv ./squirrel-sql-3.5.3-standard.jar /usr/squirrel-sql; cd /usr/squirrel-sql;
# java -jar squirrel-sql-3.5.3-standard.jar; # execute with VNC client connection
```
* usage
 * [here](http://www.squirrelsql.org/index.php?page=screenshots)
* detailed installation & usage can be found [here](http://db.apache.org/derby/integrate/SQuirreL_Derby.html).
