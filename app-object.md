var window = app.createWindow({
  width  : 1024,
  height : 768,
  icons  : __dirname + '/content/icons',
  showChrome : false,
  alpha: true,
  autoResize: false,
  resizable: true,
  margin: 0
 
  /***************************** defaults ********************************
* url            : 'http://appjs', // serve static file root and routers
* autoResize     : false,          // resizes in response to html content
* showChrome     : true,           // show border and title bar
* resizable      : false,          // control if users can resize window
* disableSecurity: true,           // allow cross origin requests
* opacity        : 1,              // flat percent opacity for window
* alpha          : false,          // per-pixel alpha blended (Win & Mac)
* fullscreen     : false,          // client area covers whole screen
* left           : -1,             // centered by default
* top            : -1,             // centered by default
*************************************************************************/
 
});

var menubar = app.createMenu([{
  label:'&File',
  submenu:[
    {
      label:'E&xit',
      action: function(){
        window.close();
      }
    }
  ]
},{
  label:'&Window',
  submenu:[
    {
      label:'Fullscreen',
      action:function(item) {
        window.frame.fullscreen();
        console.log(item.label+" called.");
      }
    },
    {
      label:'Minimize',
      action:function(){
        window.frame.minimize();
      }
    },
    {
      label:'Maximize',
      action:function(){
        window.frame.maximize();
      }
    },{
      label:''//separator
    },{
      label:'Restore',
      action:function(){
        window.frame.restore();
      }
    }
  ]
}]);

menubar.on('select',function(item){
  console.log("menu item "+item.label+" clicked");
});

var trayMenu = app.createMenu([{
  label:'Show',
  action:function(){
    window.frame.show();
  },
},{
  label:'Minimize',
  action:function(){
    window.frame.hide();
  }
},{
  label:'Exit',
  action:function(){
    window.close();
  }
}]);

var statusIcon = app.createStatusIcon({
  icon:'./data/content/icons/32.png',
  tooltip:'AppJS Hello World',
  menu:trayMenu
});