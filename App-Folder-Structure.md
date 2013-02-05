The directory tree below shows the default layout of an application.
* `app.[exe|sh]` The executable file which starts your application. It calls `data/bin/node[.exe] --harmony data/app.js`
* `app` : The root directory of your application.
* `data` : This directory contains the entire application.
* * `app.js` : This file sets up the Window and adds any "bootstrap" code you may want to use.
* * `bin` : This is where node is. You don't have to do anything with it.
* * `content` : This is the web root of your application. The files in here are accessed by the browser. 
* * `node_modules` : This is where you place any node modules you wish to use in your application. appjs is also a node module so it will be here.

    app/
      app.[exe|sh]
      data/
        app.js
        bin/
          node[.exe]
        content/
          index.html
          rainbowsky.jpg
          style.css
        node_modules/
          appjs/
            index.js
            package.json
            README.md
            example/
              ..
            lib/
              bindings.js
              bridge.js
              index.js
              utils.js
              window.js
              router/
                http.json
                index.js
                request.js
                response.js
                static-router.js
            node_modules/
              mime/
          appjs-<OS>/
            index.js
            package.json
            README.md
              build/
                Release/
                  appjs.node
              data/
                pak/
                  chrome.pak
                  locals/
                    ..