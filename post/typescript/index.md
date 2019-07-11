---
title: The TypeScript Guide
date: 2019-01-11T07:00:00+02:00
description: TypeScript is one of the fastest rising technologies of 2018. It's everywhere, everyone talks about it. This article guides you towards understanding its key concepts
tags: js
---

Few technologies in the last few years had the impact that TypeScript had.

Let me add a little bit of social proof in favor of TypeScript.

The "The State of JavaScript 2018" survey, almost 50% of respondents said they used TypeScript, and would use it again. over 30% said they would like to learn it. That's a huge percentage of people interested in it.

TypeScript is built by Microsoft, which is not new to creating programming languages, and one of its creators is Anders Hejlsberg, a danish software engineer who is known for Turbo Pascal (❤️) and Delphi. I put the heart next to Turbo Pascal because Pascal was my first programming language and we used Turbo Pascal at school.

It's an open source language, developed in public at <https://github.com/Microsoft/TypeScript>.

Angular is all about TypeScript, Vue.js is said to make version 3 using TypeScript. Ryan Dahl, the creator of Node.js, said great things about it too.

I think those things help you put TypeScript in perspective. It's not just a random JavaScript flavor that will die next month, it's definitely here to stay. And as things go, this means you are likely required to use it in a future project, or at your next job. Maybe it will help you get a job too, so let's just dive into it.

## Write and compile your first TypeScript file

Starting with TypeScript is easy. If you ever wrote a line of JavaScript, you already wrote TypeScript code!

This odd statement I made is one of the reasons for TypeScript's success: it's a strict **superset of JavaScript**.

It's a bit like what SCSS is for CSS.

In particular, it's a superset of [ECMAScript 2015](/es6/) (also known as ES6). This means that any valid JavaScript is also valid TypeScript.

Many of the features of TypeScript are equivalent to the JavaScript ones. For example variables, the module system, iterators and more.

So, there's no need to write your absolute _first_ TypeScript file, because you already did without knowing so, but let's make a little "hello world!" by explicitly making a TypeScript file, and compile that to JavaScript.

Run `npm install -g typescript` to globally install the TypeScript compiler, available to you using the `tsc` command.

Make a new folder, and create an `app.ts` file. `ts` is the TypeScript file extension.

Write this first program:

```js
const greet = () => {
  console.log('Hello world!')
}

greet()
```

This is just plain JavaScript, but stored in a `.ts` file.

Now compile the program using `tsc app.ts`. The result will be a new JavaScript file: `app.js`, with this content:

```js
var greet = function () {
    console.log('Hello world!');
};
greet();
```

The TypeScript code has been **compiled** to JavaScript. The JavaScript code changed a little bit, for example you can notice it added semicolons, and used `var` instead of `const`, and used a regular function instead of the arrow function.

It looks like *old* JavaScript, right? This is because TypeScript compiles to ES5 by default, as this is the ECMAScript version that is almost guaranteed to be supported in all modern browsers. You can change the compilation target to other versions,for example to target ES2018 use `tsc app.ts --target ES2018`:

```js
const greet = () => {
    console.log('Hello world!');
};
greet();
```

See, here almost nothing changed from our original `.ts` file except for the additional semicolons.

There is a very convenient online playground that lets you play around with the TypeScript to JavaScript compilation, at <https://www.typescriptlang.org/play/>.

## Typing

Typing is the key TypeScript feature.

So far we compiled a `.ts` file, but we just compiled plain JavaScript.

You saw one first feature of TypeScript: you can use modern JavaScript and compile it to ES5 (or higher), kind of what [Babel](/babel/) does.

We didn't use any of the TypeScript functionalities.

The most important piece of functionality provided by TypeScript is the type system: static types, interfaces, type inference, enums, hybrid types, generics, union/intersection types, access modifiers, null checking.

If you ever used a typed language, like Go or C, you already know how this works. If not, and you only programmed in a dynamic language like Python or Ruby, this is all new to you but don't worry.

The type system allows you, for example, to add types to your variables, function arguments and function return types, giving a more rigid structure to your programs.

The advantages are better tooling: the compiler (and editors like editors like [VS Code](/vscode/)) can help you a lot during development, pointing out bugs as you write the code. Bugs that couldn't possibly be detected if you didn't have types. Also, teamwork gets easier because the code is more explicit.

The resulting JavaScript code that we compile to does not have types, of course: they are lost during the compilation phase, but the compiler will point out any error it finds.

Here is how you define a string variable in TypeScript:

```ts
const greeting : string = "hello!"
```

Type inference lets us avoid writing the type in obvious cases like this:

```ts
const greeting = "hello!"
```

The type is determined by TS.

This is how a function accepts an argument of a specific type:

```ts
const multiply = (a: number, b: number) => {
  return a * b
}
```

If you pass a string to `multiply()`, the compiler will give you an error.

Here is how functions declare their return value:

```ts
const multiply = (a: number, b: number): number => {
  return a * b
}
```

Valid types are

- `number`
- `string`
- `boolean`
- `enum`
- `void`
- `null`
- `undefined`
- `any`
- `never`
- `Array`
- `tuple`

`any` is a catch-all type that identifies, as its name says, any type.

## Classes

[ES2015/ES6](/es6/) added [classes](/javascript-classes/) to JavaScript, as a simple syntactic sugar over the [prototypal inheritance](/javascript-prototypal-inheritance/).

