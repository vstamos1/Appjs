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
