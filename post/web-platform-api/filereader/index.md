---
title: "The FileReader Object"
date: 2019-05-07T07:00:00+02:00
description: "Find out what is a FileReader object and how to use it"
tags: browser
---

The `FileReader` object asynchronously reads the content of a file.

It exposes those 4 reading methods we can use to start a reading process:

- `readAsText()`
- `readAsDataURL()`
- `readAsArrayBuffer()`
- `readAsBinaryString()`

and an `abort()` method to halt any reading operation.

Reading the file is asynchronous, and the object exposes several events we can hook into to follow the progress of the operation:

- `onload` triggered when the reading successfully ends
- `onloadstart` triggered when the reading starts
- `onprogress` triggered when the reading is on progress
- `onloadend` triggered when the reading ends, successfully or not successfully
- `onerror` triggered when an error occurs
- `onabort` triggered when the reading is aborted

Once a reading operation is completed, the `result` property of FileReader contains the file content.

The `error` property contains the error message, if an error occurred, and `readyState` contains the state of the operations - `0` if no data is loaded, `1` if data loading is in progress, and `2` if the loading has finished.

## `readAsText()`

Loads the content of a [blob](/blob/) in a text string.

In this example we use that text and put it into the `#content` element's inner HTML:

```js
//..file is available as a blob

const reader = new FileReader()

reader.onload = event => {
	const text = reader.result
  document.getElementById('content').innerHTML = text
}

reader.onerror = (e) => {
  console.error(e)
}

reader.readAsText(file)
```

Here's an example that reads the content of a text file when it's uploaded using an `input` element, and prints its content to the console:

```html
<input type="file" allow="text/*" />
```

```js
const input = document.querySelector('input')

input.addEventListener('change', e => {
	const reader = new FileReader()

	reader.onload = event => {
	  const text = reader.result
	  console.log(text)
	}

	reader.onerror = (e) => {
	  console.error(e)
	}

	reader.readAsText(input.files[0])
})
```

## `readAsDataURL()`

Loads the content of a blob into a **Data URL**.

```js
//..file is available as a blob

const reader = new FileReader()

reader.onload = event => {
	const dataURL = event.target.result
  document.getElementById('image').src = dataURL
}

reader.readAsDataURL(file)
```


## `readAsArrayBuffer()`

Loads the content of a blob into an [`ArrayBuffer`](/arraybuffer/).

```js
//..file is available as a blob

const reader = new FileReader()

reader.onload = event => {
	const buffer = reader.result
	const data = new Int32Array(buffer)
	//...
}

reader.onerror = (e) => {
  console.error(e)
}

reader.readAsArrayBuffer(file)
```

