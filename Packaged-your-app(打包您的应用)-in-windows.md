Here supplement https://github.com/appjs/appjs/blob/master/docs/building.md document.
Here is a question like [this](https://github.com/appjs/appjs/issues/147)
***
View you app with commend
```Batch
data\bin\node.exe --harmony data\app.js
```
,but not
```Batch
data\bin\node.exe data\app.js
```
,because it uses ECMAScript Harmony features internally.
---(thanks  Mithgol)
***

_**But for sho_rt I would recommend to download the pre-build packages from here:**_
 _**[30-second-quick](https://github.com/appjs/appjs#30-second-quickstart) start (find the linked Windows package - I assume you are running on Windows because you often mention app.exe).**_

_**Then simple use the content of your downloaded pre-build package as a scaffold for your projects.**_

_**Its pretty easy to get started by just editing the content of the content folder.**_
 _**But first let me lighten up your path at first.**_
 _**The app.exe will call the node.exe from the data\bin folder with the paramter of app.js**_
 _**And now everything becomes clear because in app.js its defined to load all your business logic from data\content by trying to find the index.html**_

_**All you need to edit is the index.html file from data\content folder and link to your business logic/assets or what ever you are trying to hack with JavaScript.**_

_**The node_modules folder contains all the dependencies which are required to run app.js.**_
---(thanks  fibric)

_So no_w you can edit a .BAT file,and change it to .exe([Quick Batch File Compiler](http://www.abyssmedia.com/quickbfc/) ,something software like this can do that,with you cool icon)

So now you can use VS to create a setup project, you simply create a setup project, 'appjs' file folder drag and drop to the project generates can be very simple.You can easily do.(The first time I did it :p).

***
However, flaws, obviously, your application files are open.Everyone can modify your web files.
We will add the solution,as soon as we can.