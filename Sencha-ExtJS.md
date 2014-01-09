# Sencha ExtJS

# About
## Ext vs. ExtJS
* Ext Core: Javascript framework (e.g. jQuery, prototype)
* ExtJS: UI, Theme based on Ext Core
* jQuery (Javascript utilities) vs. ExtJS (UI Javascript framework, heavier than jQuery)

## Download ExtJS
* [4.2.1-GPL here](http://cdn.sencha.com/ext/gpl/ext-4.2.1-gpl.zip)

# Development
## Eclipse JavaScript Plugins
* Eclipse Web Development Tools
```
Eclipse-->Install-->New Software -->
Work with: Juno - http://download.eclipse.org/releases/juno -->
Web, XML, Java EE and OSGi Enterprise Development:
Eclipse Web Developer Tools, Eclipse XML Editors and Tools, JavaScript Development Tools
```
* VJET JavaScript IDE: Mozilla Public License (MPL)
* helloJS
```
Eclipse-->File-->New-->JavaScript Project-->helloJS-->Create a separate root folder
```

## Hello JavaScript Example
* File --> New --> Other --> Web --> Static Web Project --> helloHTML
* WebContent --> New --> HTML File --> hello.html --> [v] Use HTML Template
--> New HTML File (5)
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Hello JavaScript</title>
	<script src="test.js"></script>
</head>
<body>
	<h3 id="reportName">This is a User Info:</h3>
	<p id="guestName">David, Kim</p>
	<p id="guestAddr">Gangnam Gu, Seoul</p>
	<p id="guestTele">010-3333-7777</p>
</body>
</html>
```
* WebContent-->New-->Other-->JavaScript/JavaScript Source File-->test.js
 * use Ctrl+Space to auto-complete!
```html
function init() {
	var guest = document.getElementById("reportName");
	guets.innerHTML = "oder info...";
}

window.onload = init;
```

## Eclipse Plugin for Sencha ExtJS
* ExtJS JSDT Integration
 * JSDT (Java Script Development Tools) plugin
```
http://extjs.w3des.net/p2/
Eclipse --> Help --> Eclipse MarketPlace --> ExtJS --> ExtJS JSDT Integration --> "Install"
Copyright (C) 2013 Dawid Paku\u0142a - w3des.net
THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
```
* Clear Toolkit for ExtJS - Open Source Freeware from Farata Systems
 * Clear Toolkit is not an architectural framework. It is a set of components, code generators, and plugins that extend Apache Flex framework and tools built on top of these components that substantially increase productivity of the enterprise JavaScript and Flex developers.
 * Clear Data Builder (CDB): a code generator that can create a CRUD application immediately, will have HTML/JavaScript/ExtJS client and Java-based server
 * Install Prerequisites-1
```
Missing requirement: ClearDataBuilder for Ext JS 1.0.0.201301242238 (com.farata.cleardatabuilder.extjs 1.0.0.201301242238) requires 'bundle org.eclipse.jpt.common.core 0.0.0' but it could not be found
# Eclipse-->Install-->Web,XML,Java EE and OSGi Enterprise Development
 [v] Dali Java Persistence Tools - check all 6 related items
```
 * Install Prerequisites-2
```
Missing requirement: ClearDataBuilder for Ext JS 1.0.0.201301242238 (com.farata.cleardatabuilder.extjs 1.0.0.201301242238) requires 'bundle org.eclipse.jst.servlet.ui 0.0.0' but it could not be found
# Install Eclipse Java EE
```
 * Download & Install CDB v4.1.4
```
# wget http://cleartoolkit.com/downloads/plugins/extjs/cleardatabuilder/4.1.4/site.zip
# mv site.zip ClearDataBuilder.zip
# Eclipse-->Help-->Install New Software-->Add-->Archive-->ClearDataBuilder.zip
-->OK-->[v]ClearDataBuilder for Ext JS, v1.0-->Next-->
# restart Eclipse...
```
* Evaluation Version from Sencha (just for reference)

# Hello ExtJS @CDB Project for Eclipse
* Eclipse-->File-->New-->Other-->ClearDataBuilder for Ext JS Project-->New Clear Data Builder Project
 * Project name: helloCDB
 * Type: Apache Tomcat v7.0, Persistence Platform: None

# ExtJS Tutorial
* MapFish's ExtJS Tutorial: [here](http://mapfish.org/doc/tutorials/extjs.html)
* Sencha ExtJS: [here](https://www.sencha.com/store/extjs/), [about](http://www.sencha.com/products/extjs/)
 * Examples of Ext JS 4.2.1: [here](http://docs.sencha.com/extjs/4.2.1/#!/example)
 * License: Ext JS 4 + Standard Support (1 Developer Pack): $595.00
 * Ext JS 4.2 documents: [here](http://docs.sencha.com/extjs/4.2.1/)
 * Getting Started with Ext JS 4.2.1: [here](http://docs.sencha.com/extjs/4.2.1/#!/guide/getting_started-section-1-requirements)

# Sencha ExtJS Theme Build
## About
* Can compress (or minify) JavaScript codes internally using YUI Compressor

## Install 
* Sencha SDK Tools (latest: v2.0.0 beta3)
 * You may fail to install / execute if you: install on x86_64, virtual machine, using command line
 * you may see the following errors:
```sh
$ sencha
execvp(): No such file or directory
```
 * install 32bit libraries if you encounter errors
```sh
# you may see the following errors:
```
 * The following environments are automatically added to your user shell environment
```sh
export PATH=/opt/SenchaSDKTools-2.0.0-beta3:$PATH
export SENCHA_SDK_TOOLS_2_0_0_BETA3="/opt/SenchaSDKTools-2.0.0-beta3"
```
