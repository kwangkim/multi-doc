# Eclipse PDT with CodeIgniter Plug-in
## Installation
* [download Eclipse PHP Integrated Development Environment](https://www.eclipse.org/downloads/)
```sh
# tar zxvf tar zxvf eclipse-php-luna-SR2-linux-gtk-x86_64.tar.gz
# mv ./eclipse /usr/local/eclipse-php-luna-SR2
# cd /usr/local/; ln -s eclipse-php-luna-SR2 eclipsephp
# vi /usr/local/eclipsephp/eclipse.ini
-startup
plugins/org.eclipse.equinox.launcher_1.3.0.v20140415-2008.jar
--launcher.library
plugins/org.eclipse.equinox.launcher.gtk.linux.x86_64_1.1.200.v20150204-1316
-product
org.eclipse.epp.package.php.product
--launcher.defaultAction
openFile
-showsplash
org.eclipse.platform
--launcher.XXMaxPermSize
256m
--launcher.defaultAction
openFile
--launcher.appendVmargs
-vmargs
-Dosgi.requiredJavaVersion=1.7
-Xms256m
-Xmx8192m
-XX:PermSize=1024m
-XX:MaxPermSize=8192m
-XX:-UseCompressedOops
-Dorg.eclipse.swt.internal.gtk.cairoGraphics=false
```
* Eclipse Execution
 * Default Workspace: /home/workspacephp [v] save and do not ask again
 * Menu >> Help >> Eclipse Marketplace: 