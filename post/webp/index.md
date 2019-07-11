---
title: The WebP Image Format
date: 2018-04-03T07:04:59+02:00
updated: 2019-02-01T07:04:59+02:00
description: "WebP is an Open Source image format developed at Google, which promises to generate images smaller in size compared to JPG and PNG formats, while generating better looking images"
booktitle: "WebP"
tags: browser

---

<!-- TOC -->

- [Introduction](#introduction)
- [How much smaller?](#how-much-smaller)
- [Generating WebP images](#generating-webp-images)
- [Browsers support](#browsers-support)
- [How can you use WebP today?](#how-can-you-use-webp-today)

<!-- /TOC -->

## Introduction

WebP is an Open Source image format developed at Google, which promises to generate images smaller in size compared to JPG and PNG formats, while generating better looking images.

WebP supports **transparency**, like PNG and GIF images.

WebP supports **animations**, like GIF images

And, using WebP you can set the quality ratio of your images, so you decide if you want to get better quality or a smaller size (like it happens in JPG images).

So **WebP can do all GIF, JPG and PNG images can do**, in a single format, and generate **smaller images**. Sounds like a deal.

If you want to compare how images look in the various formats, [here's a great gallery by Google](https://developers.google.com/speed/webp/gallery).

WebP is not _new_, it's been around for several years now.

## How much smaller?

The premise of generating smaller images is very interesting, especially when you consider than most of a web page size is determined by the amount and size of the image assets the user should download.

Google published a [comparative study](https://developers.google.com/speed/webp/docs/c_study) on the results of 1 million images with this result:

_WebP achieves overall higher compression than either JPEG or JPEG 2000. Gains in file size minimization are particularly high for smaller images which are the most common ones found on the web._

You should experiment with the kind of images you intend to serve, and form your opinion based on that.

In my tests, lossless compression compared to PNG generates WebP images 50% smaller. PNG reaches that file sizes only when using lossy compression.

## Generating WebP images

All modern graphical and image editing tools let you export to `.webp` files.

Command-line tools also exist to convert images to WebP directly. Google [provides a set of tools](https://developers.google.com/speed/webp/download) for this.

`cwebp` is the main command line utility to convert any image to `.webp`, use it with

```bash
cwebp image.png -o image.webp
```

Check out all the options using `cwebp -longhelp`.

## Browsers support

WebP is currently supported by

- Chrome
- Opera
- Opera Mini
- UC Browser
- Samsung Internet

However, only Chrome for Desktop and Opera 19+ implement all the features of WebP, which are:

- lossy compression
- lossless compression
- transparency
- animation

Other browsers only implement a subset. Safari and IE do not support WebP at all, and there are no signs of WebP being implemented any time soon in those browsers.

But Firefox supports WebP since version 65 (Jan 2019) and Edge since version 18.

So if we can serve those users an optimized image, to speed up serving them and consume less bandwidth, it's great. But check if it actually reduces your images size.

Check with your JPG/PNG image optimization tooling results, and see if adding an additional layer of complexity introduced by WebP is useful or not.

## How can you use WebP today?

There are a few different ways to do so.

You can use a server-level mechanism that serves WebP images instead of JPG and PNG when the `HTTP_ACCEPT` request header contains `image/webp`.

The first is the most convenient, as completely transparent to you and to your web pages.

Another option is to use Modernizr and check the `Modernizr.webp` setting.

If you don't need to support Internet Explorer, a very convenient way is to use the `<picture>` tag, which is now [supported](https://caniuse.com/#search=picture) by all the major browsers except Opera Mini and IE (all versions).

The `<picture>` tag is generally used for responsive images, but we can use it for WebP too, as [this tutorial from HTML5 Rocks](https://www.html5rocks.com/en/tutorials/responsive/picture-element/#toc-file-type) explains.

You can specify a list of images, and they will be used in order, so in the next example, browsers that support WebP will use the first image, and fallback to JPG if not:

```html
<picture>
  <source type="image/webp" srcset="image.webp">
  <img src="image.jpg" alt="An image">
</picture>
```
