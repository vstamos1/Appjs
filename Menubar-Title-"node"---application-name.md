When running AppJS your application may be displayed as "node". To change this you can do the following:

# Windows / Linux

In app.js enter the following line of code at the start of the script

`process.title = 'My Cool Application';`

# Mac

This "should" work cross platform and at some time in the future it will. However currently in Nodejs on Mac this does not work, for example see this forum post: https://groups.google.com/forum/?fromgroups=#!topic/nodejs/3rwMNkkRC60. We suggest you still add the process.title line into your scripts so they work cross platform. However until this is fixed then Shadab Ahmed (https://github.com/shadabahmed) found the following smart workaround:

> You can meanwhile create a soft link to node -> MyAppName and change the sh script to call MyAppName

