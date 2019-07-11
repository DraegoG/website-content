---
title: Deferreds and Promises in JavaScript (+ Ember.js example)
description: Promises are a relatively new approach to async management, and they can be really helpful to structure your code
date: 2013-09-15T09:07:39+02:00
tags: js
---

> Warning: this post is old and might not reflect the current state of the art

> Check out my [Promises guide](/javascript-promises/) and my [async/await guide](/javascript-async-await/) instead.

[Promises](/javascript-promises/) are a relatively new approach to async management, and they can be really helpful to structure your code.

A Promise is an object representation of an event. In the course of its life, a Promise goes from a pending state, when it’s called, to a resolved or rejected state, when it’s been completed, or it could also stay pending forever and is never resolved.

It’s a sort of new approach to [JavaScript](/javascript/) events, but I think it generates way more readable code, and it’s less quirky. At the moment there are 2 slightly different main implementations of Promises in javascript: those libraries that follow the Promises/A spec, and jQuery.

First I’ll take jQuery into consideration as it’s everywhere and I use it, so if you don’t want another external library, you can use it.

# Introducing jQuery promises

Let’s introduce the concept of Deferred. First, a Deferred is a Promise, with in addition the fact that you can trigger a Deferred (resolve or reject it), while with a Promise, you can only add callbacks and it will be triggered by something else.
A Promise, if you want, is a ‘listen-only’ part of a Deferred.

A clear example of this is this function

```js
var promise = $('div.alert').fadeIn().promise();
```

You can now add .done() & .fail() to handle the callbacks.
This is just a call example, promises for animations have become a real deal in jQuery 1.8, also with callbacks for progress.

Another example of a promise is an AJAX call:

```js
var promise = $.get(url);
promise.done(function(data) {});
```

A deferred is something you create, set the callbacks and resolve, like:

```js
var deferred = new $.Deferred();
deferred.done(function(data) { console.log(data) });
deferred.resolve('some data');
```


The state of a deferred can be triggered using .resolve() or .reject(). Once a deferred state has been changed to one of the final stages (resolved/rejected), it can’t be changed any more.

```js
var deferred = new $.Deferred();
deferred.state();  // "pending"
deferred.resolve();
deferred.state();  // "resolved"
```

We can attach the following callbacks to a promise:

```js
.done() //will run when the promise has been executed successfully
.fail() //will run when the promise has failed
.always() //will run in either cases
```

Those callbacks can be called together using `.then()`, like:

```js
promise.then(doneFunc, failFunc, alwaysFunc);
```

This is just an intro to the jQuery implementation of Promises and Deferreds. Let’s write some real-word examples.
(if executing in node, you can import jQuery by using `$ = require(‘jquery’);` )

# Some jQuery examples
For example, here we execute a function, and when it’s finished it calls dfd.resolve(). Similar to doing a callback, but more structured and reusable.

```js
$.when(execution()).then(executionDone);

function execution(data) {
  var dfd = $.Deferred();
  console.log('start execution');

  //in the real world, this would probably make an AJAX call.
  setTimeout(function() { dfd.resolve() }, 2000);

  return dfd.promise();
}

function executionDone(){
  console.log('execution ended');
}
```

Here the elements of an array are processed, and once all of them are fine (e.g. a request has returned), I call another function. We start to see the real benefits of the Deferred usage. The $.when.apply() method is used to group the dfd.resolve() in the loop.

```js
var data = [1,2,3,4]; // the ids coming back from serviceA
var processItemsDeferred = [];

for(var i = 0; i < data.length; i++){
  processItemsDeferred.push(processItem(data[i]));
}

$.when.apply($, processItemsDeferred).then(everythingDone);

function processItem(data) {
  var dfd = $.Deferred();
  console.log('called processItem');

  //in the real world, this would probably make an AJAX call.
  setTimeout(function() { dfd.resolve() }, 2000);

  return dfd.promise();
}

function everythingDone(){
  console.log('processed all items');
}
```


A slightly more complex example, here the elements of the array are fetched from an external resource, using var fetchItemIdsDeferred = fetchItemIds(data) and fetchItemIdsDeferred.done()

```js
var data = []; // the ids coming back from serviceA
var fetchItemIdsDeferred = fetchItemIds(data); // has to add the ids to data

function fetchItemIds(data){
  var dfd = $.Deferred();
  console.log('calling fetchItemIds');

  data.push(1);
  data.push(2);
  data.push(3);
  data.push(4);

  setTimeout(function() { dfd.resolve() }, 1000);
  return dfd.promise();
}

fetchItemIdsDeferred.done(function() { // if fetchItemIds successful...
  var processItemsDeferred = [];

  for(var i = 0; i < data.length; i++){
    processItemsDeferred.push(processItem(data[i]));
  }

  $.when.apply($, processItemsDeferred).then(everythingDone);
});


function processItem(data) {
  var dfd = $.Deferred();
  console.log('called processItem');

  //in the real world, this would probably make an AJAX call.
  setTimeout(function() { dfd.resolve() }, 2000);

  return dfd.promise();
}

function everythingDone(){
  console.log('processed all items');
}
```


Those last 2 examples explain how to compute a for cycle and then wait for the end of the processing execution to do something.

It’s the less “hacky” way of doing this:

```js
var allProcessed = false;
var countProcessed = 0;
for (var i = 0, len = theArray.length; i < len; i++) {
  (function(i) {
    // do things with i
        if (++countProcessed === len) allProcessed = true;
  })(i);
}
```


Now another example of how Deferreds can be used for: take a look at this

