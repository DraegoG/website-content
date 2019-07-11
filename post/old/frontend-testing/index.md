---
title: Introduction to Frontend Testing
description: How to start with testing frontend applications using Mocha and Chai
date: 2013-07-20T09:07:21+02:00
tags: devtools
---

> Warning: this post is old and might not reflect the current state of the art

Mocha is an awesome and versatile testing tool. There are many testing frameworks out there, and I choose Mocha because of its popularity and ease of use.

Let's first see how to run the tests in a browser. Download

- [https://github.com/visionmedia/mocha](https://github.com/visionmedia/mocha)
- [https://github.com/chaijs/chai](https://github.com/chaijs/chai)
- [https://github.com/chaijs/chai-jquery](https://github.com/chaijs/chai-jquery)

---

Put the respective mocha.js, chai.js, chai-jquery.js files in a test/ subfolder on your site.

Pick your index.html file and load them, then we'll setup Mocha to use the BDD testing style and we'll load in a file called test.web.js, that will host our testing rules.

```html
<script src="test/vendor/mocha.js" data-build-exclude="true"></script>
<script src="test/vendor/chai.js" data-build-exclude="true"></script>
<script src="test/vendor/chai-jquery.js" data-build-exclude="true"></script>
<script data-build-exclude="true">
  mocha.setup('bdd');
  expect = chai.expect;
</script>
<script src="test/test.web.js" data-build-exclude="true"></script>
```

Inside your body, put a div#mocha:

```html
<div id="mocha"></div>
```

the test/test.web.js file is the main piece of the game, and it will host the testing rules.

```js
describe('Array', function(){
  describe('#indexOf()', function(){
    it('should return -1 when the value is not present', function(){
      [1,2,3].indexOf(5).should.equal(-1);
      [1,2,3].indexOf(0).should.equal(-1);
    })
  })
})

describe('After this', function() {
  it('should be logged in', function(done) {
    expect($('#the-main-div')).to.exist;
    done();
  });
});
```

Those tests can now be run inside the browser, by opening the browser console an typing `mocha.run()`.

This is great as while the tests run, you can watch the screen change and read the console messages.

Using [PhantomJS](http://phantomjs.org/) - an headless WebKit implementation - you can run the tests in the terminal. The downside is that PhantomJS is not the real environment where your code will execute, but it's better for automatic detection of problems.

How to do it? Download and install PhantomJS. Install Mocha using the global [npm](/npm/) installation: `npm install -g mocha`. Download this package [https://github.com/Backbonist/front-tests](https://github.com/Backbonist/front-tests), and put it in your project directory, under test/ for example.

You can then run your tests by calling `phantomjs run-mocha.js http://test-site.com`

The problem with this approach is that you can't programmatically execute the tests run in the real environment where they will run.
That's not really a problem when still building prototypes and developing prior to opening to the public, but when in production you don't want to run the test suite from the browser every time you want to test. On every browser, right?
[**Testem**](https://github.com/airportyh/testem) is made for this. It's just a test runner, testing framework agnostic, so it can run Mocha, Jasmine, QUnit or what you use.

1. `$ npm install testem -g`

2. go in the test directory of your app, type `$ testem`

3. open the browser to the specified location to run the tests.

You can run the tests on any browser you want by launching them, or tell testem to run the tests for you by launching

`$ testem -l Chrome,Safari`

You can also use testem in CI (Continuous Integration) mode.

`$ testem ci`

this automatically launches the tests the browser specified and outputs in a format named TAP, which is readable by us humans, and can be inputted in a continuous integration server to automate the process.

# Browser testing

You'll be probably developing your site on Chrome or Firefox: their developer tools are awesome, and they help you speed up the process.

Google Chrome has separate versions you can use to test your website on. The stable and normal version, and Chrome Canary.

Canary is a browser you can run side by side with the normal Google Chrome. Its advantage is that you get daily updates of what's committed to the Chromium sources, and you can get access to new features 11 weeks before they're sent to the main stable Chrome channel, and [file bugs](http://crbug.com/) if you need. You can even set it as your default browser.

Mozilla has its own [Firefox Nightly](http://nightly.mozilla.org/) that does the same thing as Chrome canary: daily updates will come to your browser.

You might want to use the [Chrome Dev channel](http://www.chromium.org/getting-involved/dev-channel), and [Firefox Aurora](http://www.mozilla.org/it/firefox/channel/) which represent a 'less on-the-edge' version then Canary/Nightly.

To test Safari you can use the [WebKit Nightly Builds](http://nightly.webkit.org/). When you use WebKit, you are basically running Safari with an updated version of the underlying engine.
