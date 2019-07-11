---
title: "How to continuously rotate an image using CSS"
date: 2019-01-13T07:00:00+02:00
description: "How to use CSS Animations to continuously rotate an image"
tags: css
---

While building the [React Handbook](https://reacthandbook.com) landing page, I had to search how to rotate an image. I wanted to rotate an [SVG](/svg/) image, but this works for any image type. Or any HTML element, actually.

Add this CSS instruction to the element you want to rotate:

```css
animation: rotation 2s infinite linear;
```

You can also choose to add a `rotate` class to an element, instead of targeting it directly:

```css
.rotate {
  animation: rotation 2s infinite linear;
}
```

tweak the `2s` to slow down of speed up the rotation period.

Then add this line, outside of any selector:

```css
@keyframes rotation {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(359deg);
  }
}
```

That's it! Your elements should now rotate.

> Check out the [CSS Animations](/css-animations/) and [CSS Transitions](/css-transitions/) guides

Here is the result shown in Codepen:

<p data-height="265" data-theme-id="0" data-slug-hash="zyyJpL" data-default-tab="css,result" data-user="flaviocopes" data-pen-title="How to use CSS Animations to continuously rotate an image" class="codepen">See the Pen <a href="https://codepen.io/flaviocopes/pen/zyyJpL/">How to use CSS Animations to continuously rotate an image</a> by Flavio Copes (<a href="https://codepen.io/flaviocopes">@flaviocopes</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>