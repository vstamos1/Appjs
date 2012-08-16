Here supplement https://github.com/appjs/appjs/blob/master/docs/building.md document.
Here is a question like [this](https://github.com/appjs/appjs/issues/147)
***
View you app with commend'data\bin\node.exe --harmony data\app.js',but not'data\bin\node.exe data\app.js',because it uses ECMAScript Harmony features internally.
---(thanks  Mithgol)
***
But for short I would recommend to download the pre-build packages from here: 30-second-quickstart (find the linked Windows package - I assume you are running on Windows because you often mention app.exe).

Then simple use the content of your downloaded pre-build package as a scaffold for your projects.

Its pretty easy to get started by just editing the content of the content folder.
 But first let me lighten up your path at first.
 The app.exe will call the node.exe from the data\bin folder with the paramter of app.js
 And now everything becomes clear because in app.js its defined to load all your business logic from data\content by trying to find the index.html

All you need to edit is the index.html file from data\content folder and link to your business logic/assets or what ever you are trying to hack with JavaScript.

The node_modules folder contains all the dependencies which are required to run app.js.
---(thanks  fibric)
So now you can edit a .BAT file,and change it to .exe([Q[Quick Batch File Compiler](http://www.abyssmedia.com/quickbfc/) ,something software like this can do that,with you cool icon)

So now you can use VS to create a setup project, you simply create a setup project, 'appjs' file folder drag and drop to the project generates can be very simple.You can easily do.(The first time I did it :p).

***
However, flaws, obviously, your application files are open.Everyone can modify your web files.
We will add the solution,as soon as we can.