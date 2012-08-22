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
