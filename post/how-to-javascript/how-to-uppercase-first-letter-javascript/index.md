---
title: "How to uppercase the first letter of a string in JavaScript"
date: 2018-05-09T07:06:15+02:00
updated: 2019-05-27T07:06:15+02:00
description: "JavaScript offers many ways to capitalize a string to make the first character uppercase. Learn the various ways, and also find out which one you should use, using plain JavaScript"
tags: js
---

One of the most common operations with strings is to make the string capitalized: uppercase its first letter, and leave the rest of the string as-is.

<div class="rwd-video">
<iframe width="560" height="315" src="https://www.youtube.com/embed/-pGqssugw6c" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
<br>

The best way to do this is through a combination of two functions. One uppercases the first letter, and the second slices the string and returns it starting from the second character:

```js
const name = 'flavio'
const nameCapitalized = name.charAt(0).toUpperCase() + name.slice(1)
```

You can extract that to a function, which also checks if the passed parameter is a string, and returns an empty string if not:

```js
const capitalize = (s) => {
  if (typeof s !== 'string') return ''
  return s.charAt(0).toUpperCase() + s.slice(1)
}

capitalize('flavio') //'Flavio'
capitalize('f')      //'F'
capitalize(0)        //''
capitalize({})       //''
```

Instead of using `s.charAt(0)` you could also use string indexing (not supported in older IE versions): `s[0]`.

Some solutions online advocate for adding the function to the String prototype:

```js
String.prototype.capitalize = function() {
  return this.charAt(0).toUpperCase() + this.slice(1)
}
```

(we use a regular function to make use of `this` - [arrow functions](/javascript-arrow-functions/) would fail in this case, as `this` in arrow functions does not reference the current object)

This solution is not ideal, because editing the prototype is not generally recommended, and it's a much slower solution than having an independent function.

---

Don't forget that if you just want to capitalize for presentational purposes on a Web Page, CSS might be a better solution, just add a `capitalize` class to your HTML paragraph and use:

```css
p.capitalize {
  text-transform: capitalize;
}
```

