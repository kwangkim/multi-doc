# About ExtJS 4 theming
* supported in ExtJS 4
* user can customize the look of an application while still supporting all browsers
* SASS
 * [SASS URL](http://sass-lang.com/)
 * a pre-processor which adds new syntax to CSS allowing for things like variables, mixins, nesting, and math/color functions
 * will be compiled to CSS
* Compass
 * [Compass link](http://compass-style.org/docs/)
 * extends CASS by adding a variety of CSS3 mixins and by providing the extension system that ExtJS leverages
 * compresses CSS output

## Installations
* JDK (JRE v1.7 +)
* ruby
* rubygems
* ExtJS v4.2 +
* Sencha Cmd
 * Code generation tool, Javascript compiler, lightweight web server, package management system, tuning tools, workspace management, flexible configuration system, etc.
 * compatible: with ExtJS v4.1.1 +, Sencha Touch v2.1 +
 * do not install or use deprecated Sencha SDK Tools v2
 * [download sencha command](http://www.sencha.com/products/sencha-cmd/download/)
```sh
# sencha upgrade --check
# sencha upgrade
# sencha
Sencha Cmd v4.0.1.45
...
```
* command basics
 * sencha [ category ] [ command ] [ options... ] [ arguments... ]
 * sencha help [ module ] [ action ]
 * sencha help

## Basic Environments
* Setup the workspace
```sh
# sencha -sdk ~/ext-4.2.0 generate workspace my-workspace;
```
* Application generation
```sh
# cd my-workspace; sencha -sdk ext generate app ThemeDemoApp theme-demo-app;
# cd theme-demo-app; sencha app build;
```
* Running application
 * development mode: my-workspace/theme-demo-app/index.html
 * production mode: my-workspace/build/ThemeDemoApp/production/index.html
* theme package structure
 * package.json - package properties file
 * sass/var/ - contains SASS variables
 * sass/src/ - contains SASS rules and UI mixin calls
 * sass/etc/ - contains additional utility functions or mixins
 * resources/ - contains images and other static resources that your theme requires
 * overrides/ - contains any JavaScript overrides to ExtJS component classes that may be required for theming those components
* New theme generation
```sh
# sencha generate theme my-custom-theme
# cd my-workspace/; vi packages/my-custom-theme/package.json;
"extend": "ext-theme-neptune"
# cd my-workspace/theme-demo-app/; sencha app refresh;
```
* Configure & build global theme variables
```sh
# cd my-workspace/packages/my-custom-theme/; vi sass/var/Component.scss
$base-color: #317040 !default;
# cd my-workspace/packages/my-custom-theme/; sencha package build;
```
 * using the theme in an application
```sh
# cd my-workspace/theme-demo-app/; vi .sencha/app/sencha.cfg
...
app.theme=my-custom-theme
...
# cd my-workspace/theme-demo-app/; sencha ant clean; sencha app build;
```
* Configure & build component variables
```sh
# cd my-workspace/packages/my-custom-theme/; mkdir -p sass/var/panel/; vi sass/var/panel/Panel.scss
...
$panel-header-font-family: Times New Roman !default;
# cd my-workspace/theme-demo-app/; sencha app build;
```
* Creating custom component UIs (css mixins)
```sh
# cd my-workspace/packages/my-custom-theme/; vi sass/src/panel/Panel.scss
...
@include extjs-panel-ui(
    $ui-label: 'highlight-framed',       # <-- custom 'highlight' UI
    $ui-header-background-color: red,
    $ui-border-color: red,
    $ui-header-header-border-color: red,
    $ui-body-border-color: red,
    $ui-border-width: 5px,
    $ui-border-radius: 5px
);
# 
```
 * using custom component UIs
```sh
# cd my-workspace/theme-demo-app/; vi app/view/Viewport.js
items: [{
    // default UI
    region: 'west',
    xtype: 'panel',
    title: 'West',
    split: true,
    width: 150
}, {
    // custom "highlight" UI
    region: 'center',
    xtype: 'panel',
    layout: 'fit',
    bodyPadding: 20,
    items: [
        {
            xtype: 'panel',
            ui: 'highlight',    <-- highlight-framed UI
            frame: true,
            bodyPadding: 10,
            title: 'Highlight Panel'
        }
    ]
}, {
    // neptune "light" UI
    region: 'east',
    xtype: 'panel',
    ui: 'light',
    title: 'East',
    split: true,
    width: 150
}]
# cd my-workspace/theme-demo-app/; sencha app build;
```
* theme Javascript overrides
```sh
# cd my-workspace/packages/my-custom-theme/; vi overrides/panel/Panel.js
...
Ext.define('MyCustomTheme.panel.Panel', {
    override: 'Ext.panel.Panel',
    titleAlign: 'center'
});
# cd my-workspace/packages/my-custom-theme/; sencha package build;
# cd my-workspace/theme-demo-app/; sencha app refresh; sencha app build;
```