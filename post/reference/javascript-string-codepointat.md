---
title: "The String codePointAt() method"
description: "Find out all about the JavaScript codePointAt() method of a string"
date: 2019-02-16T07:00:00+02:00
tags: js
---

This was introduced in ES2015 to handle Unicode characters that cannot be represented by a single 16-bit Unicode unit, but need 2 instead.

Using `charCodeAt()` you need to retrieve the first, and the second, and combine them. Using `codePointAt()` you get the whole character in one call.

For example, this chinese character "𠮷" is composed by 2 UTF-16 (Unicode) parts:

```js
"𠮷".charCodeAt(0).toString(16) //d842
"𠮷".charCodeAt(1).toString(16) //dfb7
```

If you create a new character by combining those unicode characters:

```js
"\ud842\udfb7" //"𠮷"
```

You can get the same result usign `codePointAt()`:

```js
"𠮷".codePointAt(0) //20bb7
```

If you create a new character by combining those unicode characters:

```js
"\u{20bb7}" //"𠮷"
```

More on Unicode and working with it in [Unicode and UTF-8](/javascript-unicode/).
