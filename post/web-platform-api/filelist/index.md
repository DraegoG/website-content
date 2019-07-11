---
title: "The FileList Object"
date: 2019-05-11T07:00:00+02:00
description: "Find out what is a FileList object and how to use it"
tags: browser
---

When you have an HTML Form with an `<input type="file" />` element, when one or more files are uploaded by the user you will interact with a `FileList` object.

That's not the only place that can give you a `FileList` object. You will get one also when interacting with Drag and Drop.

Sticking to forms, the input type by default does not allow multiple files to be uploaded.

You will retrieve a FileList with just one element, and you can retrieve it using this syntax:

```html
<input type="file" />
```

```js
const input = document.querySelector('input')

input.addEventListener('change', e => {
  const fileList = input.files
  const theFile = fileList[0]
})
```

Selecting any element from a `FileList` object will get a [`File`](/file/) object. In this case we just have one, so we select the item at position 0.

You can also retrieve it using the `item()` method, specifying the index:

```js
const input = document.querySelector('input')

input.addEventListener('change', e => {
  const fileList = input.files
  const theFile = fileList.item(0)
})
```

If multiple is enabled though, using the `multiple` attribute (`<input type="file" multiple />`), FileList will contain multiple elements.

You can get the count by looking at the `length` property of `FileList`.

This example loads the files uploaded and iterates on them to print each file's name:

```html
<input type="file" multiple />
```

```js
const input = document.querySelector('input')

input.addEventListener('change', e => {
  const files = input.files
  const filesCount = fileList.length

  for (let i = 0; i < files.length; i++) {
    const file = files[i]
    alert(file.name)
  }
})
```

