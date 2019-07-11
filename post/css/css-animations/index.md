---
title: A CSS Animations Tutorial
date: 2018-04-26T07:07:09+02:00
description: "CSS Animations are a great way to create visual animations, not limited to a single movement like CSS Transitions, but much more articulated. An animation is applied to an element using the `animation` property"
booktitle: CSS Animations
medium: true
tags: css
---

<!-- TOC -->

- [Introduction](#introduction)
- [A CSS Animations Example](#a-css-animations-example)
- [The CSS animation properties](#the-css-animation-properties)
- [JavaScript events for CSS Animations](#javascript-events-for-css-animations)
- [Which Properties You Can Animate using CSS Animations](#which-properties-you-can-animate-using-css-animations)

<!-- /TOC -->

## Introduction

An animation is applied to an element using the `animation` property.

```css
.container {
	animation: spin 10s linear infinite;
}
```

`spin` is the name of the animation, which we need to define separately. We also tell CSS to make the animation last 10 seconds, perform it in a linear way (no acceleration or any difference in its speed) and to repeat it infinitely.

You must **define how your animation works** using **keyframes**. Example of an animation that rotates an item:

```css
@keyframes spin {
	0% {
		transform: rotateZ(0);
	}
	100% {
		transform: rotateZ(360deg);
	}
}
```

Inside the `@keyframes` definition you can have as many intermediate waypoints as you want.

In this case we instruct CSS to make the transform property to rotate the Z axis from 0 to 360 grades, completing the full loop.

You can use any CSS transform here.

Notice how this does not dictate anything about the temporal interval the animation should take. This is defined when you use it via `animation`.

## A CSS Animations Example

I want to draw four circles, all with a starting point in common, all 90 degrees distant from each other.

```html
<div class="container">
  <div class="circle one"></div>
  <div class="circle two"></div>
  <div class="circle three"></div>
  <div class="circle four"></div>
</div>
```

```css
body {
  display: grid;
  place-items: center;
  height: 100vh;
}

.circle {
	border-radius: 50%;
	left: calc(50% - 6.25em);
	top: calc(50% - 12.5em);
	transform-origin: 50% 12.5em;
	width: 12.5em;
	height: 12.5em;
	position: absolute;
	box-shadow: 0 1em 2em rgba(0, 0, 0, .5);
}

.one,
.three {
	background: rgba(142, 92, 205, .75);
}

.two,
.four {
	background: rgba(236, 252, 100, .75);
}


.one {
	transform: rotateZ(0);
}

.two {
	transform: rotateZ(90deg);
}

.three {
	transform: rotateZ(180deg);
}

.four {
	transform: rotateZ(-90deg);
}
```

You can see them in this Glitch: <https://flavio-css-circles.glitch.me>

<!-- Copy and Paste Me -->
<div class="glitch-embed-wrap" style="height: 520px; width: 100%;">
  <iframe src="https://glitch.com/embed/#!/embed/flavio-css-circles?path=style.css&previewSize=52&sidebarCollapsed=true" alt="flavio-css-circles on glitch" style="height: 100%; width: 100%; border: 0;"></iframe>
</div>

<br>

Let's make this structure (all the circles together) rotate. To do this, we apply an animation on the container, and we define that animation as a 360 degrees rotation:

```css
@keyframes spin {
	0% {
		transform: rotateZ(0);
	}
	100% {
		transform: rotateZ(360deg);
	}
}

.container {
	animation: spin 10s linear infinite;
}
```

See it on <https://flavio-css-animations-tutorial.glitch.me>

<!-- Copy and Paste Me -->
<div class="glitch-embed-wrap" style="height: 520px; width: 100%;">
  <iframe src="https://glitch.com/embed/#!/embed/flavio-css-animations-tutorial?path=style.css&previewSize=52&sidebarCollapsed=true" alt="flavio-css-animations-tutorial on glitch" style="height: 100%; width: 100%; border: 0;"></iframe>
</div>

<br>

You can add more keyframes to have funnier animations:

```css
@keyframes spin {
	0% {
		transform: rotateZ(0);
	}
	25% {
		transform: rotateZ(30deg);
	}
	50% {
		transform: rotateZ(270deg);
	}
	75% {
		transform: rotateZ(180deg);
	}
	100% {
		transform: rotateZ(360deg);
	}
}
```

See the example on <https://flavio-css-animations-four-steps.glitch.me>

<!-- Copy and Paste Me -->
<div class="glitch-embed-wrap" style="height: 520px; width: 100%;">
  <iframe src="https://glitch.com/embed/#!/embed/flavio-css-animations-four-steps?path=style.css&previewSize=57&sidebarCollapsed=true" alt="flavio-css-animations-four-steps on glitch" style="height: 100%; width: 100%; border: 0;"></iframe>
</div>
<br>

## The CSS animation properties

CSS animations offers a lot of different parameters you can tweak:

Property | Description
---------|------------
`animation-name` |  the name of the animation, it references an animation created using `@keyframes`
`animation-duration` | how long the animation should last, in seconds
`animation-timing-function` | the timing function used by the animation (common values: `linear`, `ease`). Default: `ease`
`animation-delay` | optional number of seconds to wait before starting the animation
`animation-iteration-count` | how many times the animation should be performed. Expects a number, or `infinite`. Default: 1
`animation-direction` | the direction of the animation. Can be `normal`, `reverse`, `alternate` or `alternate-reverse`. In the last 2, it alternates going forward and then backwards
`animation-fill-mode` | defines how to style the element when the animation ends, after it finishes its iteration count number. `none` or `backwards` go back to the first keyframe styles. `forwards` and `both` use the style that's set in the last keyframe
`animation-play-state` | if set to `paused`, it pauses the animation. Default is `running`

The `animation` property is a shorthand for all these properties, in this order:

```css
.container {
  animation: name
             duration
             timing-function
             delay
             iteration-count
             direction
             fill-mode
             play-state;
}
```

This is the example we used above:

```css
.container {
	animation: spin 10s linear infinite;
}
```

## JavaScript events for CSS Animations

Using JavaScript you can listen for the following events:

- `animationstart`
- `animationend`
- `animationiteration`

Be careful with `animationstart`, because if the animation starts on page load, your JavaScript code is always executed after the CSS has been processed, so the animation is already started and you cannot intercept the event.

```js
const container = document.querySelector('.container')
container.addEventListener('animationstart', (e) => {
	//do something
}, false)
container.addEventListener('animationend', (e) => {
	//do something
}, false)
container.addEventListener('animationiteration', (e) => {
	//do something
}, false)
```

## Which Properties You Can Animate using CSS Animations

A lot! They are the same you can animate using CSS Transitions, too.

Here's the full list:

| Property
|--------
|background
|background-color
|background-position
|background-size
|border
|border-color
|border-width
|border-bottom
|border-bottom-color
|border-bottom-left-radius
|border-bottom-right-radius
|border-bottom-width
|border-left
|border-left-color
|border-left-width
|border-radius
|border-right
|border-right-color
|border-right-width
|border-spacing
|border-top
|border-top-color
|border-top-left-radius
|border-top-right-radius
|border-top-width
|bottom
|box-shadow
|caret-color
|clip
|color
|column-count
|column-gap
|column-rule
|column-rule-color
|column-rule-width
|column-width
|columns
|content
|filter
|flex
|flex-basis
|flex-grow
|flex-shrink
|font
|font-size
|font-size-adjust
|font-stretch
|font-weight
|grid-area
|grid-auto-columns
|grid-auto-flow
|grid-auto-rows
|grid-column-end
|grid-column-gap
|grid-column-start
|grid-column
|grid-gap
|grid-row-end
|grid-row-gap
|grid-row-start
|grid-row
|grid-template-areas
|grid-template-columns
|grid-template-rows
|grid-template
|grid
|height
|left
|letter-spacing
|line-height
|margin
|margin-bottom
|margin-left
|margin-right
|margin-top
|max-height
|max-width
|min-height
|min-width
|opacity
|order
|outline
|outline-color
|outline-offset
|outline-width
|padding
|padding-bottom
|padding-left
|padding-right
|padding-top
|perspective
|perspective-origin
|quotes
|right
|tab-size
|text-decoration
|text-decoration-color
|text-indent
|text-shadow
|top
|transform.
|vertical-align
|visibility
|width
|word-spacing
|z-index