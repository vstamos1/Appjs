# Examples
Example dump that needs organizing.

### Injecting jQuery into a page and scraping links

```javascript
var fs = require('fs'),
    appjs = require('appjs');

var window = appjs.createWindow({
  url: 'http://appjs.org'
});

window.on('ready', function(){
  var document = window.document;
  var script = document.createElement('script');
  script.src = 'http://code.jquery.com/jquery-1.7.2.min.js';
  script.onload = function(){
    document.body.removeChild(script);
    init(window.$, document);
  };
  document.body.appendChild(script);
});


function init($, document){
  $("<h1>I'M IN YOUR WEBSITE INJECTING INTO YOUR CODES</h1>").prependTo(document.body);
  var links = [];
  $('a').each(function(i, el){
    links.push({
      text: el.textContent.trim(),
      href: el.href.trim()
    });
  });
  fs.writeFileSync('./links.json', JSON.stringify(links, null, '  '));
}
```


### Adding node's module, require, and process to the browser global object

```javascript
var app = require('appjs');

app.router.get('/', function(request, response){
  response.send('');
});

var window = app.createWindow();

window.on('ready', function(){
  window.frame.show();
  window.require = require;
  window.process = process;
  window.module = module;
});
```

### Show devtools with F12 keybind

```javascript
var app = require('appjs');

app.router.get('/', function(request, response){
  response.send('');
});

var window = app.createWindow();
window.on('ready', function(){
  window.frame.show();
  window.addEventListener('keydown', function(e){
    if (e.keyIdentifier === 'F12') {
      window.frame.openDevTools();
    }
  });
});
```



### Extending node's module system into the browser context
```javascript
require('appjs').serveFilesFrom(__dirname + '/content').createWindow().on('ready', function(){
  this.frame.show();
  this.frame.center();
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