Let's say you need 'native-dns' nodejs module in your appjs.

1. Install the module via nodejs npm

   Go in the '**data**' directory of your application. Type '**npm install native-dns**'. Module will be installed into node_modules directory

2. Load the module in the window ready event

   file: app.js

   ```javascript
var app = module.exports = require('appjs');
app.serveFilesFrom(__dirname + '/content');

var window = app.createWindow({
  width  : 1200,
  height : 600
});

window.on('create', function(){
  window.frame.show();
  window.frame.center();
});

window.on('ready', function(){
  window.require = require;
  window.process = process;
  window.module = module;
  window.dns = require('native-dns');

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

3. Use it !

   Somewhere in your application:

   ```javascript

var question = dns.Question({
  name: 'www.google.com',
  type: 'A'
});

var req = dns.Request({
  question: question,
  server: { address: '8.8.8.8', port: 53, type: 'udp' },
  timeout: 1000
});

req.on('timeout', function () {
  console.log('Timeout in making request');
});

req.on('message', function (err, answer) {
  answer.answer.forEach(function (a) {
    console.log(a.address);
  });
});

req.on('end', function () {
  console.log('Finished processing request');
});

req.send();
   ```
