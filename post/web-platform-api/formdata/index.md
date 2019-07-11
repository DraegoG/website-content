---
title: "The FormData Object"
date: 2019-07-13T07:00:00+02:00
description: "Find out what is a FormData object and how to use it"
tags: browser
---

The `FormData` object is used to hold form values in a key-value pairs data structure.

You create an empty `FormData` object in this way:

```js
const fd = new FormData()
```

Once you have the item you can call one of its methods:

- `append()` to add a value to the object, with the specified key. If the key already exists, the value is added to that key, without eliminating the first one
- `delete()` deletes a key value pair
- `entries()` gives an Iterator object you can loop to list the key value pairs hosted
- `get()` get the value associated with a key. If more than one value was appended, it returns the first one
- `getAll()` get all the values associated with a key
- `has()` returns true if there's a key
- `keys()` gives an Iterator object you can loop to list the keys hosted
- `set()` to add a value to the object, with the specified key. If the key already exists, the value is replaced
- `values()` gives an Iterator object you can loop to list the values hosted

The FormData object is part of the [XMLHttpRequest 2](/xhr/) spec. It's available in [all the modern browsers](http://caniuse.com/#feat=xhr2) but keep in mind that IE versions prior to 10 do not support it.

Here is one example of using FormData to send the content of a file using an XHR connection:

```html
<input type="file" id="fileUpload" />
```

```js
const sendFile = file => {
  const uri = '/saveImage'
  const xhr = new XMLHttpRequest()
  const fd = new FormData()

  xhr.open('POST', uri, true)
  xhr.onreadystatechange = () => {
    if (xhr.readyState == 4 && xhr.status == 200) {
      const imageName = xhr.responseText
      //do what you want with the image name returned
      //e.g update the interface
    }
  }
  fd.append('myFile', file)
  xhr.send(fd)
}

const handleImageUpload = event => {
  const files = event.target.files
  sendFile(files[0])
}

$('#fileUpload').addListener('change', event => {
  handleImageUpload(event)
})
```

This snippet instead can be used to send multiple files:

```html
<input type="file" id="fileUpload" multiple />
```

```js
const sendFiles = files => {
  const uri = '/saveImage'
  const xhr = new XMLHttpRequest()
  const fd = new FormData()

  xhr.open('POST', uri, true)
  xhr.onreadystatechange = () => {
    if (xhr.readyState == 4 && xhr.status == 200) {
      const imageName = xhr.responseText
      //do what you want with the image name returned
      //e.g update the interface
    }
  }

  for (let i = 0; i < files.length; i++) {
    fd.append(files[i].name, files[i])
  }

  xhr.send(fd)
}

const handleImageUpload = event => {
  sendFiles(event.target.files)
}

$('#fileUpload').addListener('change', event => {
  handleImageUpload(event)
})
```
