When running AppJS your application may be displayed as "node". To change this you can do the following:

# Windows / Linux

In app.js enter the following line of code at the start of the script

`process.title = 'My Cool Application';`

# Mac

Currently there is a long term bug in nodejs that means that the process.title does not work as on other platforms. We suggest that you still add the line to your script so that when the bug is fixed your application will automatically function:

`process.title = 'My Cool Application';`

A smart workaround for now was suggested by Shadab Ahmed (https://github.com/shadabahmed)

> You can meanwhile create a soft link to node -> MyAppName and change the sh script to call MyAppName

