# PHP Development with CodeIgniter
## Prerequisites
* install [APM first](https://github.com/kimduho/webdev/wiki/Installing-APM---Apache-PHP-MySQL)

## About
* features
 * Model-View-Controller Based System
 * Extremely Light Weight
 * Full Featured database classes with support for several platforms.
 * Query Builder Database Support
 * Form and Data Validation
 * Security and XSS Filtering
 * Session Management
 * Email Sending Class. Supports Attachments, HTML/Text email, multiple protocols (sendmail, SMTP, and Mail) and more.
 * Image Manipulation Library (cropping, resizing, rotating, etc.). Supports GD, ImageMagick, and NetPBM
 * File Uploading Class
 * FTP Class
 * Localization
 * Pagination
 * Data Encryption
 * Benchmarking
 * Full Page Caching
 * Error Logging
 * Application Profiling
 * Calendaring Class
 * User Agent Class
 * Zip Encoding Class
 * Template Engine Class
 * Trackback Class
 * XML-RPC Library
 * Unit Testing Class
 * Search-engine Friendly URLs
 * Flexible URI Routing
 * Support for Hooks and Class Extensions
 * Large library of “helper” functions
* application flow chart
![Application Flow Chart of CodeIgniter](http://www.codeigniter.com/userguide3/_images/appflowchart.gif)
 * ~/index.php: initial router
 * ~system/core/CodeIgniter.php: bootstrapping file --> **shows the overall loading procedure**
 * configuration: ~/application/config/config.php --> stored in $config array, 'log_threshold' sets logging condition
 * hook points: prep_system, pre_controller, post_controller_constructor, post_controller, display_override, cache_override, post_system

## Install CodeIgniter on CentOS v6.4 Linux
* [home](http://www.codeigniter.com/)
 * [download](https://github.com/bcit-ci/CodeIgniter/archive/3.0rc3.zip)
 * [manual](http://www.codeigniter.com/userguide3/)
* general 4 steps
 * Unzip the package.
 * Upload the CodeIgniter folders and files to your server. Normally the index.php file will be at your root.
 * Open the application/config/config.php file with a text editor and set your base URL. If you intend to use encryption or sessions, set your encryption key.
 * If you intend to use a database, open the application/config/database.php file with a text editor and set your database settings.
* security handling
 * If you wish to increase security by hiding the location of your CodeIgniter files you can rename the system and application folders to something more private. If you do rename them, you must open your main index.php file and set the $system_path and $application_folder variables at the top of the file with the new name you’ve chosen.
 * For the best security, both the system and any application folders should be placed above web root so that they are not directly accessible via a browser. By default, .htaccess files are included in each folder to help prevent direct access, but it is best to remove them from public access entirely in case the web server configuration changes or doesn’t abide by the .htaccess.

## Develop Basic Application
* Creating a Controller: ~application/controllers/
```sh
# cp -r /home/workspace/CodeIgniter-3.0rc3 /var/www/html/CodeApp;
# cd /var/www/html/CodeApp/; cd ~/application/controllers/
# cp ./Welcome.php ./blog.php; vi ./Blog.php
<?php
defined('BASEPATH') OR exit('No direct script access allowed');
class Blog extends CI_Controller {
    public function index()
    {
        echo "Hello Duho Kim!";
    }
}
# wget http://localhost/CodeApp/index.php/Blog
```
* Creating a Model: ~/application/models/
 * change the DB connection password: [for mysql](https://github.com/kimduho/webdev/wiki/MySQL_Basics)
 * set DB connection environment: e.g. MySQL
```sh
# vi ~/application/config/database.php
<?php  if ( ! defined('BASEPATH')) exit('No direct script access allowed');
$active_group = 'default';
$active_record = TRUE;

$db['default']['hostname'] = 'localhost';
$db['default']['username'] = 'root';
$db['default']['password'] = '<password_value>';
$db['default']['database'] = 'testdb'; // <database_name>
$db['default']['dbdriver'] = 'mysql'; // mysql, postgres, odbc, etc.
$db['default']['dbprefix'] = ''; // optional table prefix for table name when running Active Record queries
$db['default']['pconnect'] = TRUE; // whether to use a persistent connection
$db['default']['db_debug'] = TRUE; // whether DB errors should be displayed or not
$db['default']['cache_on'] = FALSE;
$db['default']['cachedir'] = ''; // absolute server path to DB query cache directory
$db['default']['char_set'] = 'utf8';
$db['default']['dbcollat'] = 'utf8_general_ci'; // character collation used in communicating with the DB
$db['default']['swap_pre'] = ''; // useful for distributed applications
$db['default']['autoinit'] = TRUE; // whether or not to automatically connect to the DB when the library loads
$db['default']['stricton'] = FALSE; // whether to force "Strict Mode" connections (ensuring strict SQL)
/* End of file database.php */
# 
```sh
* Use Session info
```sh
# vi ~/application/config/config.php
...
$config['sess_use_database']    = TRUE;
$config['sess_table_name']      = 'ci_sessions';

$config['sess_cookie_name']     = 'ci_session';
$config['sess_expiration']      = 86400; // secs
$config['sess_expire_on_close'] = FALSE;
$config['sess_encrypt_cookie']  = FALSE;
$config['sess_match_ip']        = FALSE;
$config['sess_match_useragent'] = TRUE;
$config['sess_time_to_update']  = 300;
...
```
* Create DB schema and insert some data
```sh
# mkdir -p ~/sql; cd ~/sql; vi test_database.sql
SET SQL_MODE = "NO_AUTO_VALUE_ON_ZERO";
SET time_zone = "+00:00";
CREATE TABLE IF NOT EXISTS  `ci_sessions` (
	session_id varchar(40) DEFAULT '0' NOT NULL,
	ip_address varchar(45) DEFAULT '0' NOT NULL,
	user_agent varchar(120) NOT NULL,
	last_activity int(10) unsigned DEFAULT 0 NOT NULL,
	user_data text NOT NULL,
	PRIMARY KEY (session_id),
	KEY `last_activity_idx` (`last_activity`)
);

```
 * create some page: ~/application/models/test_model.php
```sh
<?php if ( ! defined('BASEPATH')) exit('No direct script access allowed');
class Test_model extends CI_Model {
  function get()
  {
    $query = $this->db->get_where('test', array('classify' => 'general'));
    return $query->result();
  }
}
```
* Creating a View: ~application/views/

## Simple Usage
* Copy CodeIgniter Template to new name CodeApp
```sh
# cd /var/www/html; cp -r ./CodeIgniter-3.0rc3 ./CodeApp
```
* Web connect to the CodeApp
 * [CodeApp-here](http://localhost/CodeApp/)

## User Guide
* install user guide
```sh
# cd /var/www/html/; mkdir -p ./CodeIgniter3; cd ./CodeIgniter3;
# wget http://www.codeigniter.com/data/CodeIgniter3-userguide.zip
# unzip ./CodeIgniter3-userguide.zip; 
```
* [local - user guide](http://localhost/CodeIgniter3/user_guide/)
* Useful User Guides
 * [Very Simple Basic Guide](http://codesamplez.com/development/codeigniter-basic-tutorial)
 * [CodeIgniter Tutorial - Learn CodeIgniter in 40 minutes](http://www.revillweb.com/tutorials/codeigniter-tutorial-learn-codeigniter-in-40-minutes/)
 * [Beginners Guide to CodeIgniter](https://www.udemy.com/codeigniter-learn-it-correct/)
 * [CodeIgniter Framework Basic Tutorial](http://www.phpeveryday.com/articles/CodeIgniter-Framework-Basic-Tutorial-P841.html)
 * [CodeIgniter: Getting Started with a Simple Example](https://www.digitalocean.com/community/tutorials/codeigniter-getting-started-with-a-simple-example)