```javascript
var drop = function(event) {
    event.preventDefault();
    var dt = event.dataTransfer;
    var files = dt.files;
    for (var i = 0; i<files.length; i++) {
        var file = files[i];
        console.log(file);
        // File is an object having lastModifiedDate, name, size, type, webkitRelativePath
    }
}

window.addEventListener("drop", drop);
```