Like it or not, under the hoods JavaScript is still using prototypal inheritance, with all its unique features and quirks.

TypeScript classes are a little bit different than JavaScript classes. The reason is that TypeScript introduced classes before JavaScript had them (they were introduced in ES2015/ES6).

Like in JavaScript, you declare classes in this way:

```ts
class Car {

}
```

This is how you define class fields:

```ts
class Car {
  color: string
}
```

All fields are **public** by default. You can set a field to be **private** or **protected**:

```ts
class Car {
  public color: string
  private name: string
  protected brand: string
}
```

Like it happens in other programming languages, private fields can only be accessed in the class that declares them. Protected fields can only be accessed by deriving classes as well.

You can also declare static fields, which are class fields rather than object fields:

```ts
class Car {
  static numberOfWheels = 4
}
```

You can initialize fields with a constructor:

```ts
class Car {
  color: string
  constructor(theColor: string) {
    this.color = theColor
  }
}
```

This shorthand syntax makes it simpler:

```ts
class Car {
  constructor(public color: string) {}

  printColor() {
    alert(this.color)
  }
}

(new Car('red')).printColor()
```

Notice how we referenced the class field using `this.x`.

A field can also be **read only**:

```ts
class Car {
  readonly color: string
}
```

and in this case its value can only be set in the constructor.

Classes have methods:

```ts
class Car {
  color: string
  constructor(public color: string) {
    this.color = color
  }
  drive() {
    console.log('You are driving the car')
  }
}
```

Like in plain JavaScript, you create objects from those classes, using the `new` keyword:

```ts
const myCar = new Car('red')
```

and you can extend an existing class using the `extend` keyword:

```ts
class ElectricCar extends Car {
  //...
}
```

You can call `super()` in the constructor and in methods to call the extended class corresponding method.

## Accessors

Fields can have getters and setters. Example:

```ts
class Car {
  private _color: string

  get color(): string {
    return this._color
  }

  set color(color: string) {
    this._color = color
  }
}
```

## Abstract classes

Classes can be defined as abstract, which means there needs to be a class that extends it, and implements its eventual abstract methods:

```ts
abstract class Car {
  abstract drive()
}

class SportsCar extends Car {
  drive() {
    console.log('You are driving a sports car')
  }
}
```

## Interfaces

Interfaces build upon basic types. You can use an interface as a type, and this interface can contain other type definitions:

```ts
interface SetOfNumbers {
  a: number;
  b: number;
}

const multiply = (set: SetOfNumbers) => {
  return set.a * set.b
}

multiply({ a:1, b: 2 })
```

An interface can also be an interface for a class implementation:

```ts
interface Car {
  name: 'string'
  new (brand: string)
  drive(): void
}

class SportsCar implements Car {
  public name
  construtor(public brand: string) {
    //...
  }
  drive() {
    console.log('You are driving a sports car')
  }
}
```

## Functions features

Functions can have optional parameters using the `?` symbol after the parameter name:

```ts
class Car {
  drive(kilometers?: number) {
    if (kilometers) {
      console.log(`Drive the car for ${kilometers} kilometers`)
    } else {
      console.log(`Drive the car`)
    }
  }
}
```

and parameters can also have default values:

```ts
class Car {
  drive(kilometers = 10) {
    console.log(`Drive the car for ${kilometers} kilometers`)
  }
}
```

A function can accept a varying number of parameters by using rest parameters:

```ts
class Car {
  drive(kilometers = 10, ...occupants: string[]) {
    console.log(`Drive the car for ${kilometers} kilometers, with those people on it:`)
    occupants.map((person) => console.log(person))
  }
}
(new Car()).drive(20, 'Flavio', 'Roger', 'Syd')
```

## Enums

Enums are one great way to define named constants, which is unfortunately not supported by JavaScript, but popularized by other languages.

TypeScript gives us enums:

```ts
enum Order {
  First,
  Second,
  Third,
  Fourth
}
```

TS internally assigns an unique identifier to each of those values, and we can reference `Order.First`, `Order.Second` and so on.

You can assign values to the constants explicitly:

```ts
enum Order {
  First = 0,
  Second = 1,
  Third = 2,
  Fourth = 3
}
```

or also use strings:

```ts
enum Order {
  First = 'FIRST',
  Second = 'SECOND',
  Third = 'THIRD',
  Fourth = 'FOURTH'
}
```

## Generics

Generics is a feature that's part of many different programming languages. In short, you can create a function, interface or class that works with different types, without specifying the type up front.

But at compile time, if you start using that function with a type and then you change type (e.g. from number to string), the compiler will throw an error.

We could do this by omitting types at all or using `any`, but with generics all the tooling is going to be able to help us.

Example syntax:

```ts
function greet<T>(a : T) {
  console.log(`Hi ${a}!`)
}
greet('Flavio')
```

The funny `T` symbol identifies a generic type.

The type can be restricted to a certain class family or interface, using the `extends` keyword:

```ts
interface Greetable { name: string }
function greet<T extends Greetable>(a : T) {
  alert(`Hi ${a.name}!`)
}
greet({ name: 'Flavio'})
```

## I am ready for more!

Those are the basics of TypeScript. Go ahead to the [official docs](https://www.typescriptlang.org/docs) to learn all the details, or start writing your apps and learn as you do!