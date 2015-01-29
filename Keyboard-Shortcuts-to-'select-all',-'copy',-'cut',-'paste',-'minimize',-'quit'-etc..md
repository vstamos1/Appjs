You can create keyboard shortcuts using JavaScript __[execCommand](https://developer.mozilla.org/en-US/docs/Web/API/document.execCommand)__.

Inside the "ready" event, you need to capture the keys and insert the __execCommand__ event you want, or the native AppJs functions, as following:

```javascript
window.on('ready', function(){
  window.require = require;
  window.process = process;
  window.module = module;
  // other code . . .

  /**********************************************
  * Keyboard Shortcuts event listeners
  **********************************************/
  window.addEventListener('keydown', function(e){
    // if you want to test the keys, uncomment this log and press CMD+KEY to see the log
    // console.log(e.keyCode);

    // SELECT ALL (CMD+A)
    if (e.keyCode == 65) {
      window.document.execCommand('selectAll');
    }
    // COPY (CMD+C)
    if (e.keyCode == 67) {
      window.document.execCommand('copy');
    }
    // EXIT (CMD+M)
    if (e.keyCode == 77) {
      window.frame.minimize();
    }
    // EXIT (CMD+Q or CMD+W)
    if (e.keyCode == 81 || e.keyCode == 87) {
      window.close();
    }
    // PASTE (CMD+V)
    if (e.keyCode == 86) {
      window.document.execCommand('paste');
    }
    // CUT (CMD+X)
    if (e.keyCode == 88) {
      window.document.execCommand('cut');
    }
    if (e.keyIdentifier === 'F12' || e.keyCode === 74 && e.metaKey && e.altKey) {
      window.frame.openDevTools();
    }
  });
});

```