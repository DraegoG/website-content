---
title: "How to use JavaScript Classes"
description: "In 2015 the ECMAScript 6 (ES6) standard introduced classes. Learn all about them"
date: 2018-07-26T07:06:29+02:00
booktitle: Classes
tags: js
tags_weight: 8
---

In 2015 the ECMAScript 6 (ES6) standard introduced classes.

JavaScript has a quite uncommon way to implement inheritance: prototypical inheritance. [Prototypal inheritance](https://flaviocopes.com/javascript-prototypal-inheritance/), while in my opinion great, is unlike most other popular programming language's implementation of inheritance,  which is class-based.

People coming from Java or Python or other languages had a hard time understanding the intricacies of prototypal inheritance, so the ECMAScript committee decided to sprinkle syntactic sugar on top of prototypical inheritance so that it resembles how class-based inheritance works in other popular implementations.

This is important: JavaScript under the hood is still the same, and you can access an object prototype in the usual way.

## A class definition

This is how a class looks.

```js
class Person {
  constructor(name) {
    this.name = name
  }

  hello() {
    return 'Hello, I am ' + this.name + '.'
  }
}
```

A class has an identifier, which we can use to create new objects using `new ClassIdentifier()`.

When the object is initialized, the `constructor` method is called, with any parameters passed.

A class also has as many methods as it needs. In this case `hello` is a method and can be called on all objects derived from this class:

```js
const flavio = new Person('Flavio')
flavio.hello()
```

## Class inheritance

A class can extend another class, and objects initialized using that class inherit all the methods of both classes.

If the inherited class has a method with the same name as one of the classes higher in the hierarchy, the closest method takes precedence:

```js
class Programmer extends Person {
  hello() {
    return super.hello() + ' I am a programmer.'
  }
}

const flavio = new Programmer('Flavio')
flavio.hello()
```

(the above program prints "_Hello, I am Flavio. I am a programmer._")

Classes do not have explicit class variable declarations, but you must initialize any variable in the constructor.

Inside a class, you can reference the parent class calling `super()`.

## Static methods

Normally methods are defined on the instance, not on the class.

Static methods are executed on the class instead:

```js
class Person {
  static genericHello() {
    return 'Hello'
  }
}

Person.genericHello() //Hello
```

## Private methods

JavaScript does not have a built-in way to define private or protected methods.

There are workarounds, but I won't describe them here.

## Getters and setters

You can add methods prefixed with `get` or `set` to create a getter and setter, which are two different pieces of code that are executed based on what you are doing: accessing the variable, or modifying its value.

```js
class Person {
  constructor(name) {
    this._name = name
  }

  set name(value) {
    this._name = value
  }

  get name() {
    return this._name
  }
}
```

If you only have a getter, the property cannot be set, and any attempt at doing so (outside of the constructor, which sets the value when you initialize a new object with this class) will be ignored:

```js
class Person {
  constructor(name) {
    this._name = name
  }

  get name() {
    return this._name
  }
}
```

If you only have a setter, you can change the value but not access it from the outside:

```js
class Person {
  constructor(name) {
    this._name = name
  }

  set name(value) {
    this._name = value
  }
}
```

Getters and setters are very useful when you want to execute some code upon changing the property value, or if you want to create a "computed" property. You can alter the values you return by using a getter.

You can also run some code, like logging to the console or to a file when a value is changed.
