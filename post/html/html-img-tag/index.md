---
title: "The HTML `img` tag"
seotitle: "How to use the HTML img tag"
date: 2019-08-10T07:00:00+02:00
description: "Discover the basics of working with images and the HTML `img` tag, and how to make them responsive"
tags: html
---

Images can be displayed using the `img` tag.

This tag accepts a `src` attribute, which we use to set the image source:

```html
<img src="image.png" />
```

We can use a wide set of images. The most common ones are PNG, JPEG, GIF, SVG and more recently WebP.

The HTML standard requires an `alt` attribute to be present, to describe the image. This is used by screen readers and also by search engine bots:

```html
<img src="dog.png" alt="A picture of a dog" />
```

You can set the `width` and `height` attributes to set the space that the element will take, so that the browser can account for it and it does not change the layout when it's fully loaded. It takes a numeric value, expressed in pixels.

```html
<img src="dog.png" alt="A picture of a dog" width="300" height="200" />
```

## Responsive images using `srcset`

The `srcset` attribute allows you to set responsive images that the browser can use depending on the pixel density or window width, according to your preferences. In this way it can only download the resources it needs to render the page, without downloading a bigger image if it's on a mobile device, for example.

Here's an example, where we give 4 additional images for 4 different screen sizes:

```html
<img src="dog.png"
	alt="A picture of a dog"
	srcset="dog-500.png 500w,
	  		 dog-800.png 800w,
			 dog-1000.png 1000w,
			 dog-1400.png 1400w">
```

In the `srcset` we use the `w` measure to indicate the window width.

Since we do so, we also need to use the `sizes` attribute:

```html
<img src="dog.png"
	alt="A picture of a dog"
	sizes="(max-width: 500px) 100vw, (max-width: 900px) 50vw, 800px"
	srcset="dog-500.png 500w,
	  		 dog-800.png 800w,
			 dog-1000.png 1000w,
			 dog-1400.png 1400w">
```

In this example the `(max-width: 500px) 100vw, (max-width: 900px) 50vw, 800px` string in the `sizes` attribute describes the size of the image in relation to the viewport, with multiple conditions separated by a semicolon.

The media condition `max-width: 500px ` sets the size of the image in correlation to the  viewport width. In short, if the window size is < 500px, it renders the image at 100% of the window size.

If the window size is bigger but < `900px`, it renders the image at 50% of the window size.

And if even bigger, it renders the image at 800px.

The `vw` unit of measure can be new to you, and in short we can say that 1 `vw` is 1% of the window width, so `100vw` is 100% of the window width.

A useful website to generate the `srcset` and progressively smaller images is [https://responsivebreakpoints.com/](https://responsivebreakpoints.com/).

