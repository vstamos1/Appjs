**WARNING: IF YOUR APPLICATION DISPLAYS EXTERNAL DATA AND IF YOU MISS A CROSS SITE SCRIPTING VULNERABILITY, IMPLEMENTING THIS FEATURE CAN BE VERY DANGEROUS**

First, you have to disable security when you create the window in appjs.js 

```javascript
var window = app.createWindow({
  disableSecurity:true
});
```

Then, add the function below in your main js code

```javascript
    Clipboard = {}; 
    Clipboard.utilities = {}; 
    Clipboard.utilities.createTextArea = function(value) { 
        var txt = document.createElement('textarea'); 
        txt.style.position = "absolute"; 
        txt.style.left = "-100%"; 
        if (value != null) txt.value = value; 
        document.body.appendChild(txt); 
        return txt; 
    }; 

    Clipboard.copy = function(data) { 
        if (data == null) return; 
        var txt = Clipboard.utilities.createTextArea(data); 
        txt.select(); 
        document.execCommand('Copy'); 
        document.body.removeChild(txt); 
    }; 
```

Now you can use Clipboard.copy('sometext') (bind a button or Ctrl+C ? as you want)
