---
title: How to upload files to the server using JavaScript
description: Uploading a file an process it in the backend in one of the most common file handling functionalities in a web app
date: 2013-10-25T09:07:30+02:00
updated: 2019-05-16T09:07:30+02:00
tags: js
---

Uploading a file an process it in the backend in one of the most common file handling functionalities in a web app: think about uploading an avatar or an attachment.

There are a lot of pre-built libraries that deal with this, but let's keep things simple by writing the smallest amount of code needed for this task. The solution here provided does not provide progress tracking, which can be implemented upon it.

We have an HTML input element with `type="file"`:

```html
<input type="file" id="fileUpload" />
```

This is the frontend code. We register a change handler on the `#fileUpload` [DOM](/dom/) element, and when the user chooses an image, we trigger the `sendFile()` function passing in the file selected.

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

`sendFile()` prepares the XHR (AJAX) request and sends the file to the server. When the server returns successfully, it will send us the image name. With that, we will do what we need to do, like updating the interface with the image.

## Handling the file upload server-side using Node.js

The server part is detailed here below. I'm using [Node.js](/nodejs/) with the Express framework to handle the request, and the fs module to save the file to disk, in a directory `/files/` relative to the path where the source file lives.

```js
const fs = require('fs')

app.post('/saveImage', (req, res) => {
  const fileName = req.files.myFile.name
  fs.readFile(req.files.myFile.path, (err, data) => {
    const newPath = __dirname + '/images/' + fileName
    fs.writeFile(newPath, data, error => {
      if (error) {
        console.error(error)
        res.end()
      } else {
        res.end(fileName)
        //here you can save the file name to db, if needed
      }
    })
  })
})
```

This is the smallest amount of code needed to handle files.

## Check the properties of the files uploaded client-side

If you need to check the filetype or the file size, you can preprocess them in the `handleImageUpload` function, like this:

```js
const handleImageUpload = event => {
  const files = event.target.files
  const myImage = files[0]
  const imageType = /image.*/

  if (!myImage.type.match(imageType)) {
    alert('Sorry, only images are allowed')
    return
  }

  if (myImage.size > (100*1024)) {
    alert('Sorry, the max allowed size for images is 100KB')
    return
  }

  //...
}
```
