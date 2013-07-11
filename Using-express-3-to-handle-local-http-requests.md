```javascript
var express = require('express'),
    appjs = require('appjs'),
    utils = require('util'),
    http = require('http'),
    path = require('path');
 
// Create express server
var app = express();
app.set('port', process.env.PORT || 3000);
 
app.set('views', __dirname + '/content');
app.set('view engine', 'jade');
app.use(express.bodyParser());
app.use(express.static(path.join(__dirname, 'content')));
 
/**
 * Set up the express routes
 */
app.get('/', function(req, res, next){
  res.render('index', { title: 'title' });
});
 
/**
 * Setup AppJS
 */
 
// override AppJS's built in request handler with connect
appjs.router.handle = app.handle.bind(app);
 
// have express listen on a port
http.createServer(app).listen(app.get('port'), function(){
  console.log('Express server listening on port ' + app.get('port'));
});
 
var window = appjs.createWindow('http://localhost:' + app.get('port') + '/',
 {
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
    if (e.keyIdentifier === 'F12' || e.keyCode === 74 && e.metaKey && e.altKey) {
      window.frame.openDevTools();
    }
  });
});
```