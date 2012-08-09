# Examples
Example dump that needs organizing.

### Use DOM events to coordinate execution and using Node's process and require with the DOM
__app.js__
```javascript
var appjs = require('appjs');

appjs.serveFilesFrom(__dirname + '/content');

var window = appjs.createWindow('/');

window.on('ready', function(){
  window.frame.show();
  window.require = require;
  window.process = process;
  window.module = module;

  window.addEventListener('app-done', function(e){
    console.log(e);
  });

  window.dispatchEvent(new window.Event('app-ready'));
});
```
__./content/index.html__
```html
<!doctype html>
<html>
  <head>
    <meta charset="utf8">
    <title>My App</title>
  </head>
  <body>

    <div id="main">
      <h1>Paths:</h1>
      <ul id="paths"></ul>
    </div>

    <script src="browser-main.js"></script>

  </body>
</html>
```
__./content/browser-main.js__
```javascript
addEventListener('app-ready', function(e){
  var fs   = require('fs'),
      path = require('path'),
      cwd  = process.cwd(),
      ul   = document.getElementById('paths');

  fs.readdirSync(cwd).forEach(function(child){
    var li = document.createElement('li');
    li.textContent = path.resolve(cwd, child);
    ul.appendChild(li);
  });

  window.dispatchEvent(new Event('app-done'));
});
```

***

### Injecting jQuery into a page and scraping links

```javascript
var fs = require('fs'),
    appjs = require('appjs');

var window = appjs.createWindow('http://appjs.org');

window.on('ready', function(){
  var document = window.document;
  var script = document.createElement('script');
  script.src = 'http://code.jquery.com/jquery-1.7.2.min.js';
  script.onload = function(){
    var $ = window.$;
    document.body.removeChild(script);

    var links = [];
    $('a').each(function(i, el){
      links.push({
        text: el.textContent.trim(),
        href: el.href.trim()
      });
    });
    fs.writeFileSync('./links.json', JSON.stringify(links, null, '  '));
    appjs.exit();
  };
  document.body.appendChild(script);
});
```


***

### Adding node's module, require, and process to the browser global object

```javascript
var appjs = require('appjs');

appjs.router.get('/', function(request, response){
  response.send(200, 'hello');
});

var window = appjs.createWindow();

window.on('ready', function(){
  window.frame.show();
  window.require = require;
  window.process = process;
  window.module = module;
});
```

***

### Show devtools with F12 keybind

```javascript
var appjs = require('appjs');

appjs.router.get('/', function(request, response){
  response.send(200, 'hello');
});

appjs.createWindow().on('ready', function(){
  this.frame.show();
  this.addEventListener('keydown', function(e){
    if (e.keyIdentifier === 'F12') {
      this.frame.openDevTools();
    }
  });
});
```


***

### Extending node's module system into the browser context
```javascript
require('appjs')
 .serveFilesFrom(__dirname + '/content')
 .createWindow()
 .on('ready', function(){
  this.frame.show().center();
  this.Function('return '+function(require, process, Buffer){
    var Module = require('module'),
        path = require('path'),
        nodeCompile = Module.prototype._compile

    Module.prototype._compile = function(content, filename){
      if (inBrowser) {
        return browserCompile.call(this, content, filename);
      } else {
        return nodeCompile.call(this, content, filename);
      }
    };

    var inBrowser = true;
    // entry point is here, currently loads browser-main.js
    document.mainModule = require('./browser-main');
    inBrowser = false;

    function browserCompile(content, filename) {
      var self = this;
      this.exports = {};
      this.children = [];
      content = content.replace(/^\#\!.*/, '');

      function require(request){
        inBrowser = true;
        request = self.require(request);
        inBrowser = false;
        return request;
      }

      require.resolve = function(request){
        return Module._resolveFilename(request, self);
      };

      require.main = document.mainModule;
      var argNames = ['exports', 'require', 'module', '__filename', '__dirname', 'global', 'process', 'Buffer', content];
      var args = [this.exports, require, this, filename, path.dirname(filename), window, process, Buffer];
      return Function.apply(null, argNames).apply(this.exports, args);
    }
  })().call(this, require, process, Buffer);
});
```


***

### Using express to handle local http requests
```javascript
var express = require('express'), // express 2.5.9
    appjs = require('appjs'),
    utils = require('util');

// Create express server for routing
var appRouter = express.createServer();
appRouter.use(express.bodyParser());
appRouter.register('jade', require('jade').express);

/**
 * Set up the express routes
 */
appRouter.get('/', function(req, res, next){
  res.render('index.jade', { layout: false });
});

appRouter.all('/page/*', function(req, res, next){
  // User should logged in
  if (req.LoggedUser) {
    next();
  } else {
    // User is not logged in, stop request and render login page
    res.status(401).render("login.jade", { layout: false });
  }
});


// Routing for view posts on a blog page 
appRouter.get('/page/:page_id/posts/:post_id', function(req, res, next){
  if (req.params.page_id && req.params.post_id) {
    var page_id = parseInt(req.params.page_id, 10);
    var post_id = parseInt(req.params.post_id, 10);
    res.send(200, "You selected page " + page_id + " and post number " + post_id);
  } else {
    res.send(412, "You should select a correct page_id and post_id");
  }
});

/**
 * Setup AppJS
 */

// override AppJS's built in request handler with connect
appjs.router.handle = appRouter.handle.bind(appRouter);

// create window
var window = appjs.createWindow({
  width : 640,
  height: 460,
  icons : __dirname + '/content/icons'
});

// show the window after initialization
window.on('create', function(){
  window.frame.show();
  window.frame.center();
});

// add require/process/module to the window global object for debugging from the DevTools
window.on('ready', function(){
  window.require = require;
  window.process = process;
  window.module = module;
  window.addEventListener('keydown', function(e){
    if (e.keyIdentifier === 'F12') {
      window.frame.openDevTools();
    }
  });
});
```