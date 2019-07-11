---
title: "Compare the options for Animations on the Web"
description: "Animation is a fascinating topic. Whether you want to add interaction animations like transitions, or building a whole full screen experience, you have all the tools you need"
date: 2018-04-24T07:06:29+02:00
booktitle: Animations
---

Animation is a fascinating topic. Whether you want to add interaction animations like transitions, or building a whole full screen experience, you have all the tools you need.

And you have quite a few choices, which are all completely different and serve different purposes.

[CSS](/css/) is commonly known to be more performant, although JavaScript can also be very performant. It all depends on what you need to do, and how much time it takes for each frame to render.

<!-- TOC -->

- [CSS Transitions](#css-transitions)
- [CSS Animations](#css-animations)
- [SVG Animations](#svg-animations)
- [Canvas API Animations](#canvas-api-animations)
- [The Web Animations API](#the-web-animations-api)
- [WebGL](#webgl)

<!-- /TOC -->

Let's see an overview of these options, to find out which one is the right choice.

## CSS Transitions

[CSS Transitions](/css-transitions/) have a start and and end. They move one point from X to Y, or from visible to invisible.

It's the simplest of the animations, and mostly used for subtle animations that integrate well with the rest of the page.

With transitions you go from one state to another, but you can't have much more.

## CSS Animations

[CSS Animations](/css-animations/) compared to CSS transitions allow you to have more than just 2 states, in fact you can have lots of them, and they can be used to create more complex animations.

CSS Animations are recommended when you need relatively simple animations which are not possible to do with transitions.

## SVG Animations

[SVG](/svg/) is a great vector-based format which allows to create animations using SMIL, the SVG animations "native" format.

SMIL was about to be deprecated in Chrome, but the team reversed this decision for the time being due to resistance, although SMIL has cross-browser inconsistencies (and IE/Edge do not support it).

They want to push CSS Animations and the Web Animations API instead of SMIL.

## Canvas API Animations

The [Canvas API](/canvas/) offers a way to paint on the screen, using rasters rather than vectors.

Animations are possible although not as performant

## The Web Animations API

The Web Animations API is the future of animations on the Web. It aims to bring the performance of CSS animations with the ability of using JavaScript to create longer animations easily.

It's currently only working in Chrome and Firefox. Safari, IE and Edge are still considering it, but [a polyfill exists](https://github.com/web-animations/web-animations-js/) to make it work across all browsers.

## WebGL

WebGL allows you to create 3D animations, and it's more suited for immersive, full-screen animations experiences and VR, although more complex.

---

In addition to the native APIs, there are great libraries that abstract most of the details for you:

- [Greensock](http://greensock.com/)
- [Three.js](https://threejs.org/)
- [React-Motion](https://github.com/chenglou/react-motion)
- [Velocity.js](http://velocityjs.org/)
