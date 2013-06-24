# Sencha ExtJS

# About

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
 * Clear Data Builder (CDB): a code generator that can create a CRUD application immediately, will have HTML/JavaScript/ExtJS client and Java-based server
* Evaluation Version from Sencha

# Hello ExtJS Project for Eclipse
* Eclipse --> File --> New --> Other --> JavaScript Project --> helloExtJS --> Create a separate root folder
* helloExtJS --> script --> New --> JavaScript Source File --> test.js --> Generate comments --> Finish
* Run As --> Java2Script Application
