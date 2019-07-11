---
title: "Bower, the browser package manager"
description: "Bower defines itself as a browser package manager, and it’s a powerful tool to manage your project assets: javascript, CSS and images."
date: 2013-05-25T09:07:49+02:00
tags: devtools
---

> Warning: this post is old and might not reflect the current state of the art

[Bower](https://bower.io/) defines itself as a browser package manager, and it’s a powerful tool to manage your project assets: [JavaScript](/javascript/), CSS and images. Here I’ll only talk about JavaScript as it’s my main use case.

Let’s start, install it.

`npm install bower -g`

Now create a .bowerrc file in your project root (where you’ll invoke bower) or in your home folder, and add some customization: for example here we tell bower to install packages in the subfolder javascript/components, and use a file named ‘bower.json’ to store its data.

    {
      "directory" : "javascript/components",
      "json" : "bower.json"
    }

The bower.json file is the same thing as the package.json file for [npm](/npm/) packages in [Node.js](/nodejs/), except it’s for assets.

Let’s start by adding to your project something popular: jQuery.

You can install it by typing

`bower install --save jquery`

And by referencing the newly installed package in your HTML code:

`<script src="javascript/components/jquery/jquery.js"></script>`

The –save option tells bower to add the entry to the bower.json file, so it will be easy to recreate the same packages structure later, just like with NPM in Node.js.

Once this package is installed, it’s super easy to jump to a newer jQuery release:

`bower update jquery`

The bower project maintains a list of popular packages on their servers so you can install them easily. [Here you can find a list of them](http://sindresorhus.com/bower-components), ordered by popularity.

Of course there are thousands of projects not included, and you can install every git-powered software by using the git:// protocol, like:

`bower install git://github.com/desandro/masonry`

or just any path

`bower install http://foo.com/jquery.awesome-plugin.js`

Bower is smart enough to install a specific tag or commit of a package you’re interested in, if you need a previous version for compatibility or you don’t need to upgrade to a newer package:

`bower install git://github.com/components/jquery.git#~1.8.1`

Uninstalling a packages is simple as well:

`bower uninstall jquery`

I really like using Bower especially when it comes to upgrade dependencies from time to time, instead of wandering across multiple [Github](/github) projects (when we’re lucky enough to have a Github page), a simple `bower update` will take care of everything, except making sure everything still works on your project. That’s our job :-)
