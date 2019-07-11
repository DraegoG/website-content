---
title: Introduction to Yeoman
description: "Yeoman is one of the cool kids in the yard, a combined effort of a lot of respectable developers to provide a tool that simplifies the setup and management of web app projects"
date: 2013-04-25T09:06:40+02:00
tags: devtools
---

> Warning: this post is old and might not reflect the current state of the art

Yeoman is one of the cool kids in the yard, a combined effort of a lot of respectable developers to provide a tool that simplifies the setup and management of web app projects: less time spent in learning X different tools, more consistency and ease of use.

There are a lot of points of interest in Yeoman, the most important of them are:

- it is built upon rock-solid tools to provide an easy access and quick, no-brainer use of them. Does not re-invent the wheel.
- it is a scaffolding tool for the most popular frameworks, think Bootstrap, Ember.js, Angular.js, Backbone.js
- thanks to [Bower](https://bower.io) (a frontend package manager similar to Jam, Volo, Ender - but better), it has quick install, uninstall and update helpers for common libs such as jQuery, Underscore.js, Modernizer, Mocha, Backbone, and any Bower package already in place.
- it has testing built-in, using mocha against a PhantomJS (headless browser) instance when launched from the command line, or otherwise tests run in the browser when you open the test/index.html page in the browser.
- it provides a python HTTP server to test out your code. When the webserver is running, it listens for file changes in your project and reloads the browser when the page you have open has dependencies on a file that changed. So, you don't even need a backend in place before starting writing the frontend code.

Building an Yeoman project is easy.
First, install it:

`$ curl -L get.yeoman.io | sh`

Then enter in an empty directory and type

`$ yeoman init`

This will present you a welcome screen, and a list of options of what you'd like to add to the project.

You can start a new Ember.js project by typing

`$ yeoman init ember`

This creates a new Ember.js app, creates a basic set of models, controllers and views/templates (and their directories), adds the script tags for all dependencies (jQuery, Handlebars) and creates an index.html file based on the HTML5 boilerplate project http://html5boilerplate.com/.

You can use Yeoman to bootstrap the project, update dependencies in your project, run tests and so on.
And, when the project is ready for deployment, you can take advantage of Grunt https://github.com/cowboy/grunt built in Yeoman by calling "yeoman build", so that it lints, compiles everything for production, concatenates and minifies script and styles, compresses images and so on.


