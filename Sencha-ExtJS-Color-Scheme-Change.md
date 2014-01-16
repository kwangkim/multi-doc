# Sencha ExtJS Color Scheme Change
* Custom theme structure
 * index.html
<link rel="stylesheet" type="text/css" href="extjs/resources/css/ext-all-custom.css" />
 * extjs/resources/css/ext-all-custom.css
@import '../ext-theme-custom/ext-theme-custom-all.css';
 * cp -r extjs/resources/ext-theme-neptune extjs/resources/ext-theme-custom;
 * vi extjs/resources/css/ext-all-muse.css
* Pick a source color code
 * Use Linux GIMP --> Change Foreground Color --> Spoid --> get HTML codes
```sh
# vi extjs/resources/ext-theme-muse/ext-theme-muse-all.css
```
* Pick a destination color code
 * In preferred design photo, use Linux GIMP --> Change Foreground Color --> Spoid --> get HTML codes
 * vi extjs/resources/ext-theme-muse/ext-theme-muse-all.css
* Change color code
 * from Linux vi command, do the following:
```sh
# vi extjs/resources/ext-theme-muse/ext-theme-muse-all.css
/#2A6D9E
:%s/#2A6D9E/#AABBCC/g
```