```js
var interval = setInterval(function() {
  if (App.value) {
    clearInterval(interval);
    // do things
  }
}, 100);
```


This is a construct that evaluates a condition; if the condition is true, the code clears the interval and executes the code contained in the if.

This is useful for example to check when a value is not undefined any more:

```js
var DeferredHelper = {
  objectVariableIsSet: function(object, variableName) {
    var dfd = $.Deferred();

    var interval = setInterval(function() {
      if (object[variableName] !== undefined) {
        clearInterval(interval);
        console.log('objectVariableIsSet');
        dfd.resolve()
      }
    }, 10);

    return dfd.promise();
  },

  arrayContainsElements: function(array) {
    var dfd = $.Deferred();

    var interval = setInterval(function() {
      if (array.length > 0) {
        clearInterval(interval);
        console.log('arrayContainsElements');
        dfd.resolve()
      }
    }, 10);

    return dfd.promise();
  }
}

var executeThis = function() {
  console.log('ok!');
}

var object = {};
object.var = undefined;
var array = [];

$.when(DeferredHelper.arrayContainsElements(array)).then(executeThis);
$.when(DeferredHelper.objectVariableIsSet(object, 'var')).then(executeThis);

setTimeout(function() {
  object.var = 2;
  array.push(2);
  array.push(3);
}, 2000);
```


The above example is in fact 3 examples in one. I created a DeferredHelper object and its methods arrayContainsElements and objectVariableIsSet are self-explaining.

Keep in mind that primitive types are passed by value, so you can’t do

```js
var integerIsGreaterThanZero = function(integer) {
  var dfd = $.Deferred();

  var interval = setInterval(function() {
    if (integer > 0) {
      clearInterval(interval);
      dfd.resolve()
    }
  }, 10);

  return dfd.promise();
};

var variable = 0;

$.when(integerIsGreaterThanZero(variable)).then(executeThis);
```


nor you can do

```js
var object = null;

var variableIsSet = function(object) {
  var dfd = $.Deferred();

  var interval = setInterval(function() {
    if (object !== undefined) {
      clearInterval(interval);
      console.log('variableIsSet');
      dfd.resolve()
    }
  }, 10);

  return dfd.promise();
};

$.when(variableIsSet(object)).then(executeThis);

setTimeout(function() {
  object = {};
}, 2000);
```


because when doing object = {}, the object reference is changed, and as Javascript actually references variables by copy-reference, the reference of the object variable inside the variableIsSet function is not the same as the outer object variable.

# An ember.js example

A thing I use with Ember.js is

```js
App.DeferredHelper = {

  /**
    * Check if an array has elements on the App global object if object
    * is not set.
    * If object is set, check on that object.
    */
  arrayContainsElements: function(arrayName, object) {
    var dfd = $.Deferred();
    if (!object) object = App;

    var interval = setInterval(function() {
      if (object.get(arrayName).length > 0) {
        clearInterval(interval);
        dfd.resolve()
      }
    }, 50);

    return dfd.promise();
  },

  /**
    * Check if a variable is set on the App global object if object
    * is not set.
    * If object is set, check on that object.
    */
  variableIsSet: function(variableName, object) {
    var dfd = $.Deferred();
    if (!object) object = App;

    var interval = setInterval(function() {
      if (object.get(variableName) !== undefined) {
        clearInterval(interval);
        dfd.resolve()
      }
    }, 50);

    return dfd.promise();
  }
}
```


so I can do in my client code:

```js
$.when(App.DeferredHelper.arrayContainsElements('itemsController.content'))
  .then(function() {
  //do things
});
```


and

```js
$.when(App.DeferredHelper.variableIsSet('aVariable'))
  .then(function() {
  //do things
});

//&

$.when(App.DeferredHelper.variableIsSet('aVariable', anObject))
  .then(function() {
  //do things
});
```


All those examples were made using the jQuery deferreds implementation.

If you’re not willing to use the jQuery deferred implementation, maybe because you’re not using jQuery and loading it just for the deferreds is overkill, or you’re using another library that does not have a deferred implementation, you can use other libraries specialized in this, such as [Q](https://github.com/kriskowal/q), [rsvp.js](https://github.com/tildeio/rsvp.js), [when.js](https://github.com/cujojs/when).

# Let’s write some examples using when.js

For example, I have the ID of an item, and I want to call the API endpoint to get more detail about it. Once the AJAX call returns, continue processing.

```js
function processItem(item) {
  var deferred = when.defer();

  var request = $.ajax({
    url: '/api/itemDetails',
    type: 'GET'
    data: {
      item: item
    }
  });

  request.done(function(response) {
    deferred.resolve(JSON.parse(response));
  });

  request.fail(function(response) {
    deferred.reject('error');
  });

  return deferred.promise;
}

var item = {
  id: 1
}

processItem(item).then(
  function gotIt(itemDetail) {
    console.log(itemDetail);
  },
  function doh(err) {
    console.error(err);
  }
);
```


I got some ID values from a server, process them using the processItem() function from above, and then once finished processing ALL of them, I can do something

```js
function processItems(anArray) {
  var deferreds = [];

  for (var i = 0, len = anArray.length; i < len; i++) {
    deferreds.push(processItem(anArray[i].id));
  }

  return when.all(deferreds);
}

var anArray = [1, 2, 3, 4];

processItems(anArray).then(
  function gotEm(itemsArray) {
    console.log(itemsArray);
  },
  function doh(err) {
    console.error(err);
  }
);
```


The when.js library provides some utility methods such as when.any() and when.some(), that let the deferred callback run when 1) one of the promises has been solved 2) at least a specified number of promises have returned.
