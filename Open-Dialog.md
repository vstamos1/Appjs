
    window.frame.openDialog({
        type: 'open', // Either open or save
        title: 'Open...', // Dialog title, default is window title
        multiSelect: false, // Allows multiple file selection
        dirSelect:true, // Directory selector
        initialValue:'c:\\Program Files' // Initial save or open file name
    }, function( err , files ) {
        // save the file using fs module according to files array.
    });

