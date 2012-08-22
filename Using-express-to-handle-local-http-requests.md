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