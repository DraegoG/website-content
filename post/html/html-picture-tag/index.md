---
title: "The HTML `picture` tag"
seotitle: "How to use the HTML picture tag"
date: 2019-08-15T07:00:00+02:00
description: "Discover the basics of working with images and the HTML `picture` tag, and how to make them responsive"
tags: html
---

HTML gives us the `picture` tag, which does a very similar job of the `srcset` attribute of an `img` tag, and the differences are very subtle.

You use `picture` when instead of just serving a smaller version of a file, you completely want to change it. Or serve a different image format.

The best use case I found is when serving a WebP image, which is a format still not widely supported. In the `picture` tag you specify a list of images, and they will be used in order, so in the next example, browsers that support WebP will use the first image, and fallback to JPG if not:

```html
<picture>
  <source type="image/webp" srcset="image.webp">
  <img src="image.jpg" alt="An image">
</picture>
```

> The `source` tag defines one (or more) formats for the images. The `img` tag is the fallback in case the browser is very old and does not support the `picture` tag.

In the `source` tag inside `picture` you can add a `media` attribute to set media queries.

The example that follows kind of works like the above example with `srcset`:

```html
<picture>
  <source media="(min-width: 500w)" srcset="dog-500.png" sizes="100vw">
  <source media="(min-width: 800w)" srcset="dog-800.png" sizes="100vw">
  <source media="(min-width: 1000w)" srcset="dog-1000.png"	sizes="800px">
  <source media="(min-width: 1400w)" srcset="dog-1400.png"	sizes="800px">
  <img src="dog.png" alt="A dog image">
</picture>
```

But that's not its use case, because as you can see it's much more verbose.

The `picture` tag is recent but is now [supported](https://caniuse.com/#search=picture) by all the major browsers except Opera Mini and IE (all versions).
