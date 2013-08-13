# MySQL_Basics
* [ref](https://www.digitalocean.com/community/articles/a-basic-mysql-tutorial)

# Connect to a MySQL Database
```sh
# mysql -u kimduho -p kimduhodb;
Enter password: ****************
# mysql -u kimduho -pmysecretpassword kimduhodb;
```

# Add a MySQL User
```sh
mysql> USE kimduhodb;
mysql> grant CREATE,INSERT,DELETE,UPDATE,SELECT on kimduhodb.* to kimduho@localhost;
mysql> grant ALL on kimduhodb.* to kimduho@localhost;
mysql> set password for kimduho = password('mysecretpassword');
mysql> set password for kimduho@localhost = password('mysecretpassword');
mysql> grant ALL on database.* to kimduho@'%' identified by 'mysecretpassword';
mysql> exit;
```

# Add new user into users Table
```sh
```

```sh
# mysql -u root -p
mysql> USE kimduhodb;
mysql> CREATE TABLE potluck (id INT NOT NULL PRIMARY KEY AUTO_INCREMENT, 
name VARCHAR(20),
food VARCHAR(30),
confirmed CHAR(1), 
signup_date DATE);
mysql> SHOW TABLES;
INSERT INTO `potluck` (`id`,`name`,`food`,`confirmed`,`signup_date`) VALUES (NULL, "Tina", "Salad","Y", '2012-04-10'); 
mysql> SELECT * FROM potluck;


mysql> grant CREATE,INSERT,DELETE,UPDATE,SELECT on kimduhodb.* to kimduho@localhost;
mysql> SELECT 
```

# Create and Delete a MySQL Database
```sh
# mysql -u root -p
mysql> DROP DATABASE IF EXISTS kimduhodb;
mysql> CREATE DATABASE kimduhodb;
mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| kimduhodb          |
| mysql              |
| performance_schema |
| test               |
+--------------------+
5 rows in set (0.01 sec)
mysql> DROP DATABASE kimduhodb;
```

# Access a MySQL Database
```sh
mysql> USE kimduhodb;
mysql> SHOW tables;
```

# Create a MySQL Table
```sh
mysql> CREATE TABLE potluck (id INT NOT NULL PRIMARY KEY AUTO_INCREMENT, 
name VARCHAR(20),
food VARCHAR(30),
confirmed CHAR(1), 
signup_date DATE);
mysql> SHOW TABLES;
+---------------------+
| Tables_in_kimduhodb |
+---------------------+
| potluck             |
+---------------------+
1 row in set (0.01 sec)
mysql> DESCRIBE potluck;
+-------------+-------------+------+-----+---------+----------------+
| Field       | Type        | Null | Key | Default | Extra          |
+-------------+-------------+------+-----+---------+----------------+
| id          | int(11)     | NO   | PRI | NULL    | auto_increment |
| name        | varchar(20) | YES  |     | NULL    |                |
| food        | varchar(30) | YES  |     | NULL    |                |
| confirmed   | char(1)     | YES  |     | NULL    |                |
| signup_date | date        | YES  |     | NULL    |                |
+-------------+-------------+------+-----+---------+----------------+
5 rows in set (0.01 sec)
```

# Add Information to a MySQL Table
```sh
mysql> INSERT INTO `potluck` (`id`,`name`,`food`,`confirmed`,`signup_date`) VALUES (NULL, "John", "Casserole","Y", '2012-04-11');
mysql> INSERT INTO `potluck` (`id`,`name`,`food`,`confirmed`,`signup_date`) VALUES (NULL, "Sandy", "Key Lime Tarts","N", '2012-04-14');
INSERT INTO `potluck` (`id`,`name`,`food`,`confirmed`,`signup_date`) VALUES (NULL, "Tom", "BBQ","Y", '2012-04-18');
INSERT INTO `potluck` (`id`,`name`,`food`,`confirmed`,`signup_date`) VALUES (NULL, "Tina", "Salad","Y", '2012-04-10'); 
mysql> SELECT * FROM potluck;
+----+-------+----------------+-----------+-------------+
| id | name  | food           | confirmed | signup_date |
+----+-------+----------------+-----------+-------------+
|  1 | John  | Casserole      | Y         | 2012-04-11  |
|  2 | Sandy | Key Lime Tarts | N         | 2012-04-14  |
|  3 | Tom   | BBQ            | Y         | 2012-04-18  |
|  4 | Tina  | Salad          | Y         | 2012-04-10  |
+----+-------+----------------+-----------+-------------+
4 rows in set (0.00 sec)
```

# Update Information in the Table
```sh
mysql> UPDATE `potluck` 
SET 
`confirmed` = 'Y' 
WHERE `potluck`.`name` ='Sandy';
```

# Add or Delete a Column
```sh
mysql> ALTER TABLE potluck ADD email VARCHAR(40);
mysql> ALTER TABLE potluck ADD email VARCHAR(40) AFTER name; 
mysql> ALTER TABLE potluck DROP email;
```

# Delete a Row
* DELETE from [table name] where [column name]=[field text];
```sh
mysql> DELETE from potluck  where name='Sandy';
Query OK, 1 row affected (0.00 sec)

mysql> SELECT * FROM potluck;
+----+------+-----------+-----------+-------------+
| id | name | food      | confirmed | signup_date |
+----+------+-----------+-----------+-------------+
|  1 | John | Casserole | Y         | 2012-04-11  |
|  3 | Tom  | BBQ       | Y         | 2012-04-18  |
|  4 | Tina | Salad     | Y         | 2012-04-10  |
+----+------+-----------+-----------+-------------+
3 rows in set (0.00 sec)
```

# Execute an SQL Script in MySQL
```sh
# vi employees_table.sql
USE kimduhodb;
DROP TABLE IF EXISTS employees;
CREATE TABLE employees (id INT, first_name VARCHAR(20), last_name VARCHAR(30));
INSERT INTO employees (id, first_name, last_name) VALUES (1, 'John', 'Doe');
INSERT INTO employees (id, first_name, last_name) VALUES (2, 'Bob', 'Smith');
INSERT INTO employees (id, first_name, last_name) VALUES (3, 'Jane', 'Doe');
SELECT * FROM employees;
# mysql -u root -p
mysql> SOURCE ./employees_table.sql
```
* or run using MySQL command line tool
```sh
# mysql kimduhodb < employees_table.sql;
# mysql < employees_table.sql;  # // if USE kimduhodb; statement is placed at the first statement in the file
```

# MySQL with PHP
```php
<?php
// your codes here
mysql_query('DROP TABLE IF EXISTS `kimduhodb`.`employees`') or die(mysql_error());
?>
```

# MySQL Dump & Restore
```sh
# mysqldump -u <user_id> -p <database_name> [table_name] > mysql_data_201308.sql
# mysqldump -u <user_id> -p --all-databases [--add-locks] [--default-character-set euc-kr] > mysql_data_201308.sql
# mysqldump -u <user_id> -p -d <database_name> > mysql_data_schema_201308.sql; // schema only backup
# mysql -u <user_id> -p <database_name> < mysql_data_201308.sql
# mysql -u <user_id> -p < mysql_data_201308.sql; // restore all databases
```
