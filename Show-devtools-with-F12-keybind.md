
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
