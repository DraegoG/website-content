---
title: CSS Colors
date: 2019-05-02T07:00:00+02:00
description: "Learn how to work with colors in CSS"
tags: css
---

By default an HTML page is rendered by web browsers quite sadly in terms of the colors used.

We have a white background, black color, and blue links. That's it.

Luckily CSS gives us the ability to add colors to our designs.

We have these properties:

- `color`
- `background-color`
- `border-color`

All of them accept a **color value**, which can be in different forms.

## Named colors

First, we have CSS keywords that define colors. CSS started with 16, but today there is a huge number of colors names:

- `aliceblue`
- `antiquewhite`
- `aqua`
- `aquamarine`
- `azure`
- `beige`
- `bisque`
- `black`
- `blanchedalmond`
- `blue`
- `blueviolet`
- `brown`
- `burlywood`
- `cadetblue`
- `chartreuse`
- `chocolate`
- `coral`
- `cornflowerblue`
- `cornsilk`
- `crimson`
- `cyan`
- `darkblue`
- `darkcyan`
- `darkgoldenrod`
- `darkgray`
- `darkgreen`
- `darkgrey`
- `darkkhaki`
- `darkmagenta`
- `darkolivegreen`
- `darkorange`
- `darkorchid`
- `darkred`
- `darksalmon`
- `darkseagreen`
- `darkslateblue`
- `darkslategray`
- `darkslategrey`
- `darkturquoise`
- `darkviolet`
- `deeppink`
- `deepskyblue`
- `dimgray`
- `dimgrey`
- `dodgerblue`
- `firebrick`
- `floralwhite`
- `forestgreen`
- `fuchsia`
- `gainsboro`
- `ghostwhite`
- `gold`
- `goldenrod`
- `gray`
- `green`
- `greenyellow`
- `grey`
- `honeydew`
- `hotpink`
- `indianred`
- `indigo`
- `ivory`
- `khaki`
- `lavender`
- `lavenderblush`
- `lawngreen`
- `lemonchiffon`
- `lightblue`
- `lightcoral`
- `lightcyan`
- `lightgoldenrodyellow`
- `lightgray`
- `lightgreen`
- `lightgrey`
- `lightpink`
- `lightsalmon`
- `lightseagreen`
- `lightskyblue`
- `lightslategray`
- `lightslategrey`
- `lightsteelblue`
- `lightyellow`
- `lime`
- `limegreen`
- `linen`
- `magenta`
- `maroon`
- `mediumaquamarine`
- `mediumblue`
- `mediumorchid`
- `mediumpurple`
- `mediumseagreen`
- `mediumslateblue`
- `mediumspringgreen`
- `mediumturquoise`
- `mediumvioletred`
- `midnightblue`
- `mintcream`
- `mistyrose`
- `moccasin`
- `navajowhite`
- `navy`
- `oldlace`
- `olive`
- `olivedrab`
- `orange`
- `orangered`
- `orchid`
- `palegoldenrod`
- `palegreen`
- `paleturquoise`
- `palevioletred`
- `papayawhip`
- `peachpuff`
- `peru`
- `pink`
- `plum`
- `powderblue`
- `purple`
- `rebeccapurple`
- `red`
- `rosybrown`
- `royalblue`
- `saddlebrown`
- `salmon`
- `sandybrown`
- `seagreen`
- `seashell`
- `sienna`
- `silver`
- `skyblue`
- `slateblue`
- `slategray`
- `slategrey`
- `snow`
- `springgreen`
- `steelblue`
- `tan`
- `teal`
- `thistle`
- `tomato`
- `turquoise`
- `violet`
- `wheat`
- `white`
- `whitesmoke`
- `yellow`
- `yellowgreen`

plus `tranparent`, and `currentColor` which points to the `color` property, for example useful to make the `border-color` inherit it.

They are defined in the [CSS Color Module, Level 4](https://www.w3.org/TR/css-color-4/). They are case insensitive.

Wikipedia has a [nice table](https://en.wikipedia.org/wiki/Web_colors) which lets you pick the perfect color by its name.

Named colors are not the only option.

## RGB and RGBa

You can use the `rgb()` function to calculate a color from its RGB notation, which sets the color based on its red-green-blue parts. From 0 to 255:

```css
p {
  color: rgb(255, 255, 255); /* white */
	background-color: rgb(0, 0, 0); /* black */
}
```

`rgba()` lets you add the alpha channel to enter a transparent part. That can be a number from 0 to 1:

```css
p {
	background-color: rgba(0, 0, 0, 0.5);
}
```

## Hexadecimal notation

Another option is to express the RGB parts of the colors in the hexadecimal notation, which is composed by 3 blocks.

Black, which is `rgb(0,0,0)` is expressed as `#000000` or `#000` (we can shortcut the 2 numbers to 1 if they are equal).

White, `rgb(255,255,255)` can be expressed as `#ffffff` or `#fff`.

The hexadecimal notation lets express a number from 0 to 255 in just 2 digits, since they can go from 0 to "15" (f).

We can add the alpha channel by adding 1 or 2 more digits at the end, for example `#00000033`. Not all browsers support the shortened notation, so use all 6 digits to express the RGB part.

## HSL and HSLa

This is a more recent addition to CSS.

HSL = Hue Saturation Lightness.

In this notation, black is `hsl(0, 0%, 0%)` and white is `hsl(0, 0%, 100%)`.

If you are more familiar with HSL than RGB because of your past knowledge, you can definitely use that.

You also have `hsla()` which adds the alpha channel to the mix, again a number from 0 to 1: `hsl(0, 0%, 0%, 0.5)`