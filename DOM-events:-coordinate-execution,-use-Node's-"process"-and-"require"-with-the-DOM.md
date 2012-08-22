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
