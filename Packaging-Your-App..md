So you've downloaded the [quickstart app] (https://github.com/appjs/appjs#30-second-quickstart) and made something awesome. Now you want to know how to bundle it all up for distribution!

##It's Simple

If you want to provide your own application launcher instead of `app.[exe|sh]` you'll have to launch node with the harmony option and pass it `data\app.js`.

On windows it looks like this:
```Batch
data\bin\node.exe --harmony data\app.js
```

You can then use a tool to compile your launcher and add an icon. Some people have suggested using [Quick Batch File Compiler](http://www.abyssmedia.com/quickbfc/) There are different methods for each operating system and this isn't mandatory, it's just an extra touch of awesome.

Once you've got your custom launcher just zip up your project and let people download it!

##Would you like to support other operating systems?

Ok. Here's how to do it:

1. Grab the quickstart apps for all the available systems.
2. Create your custom launcher for each different system and replace the default launcher.
3. Delete `app.js` and the `content` folder in each of the quickstart examples.
4. Put a copy of your `content` folder, `app.js`, and any other files you've modified or created, into each of the quickstart examples in the same place they're at in your working copy.
5. If you've added any node modules to your project you'll need to install them into the quickstart examples as well. Some modules can just be copied and pasted, but others can't be. To be safe it would be best to use the actual operating systems you're going to deploy to, to install the modules you want to add.
6, Zip up each of your projects, you could even get fancy and use some kind of fancy installer like [IzPack](http://izpack.org/)
7. Tell people about your app!

