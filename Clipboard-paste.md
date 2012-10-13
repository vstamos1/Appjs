
Very basic code :

```javascript
  document.body.onpaste = function(event) {
    if (!event.clipboardData.types) return;
    var data = event.clipboardData.getData('text/plain');
    if (!data) return;
    alert('Pasted data: '+data);
  }
```

