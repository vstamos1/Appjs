You can not make something like readFile('myFile.txt'); in HTML5. Don't forget there is nodejs behind appjs, so you can use nodejs to readfile of course. But let's say you are trying to make an app which can be both on a webserver or an appjs one, you will play with form, and, why not, HTML5.

You will find really usefull information here : http://www.html5rocks.com/en/tutorials/file/dndfiles/

So let's continue our drag & drop files code, but this time, let's read files content ;)


```javascript


var readStart = function(progressEvent) {
    console.log('readStart',progressEvent);
}

var readEnd = function(progressEvent) {
    console.log('readEnd',progressEvent,this);
    var fileReader = this;
    var fileContent = fileReader.result;
    var fileName = fileReader.file.name;
    // Note you can not retreive file path, for security reasons. 
    // But you are not supposed to need it, you already have the content ;)
    console.log('readEnd:',fileName,fileContent);
}

var readProgress = function(progressEvent) {
    console.log('readProgress',progressEvent);
    if (progressEvent.lengthComputable) {
        var percentage = Math.round((event.loaded * 100) / event.total);
        console.log('readProgress: Loaded : '+percentage+'%');
    }
}

var readError = function(progressEvent) {
    console.log('readError',progressEvent);
    switch(progressEvent.target.error.code) {
        case progressEvent.target.error.NOT_FOUND_ERR:
            alert('File not found!');
            break;
        case progressEvent.target.error.NOT_READABLE_ERR:
            alert('File not readable!');
            break;
        case progressEvent.target.error.ABORT_ERR:
            break; 
        default: 
            alert('Unknow Read error.');
    }
}

var readFile = function(file) {
    var reader = new FileReader();
    reader.file = file; // We need it later (filename)
    reader.addEventListener('loadstart', readStart, false);
    reader.addEventListener('loadend', readEnd, false);
    reader.addEventListener('error', readError, false);
    reader.addEventListener('progress', readProgress, false);
    reader.readAsBinaryString(file);
}

var drop = function(event) {
    event.preventDefault();
    var dt = event.dataTransfer;
    var files = dt.files;
    for (var i = 0; i<files.length; i++) {
        var file = files[i];
        readFile(file);
    }
}

window.addEventListener("drop", drop);
```