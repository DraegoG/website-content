---
title: Using node-webkit to create a Desktop App
description: In this post I'm scratching the surface of node-webkit, by deploying and building a package for a web application, on Mac and Windows.
date: 2013-12-10T09:06:15+02:00
tags: devtools
---

> Warning: this post is old and might not reflect the current state of the art

First, a disclaimer: I’m not going to cover running [Node.js](/nodejs/) code, but just packaging a web app to run on Mac and Windows. Linux is also part of the game, but I’m not covering it.

[node-webkit](https://github.com/rogerwang/node-webkit) is, that’s how it’s called from its creators, a web runtime.

It’s based on Chromium (despite its name) and node.js. It lets us call node.js code and modules directly from the DOM, and opens new possibilities for native applications written using Web technologies.

In this post I’m just scratching the surface of it, by deploying and building a package for a web application, on Mac and Windows, just like it’s a native application.

# Run the app

First, let’s introduce the index.html file

    <html>
      <body>
        <p>test</p>
      </body>
    </html>


We also need a package.json file

    {
      "name": "My Web App",
      "main": "index.html"
    }

That’s it from the code-side! Really.

Now to run the app, download the runtime from the site [https://github.com/rogerwang/node-webkit](https://github.com/rogerwang/node-webkit) for your specific platform, and then you can call

    1)
    $ alias nw="open -n -a node-webkit '/PATH_TO_APP_DIRECTORY/'
    $ ./nw

    2)
    cd /PATH_TO_APP_DIRECTORY/
    zip -r app.nw ./

You have now created a package of the app. You can double-click it on Mac, or drag over the node-webkit application on Windows, and it will run.

There are a lot of options you can now add to the package.json file [https://github.com/rogerwang/node-webkit/wiki/Manifest-format](https://github.com/rogerwang/node-webkit/wiki/Manifest-format), but that’s a start. You can for example hide the top bar with address and debugger, set the menu items, and decide pretty much all you need.

Now, let’s dig into packaging and distributing an app.

# Package the app on the Mac

Unzip the node-webkit.app package downloaded from the node-webkit site.

Right-click, “Show package content”, go in Contents/Resources and copy there the app.nw file built with

`$ zip -r app.nw ./`

or alternatively, copy the app directory there and name it “app.nw”.

That’s it! You can now change the default icon and properties in the Contents/Info.plist file.

# Package the app on Windows

Download the latest Windows package.

Copy the .nw file built using Zip in the package directory, alongside nw.exe, and call it app.nw

Run the command

`copy /b nw.exe+app.nw app.exe`

You can now remove the nw.exe & app.nw files, zip the directory and distribute the package. Your users will need to download the zip file, uncompress and then run the app.exe file contained.

