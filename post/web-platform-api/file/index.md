---
title: "The File Object"
date: 2019-05-06T07:00:00+02:00
updated: 2019-05-10T07:00:00+02:00
description: "Find out what is a File object and how to use it"
tags: browser
---

Browsers provide us a `File` object.

The File object is a [**Blob**](/blob/) object, and it provides 3 properties on top of it:

- `name` (a [String](/javascript-string/))
- `lastModified` (the [UNIX timestamp](/how-to-get-timestamp-javascript/) of the last modified date time)

which adds up to the `Blob` object properties:

- `size` (the size in bytes)
- `type` (the MIME type)

You will receive a `File` object when interacting with the `FileList` object, which can be retrieved from an HTML Form with an `<input type="file" />` element, or when interacting with **Drag and Drop**.

When you got a `FileList` object, when you loop over it or you pick an element (for example the first item with `myFileList[0]`) you will get a `File` object.

Say you have an `input type="file"` element in your form:

```js
<input type="file" />
```

Now you can listen for the `change` event on this element, so when you choose a file you'll get information about it. `document.querySelector('input').files` will return a `FileList` object, like explained above, and using `[0]` we get the first file loaded, and we can access all the properties we need from the `File` object:

```js
document.querySelector('input').addEventListener('change', () => {
  const file = document.querySelector('input').files[0]
  alert(`The file ${file.name} was last modified on ${new Date(file.lastModified).toDateString()}`)
})
```

<p class="codepen" data-height="265" data-theme-id="0" data-default-tab="js,result" data-user="flaviocopes" data-slug-hash="EzxdMm" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="File object demo">
  <span>See the Pen <a href="https://codepen.io/flaviocopes/pen/EzxdMm/">
  File object demo</a> by Flavio Copes (<a href="https://codepen.io/flaviocopes">@flaviocopes</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>
