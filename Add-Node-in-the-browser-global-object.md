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
