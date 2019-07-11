---
title: CSS url()
date: 2019-05-04T07:00:00+02:00
description: "Learn how to work with the CSS url() function"
tags: css
---

When we talk about background images, `@import`, and more, we use the `url()` function to load a resource:

```css
div {
  background-image: url(test.png);
}
```

In this case I used a relative URL, which searches the file in the folder where the CSS file is defined.

I could go one level back

```css
div {
  background-image: url(../test.png);
}
```

or go into a folder

```css
div {
  background-image: url(subfolder/test.png);
}
```

Or I could load a file starting from the root of the domain where the CSS is hosted:

```css
div {
  background-image: url(/test.png);
}
```

Or I could use an absolute URL to load an external resource:

```css
div {
  background-image: url(https://mysite.com/test.png);
}
```

