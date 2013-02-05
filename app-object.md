This page shows examples of the current app object API. First we show how to open a window:

    var window = app.createWindow({
       width  : 1024,
       height : 768,
       icons  : __dirname + '/content/icons', //used for application window icon
       showChrome : false,                    //display as standard os window with max/min/close buttons
       alpha: true,
       autoResize: false,            //adjust window size automatically according to content.
       resizable: true,              //allow user resize of window
       margin: 0,
       disableSecurity:true,         //turn off security restrictions.
       showResizeGrip:false,         //show/hide the resize grip.
       name:'test',                  //undocumented parameter
       left:-1,
       top:-1,
       opacity:1,
       fullscreen:false,
       topmost:false,
       
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

Following code gives an example of creating a native menu. Use & to create a shortcut key, so &File will cause Alt+F to select the File menu item on windows, other OS use the appropriate key plus the letter after the & to select it:

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

Create a tray menu to be displayed in the status bar:

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

Display a status icon and attach the `trayMenu` to it.

    var statusIcon = app.createStatusIcon({
      icon:'./data/content/icons/32.png',
      tooltip:'AppJS Hello World',
      menu:trayMenu
    });