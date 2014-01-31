# Welcome to AppJS

**AppJS** is an SDK to develop **desktop applications** using **Node.js melded with Chromium**. 

With AppJS you can develop desktop tools and applications using the same libraries and knowledge used to build websites and web applications. You get all the following in one package:

* JS, HTML5, CSS, SVG, WebGL — by Chromium
* mature HTTP/HTTPS servers and client APIs — by Node.js
* filesystem, DNS, cryptography, subprocesses, OS APIs — by Node.js
* sandboxed code execution environements, virtual machines — by Node.js
* tools for exposing native C++ bindings to JavaScript — by Node.js

**_IRC: [#appjs](http://webchat.freenode.net/?channels=#appjs) on freenode. You are welcome !_**

[Map view](http://jrvis.com/red-dwarf/?user=appjs&repo=appjs) of the stars to the AppJS github repo

## AppJS and Rich Internet Application frameworks already tested
  * [Qooxdoo](http://www.qooxdoo.org/)
  * [ExtJS/Sencha](http://www.sencha.com/products/extjs)
  * [Durandal](http://durandaljs.com/)

## Getting Started
These are some of the first pages you should read, they're very short and will get you familiar with how simple it is to develop applications with AppJS!
 * [App Folder Structure](/appjs/appjs/wiki/App-Folder-Structure): an overview of the anatomy of an AppJS application.
 * [app object](/appjs/appjs/wiki/app-object): the `app` object creates windows and menus.
 * [CEF Events](/appjs/appjs/wiki/CEF-Events): a list of events that fire so you can set up listeners instead of making [gordian knots](http://en.wikipedia.org/wiki/Gordian_Knot) from callback functions.
 * [Packaging Your App.](/appjs/appjs/wiki/Packaging-Your-App.): since AppJS applications are inherently portable, there isn't much to packaging them up.
 * [Community Apps.](/appjs/appjs/wiki/Community-Apps): a list of applications built on AppJS.

Then, check out the code samples listed below or just browse the [wiki pages](/appjs/appjs/wiki/_pages).

There is an [in depth tutorial](http://www.studiochris.us/2012/creating-your-first-appjs-app-with-custom-chrome/) available elsewhere, it may help.
## Code samples

**Deploying nodejs in AppJS**
  * [Use DOM events to coordinate execution and using Nodejs's "process" and "require" with the DOM](./Node's-"process"-and-"require"-in-your-app)
  * [Adding nodejs's "module", "require", and "process" to the browser global object](./Add-Node-in-the-browser-global-object)
  * [Extending nodejs's module system into the browser context](./Extending-node's-module-system-into-the-browser-context)
  * [Node's console into Chrome's console](./Node's-console-into-Chrome's-console)

**Using nodejs, node modules, and javascript in AppJS**
  * [Install and use a third party nodejs module](./Install-and-use-a-third-party-nodejs-module)
  * [Injecting jQuery into a page and scraping links](./Injecting-jQuery-into-a-page-and-scraping-links)
  * [Using express to handle local http requests](./Using-express-3-to-handle-local-http-requests)


**Debugging**
  * [Show Chrome Console with F12 keybind](./Show-devtools-with-F12-keybind)

**Clipboard**
  * [Copy text in the OS clipboard](./Clipboard-Copy)
  * [Paste text in the OS clipboard](./Clipboard-Paste)

**HTML5**
  * [Drag & Drop from desktop](./HTML5:-Drag-&-Drop-from-Desktop)
  * [Read local files](./HTML5:-Read-local-files) (Drag & Drop based)

## Building AppJS
If you would like to build AppJS from source, there are directions at [Building AppJS](https://github.com/appjs/appjs/blob/master/docs/building.md)