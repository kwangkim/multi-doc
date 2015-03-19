# PHP Development with CodeIgniter
## Prerequisites
* install [APM first](https://github.com/kimduho/webdev/wiki/Installing-APM---Apache-PHP-MySQL)

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
