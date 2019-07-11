---
title: The Lexical Structure of JavaScript
date: 2018-02-12T16:04:59+02:00
description: "A deep dive into the building blocks of JavaScript: unicode, semicolons, white space, case sensitivity, comments, literals, identifiers and reserved words"
booktitle: Lexical Structure
tags: js
tags_weight: 3
---

<!-- TOC -->

- [Unicode](#unicode)
- [Semicolons](#semicolons)
- [White space](#white-space)
- [Case sensitive](#case-sensitive)
- [Comments](#comments)
- [Literals and Identifiers](#literals-and-identifiers)
- [Reserved words](#reserved-words)

<!-- /TOC -->

## Unicode

[JavaScript](/javascript/) is written in [Unicode](/unicode/). This means you can use Emojis as variable names, but more importantly, you can write identifiers in any language, for example Japanese or Chinese, [with some rules](https://mathiasbynens.be/notes/javascript-identifiers).

## Semicolons

JavaScript has a very C-like syntax, and you might see lots of code samples that feature semicolons at the end of each line.

**Semicolons aren't mandatory**, and JavaScript does not have any problem in code that does not use them, and lately many developers, especially those coming from languages that do not have semicolons, started avoiding using them.

You just need to avoid doing strange things like typing statements on multiple lines

```js
return
variable
```

or starting a line with parentheses (`[` or `(`) and you'll be safe 99.9% of the times (and your linter will warn you).

It goes to personal preference, and lately I have decided to **never add useless semicolons**, so on this site you'll never see them.

## White space

JavaScript does not consider white space meaningful. Spaces and line breaks can be added in any fashion you might like, even though this is _in theory_.

In practice, you will most likely keep a well defined style and adhere to what people commonly use, and enforce this using a linter or a style tool such as _Prettier_.

For example I like to always 2 characters to indent.

## Case sensitive

JavaScript is case sensitive. A variable named `something` is different from `Something`.

The same goes for any identifier.

## Comments

You can use two kind of comments in JavaScript:

```
/* */

//
```

The first can span over multiple lines and needs to be closed.

The second comments everything that's on its right, on the current line.

## Literals and Identifiers

We define as **literal** a value that is written in the source code, for example a number, a string, a boolean or also more advanced constructs, like Object Literals or Array Literals:

```js
5
'Test'
true
['a', 'b']
{color: 'red', shape: 'Rectangle'}
```

An **identifier** is a sequence of characters that can be used to identify a variable, a function, an object. It can start with a letter, the dollar sign `$` or an underscore `_`, and it can contain digits. Using Unicode, a letter can be any allowed char, for example an emoji 😄.

```js
Test
test
TEST
_test
Test1
$test
```

The dollar sign is commonly used to reference [DOM](/dom/) elements.

## Reserved words

You can't use as identifiers any of the following words:

```js
break
do
instanceof
typeof
case
else
new
var
catch
finally
return
void
continue
for
switch
while
debugger
function
this
with
default
if
throw
delete
in
try
class
enum
extends
super
const
export
import
implements
let
private
public
interface
package
protected
static
yield
```

because they are reserved by the language.
