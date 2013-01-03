Appjs is cross platform (Windows / MacOs / Linux). 

## Windows

The following guide worked on a fresh install of windows 7 on 2013-01-03.

There are two main ways to prepare a machine to be able to compile the appjs source code. One involves using the [MozillaBuild](https://wiki.mozilla.org/MozillaBuild) environment, check the appjs forums for information on this method. The other method is documented here. We start from a completely new install of windows 7 and then go through all of the necessary steps to get a full working environment. Skip any steps that are already setup on your machine.

### NPM / node-gyp
The first step involves creating a working npm environment that is able to compile C++ modules.
* Go to [nodejs.org](http://nodejs.org/) and click on the install button to get the latest version of node.
* Click on the "Node.js Command Prompt" link and then type in:

      npm install -g node-gyp 
* Install python (version 2.7.3 since version 3.* versions are not compatible).
* Create an environment variable PYTHON = <install directory>\python.exe

### C++ Compiler setup
This section details using the free visual studio express edition since that is available for all. 

* Download the Microsoft Visual Studio C++ 2010 Express (http://go.microsoft.com/?linkid=9709949)
 * This link is a web installer and it installs a lot of stuff (2.3 gig)
 * install includes .Net Framework 4 and Microsoft SQL Server Compact

* For windows 7 you will also need to download and install Microsoft Windows SDK for Windows 7
  * Link is another web installer that installs a further 1.6 gig
  * http://www.microsoft.com/en-us/download/details.aspx?displayLang=en&id=8279

You can run all of the above installers without restarting your machine. Once that is done 