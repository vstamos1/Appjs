```javascript
var fs = require('fs'),
    appjs = require('appjs');

var window = appjs.createWindow('http://appjs.org');

window.on('ready', function(){
  var document = window.document;
  var script = document.createElement('script');
  script.src = 'http://code.jquery.com/jquery-1.7.2.min.js';
  script.onload = function(){
    var $ = window.$;
    document.body.removeChild(script);

    var links = [];
    $('a').each(function(i, el){
      links.push({
        text: el.textContent.trim(),
        href: el.href.trim()
      });
    });
    fs.writeFileSync('./links.json', JSON.stringify(links, null, '  '));
    appjs.exit();
  };
  document.body.appendChild(script);
});
```
