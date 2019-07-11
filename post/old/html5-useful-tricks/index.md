---
title: Some useful tricks available in HTML5
date: 2013-05-14T09:06:59+02:00
tags: browser
---

> Warning: this post is old and might not reflect the current state of the art

## Autofocus
`<input autofocus="autofocus" />` will put the focus on the specified HTML element when the page loads

## Downloading files
`<a href="file.pdf" download="pdf-file">Download</a>` will download the specified file, with the name provided.

## Hide elements
`<div hidden="hidden"></div>` despite putting the presentation in the HTML, which is bad, this can sometimes turn out useful.

## Turning off (or on) spellchecking
Operating systems configured to spell check everything a user types can sometimes get in the way - `<input type="text" spellcheck="true|false">` can help.

## Auto suggestion text input control

```html
  <input list="mylist" name="mylist" >
  <datalist id="mylist">
    <option value="CSS">
    <option value="HTML">
    <option value="PHP">
    <option value="Jquery">
    <option value="Wordpress">
  </datalist>
```
