---
title: "CSS System Fonts"
description: "How to use System Fonts in CSS to improve your site and provide a better experience to your users in terms of speed and page load time"
date: 2018-03-27T08:06:29+02:00
tags: css
---

<!-- TOC -->

- [A little bit of history](#a-little-bit-of-history)
- [Today](#today)
- [The impact of Web Fonts](#the-impact-of-web-fonts)
- [Enter System Fonts](#enter-system-fonts)
- [Popular websites use System Fonts](#popular-websites-use-system-fonts)
- [I'm sold. Give me the code](#im-sold-give-me-the-code)
  - [A note on `system-ui`](#a-note-on-system-ui)
- [Use font variations by creating @font-face rules](#use-font-variations-by-creating-font-face-rules)
- [Read more](#read-more)

<!-- /TOC -->

## A little bit of history

For _years_, websites could only use fonts available on all computers, such as Georgia, Verdana, Arial, Helvetica, Times New Roman. Other fonts were not guaranteed to work on all websites.

If you wanted to use a fancy font you had to use images.

In 2008 Safari and Firefox introduced the `@font-face` CSS property, and online services started to provide licenses to Web Fonts. The first was Typekit in 2009, and later Google Fonts got hugely popular thanks to its free offering.

`@font-face` was implemented in all the major browsers, and nowadays it's a given on every reasonably recent device. If you're a young web developer you might not realize it, but in 2012 we still had articles explaining this new technology of Web Fonts.

## Today

You _can_ use whatever font you wish to use, by relying on a service like Google Fonts, or providing your own font to download.

You _can_, but **should you**?

If you have the choice (and by this I mean, you're not implementing a design that a client gave you), you might want to think about it, in a move to go back to the basics (but in style!)

## The impact of Web Fonts

Everything you load on your pages has a **cost**. This cost is especially impactful on mobile, where every byte you require is impacting the load time, and the amount of bandwidth you make your users consume.

The font must load before the content renders, so you need to **wait** for that resource loading to complete before the user is able to read even a single word you wrote.

But Web Fonts are a way to provide an **awesome user experience** through good typography.

## Enter System Fonts

Operating Systems have great default fonts.

System Fonts offer the great advantage of **speed** and **performance**, and a **reduction of your web page size**.

But as a side effect, they make your website look **very familiar** to anyone looking at it, because they are used to see that same font every day on their computer or mobile device.

It's effectively a **native font**.

And as it's the system font, it's **guaranteed to look great**.

## Popular websites use System Fonts

You might know one of these, as an example:

- GitHub
- Medium
- Ghost
- Bootstrap
- Booking.com

..they have been using System Fonts for years.

Even the Wordpress dashboard - that runs millions of websites - uses system fonts, and Medium, which is all about reading, decided to use system fonts.

If it works for them, chances are it works for you as well.

## I'm sold. Give me the code

This is the CSS line you should add to your website:

```css
body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI",
  "Roboto", "Oxygen", "Ubuntu", "Helvetica Neue", Arial, sans-serif;
}
```

The browser will interpret all these font names, and starting from the first it will check if it's available.

Safari and Firefox on macOS "intercept" `-apple-system`, which means the San Francisco font on newer versions, Helvetica Neue and Lucida Grande on older versions.

Chrome works with BlinkMacSystemFont, which defaults to the OS font (again, San Francisco on macOS).

Segoe UI is used in modern Windows systems and Windows Phone, Tahoma in Windows XP, Roboto in Android, and so on targeting other platforms.

Arial and sans-serif are the fallback fonts.

If you use **Emojis** in your site, make sure you load the symbol fonts as well:

```css
body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "Roboto",
  "Oxygen", "Ubuntu", "Helvetica Neue", Arial, sans-serif, "Apple Color Emoji",
  "Segoe UI Emoji", "Segoe UI Symbol";
}
```

You might want to change the order of the font appearance based on your website usage statistics.

### A note on `system-ui`

Maybe you will see `system-ui` mentioned in System Fonts posts online, but at the moment it's known to cause issues in Windows (see <https://infinnie.github.io/blog/2017/systemui.html> and <https://github.com/twbs/bootstrap/pull/22377>)

There is work being done towards standardizing system-ui as a generic font family, so in the future you will just write

```css
body {
  font-family: system-ui;
}
```

See <https://www.chromestatus.com/feature/5640395337760768> and <https://caniuse.com/#feat=font-family-system-ui> to keep an eye on the progress. Chrome, Safari already support it, Firefox partially, while Edge does not yet implement it.

## Use font variations by creating @font-face rules

The approach described above works _great_ until you need to alter the font on a second element, and maybe even on more than one.

Maybe you want to specify the italic as a `font` property rather than in `font-style`, or set a specific font weight.

This nice project by Jonathan Neal <https://jonathantneal.github.io/system-font-css/> lets you use System Fonts by importing a module, and you can set

```css
body {
  font-family: system-ui;
}
```

This `system-ui` is defined in <https://github.com/jonathantneal/system-font-css/blob/gh-pages/system-font.css>.

You are now able to use different font variations by referencing:

```css
.special-text {
  font: italic 300 system-ui;
}

p {
  font: 400 system-ui;
}
```

## Read more

- <https://css-tricks.com/snippets/css/system-font-stack/>
- <https://www.smashingmagazine.com/2015/11/using-system-ui-fonts-practical-guide/>
- <https://medium.design/system-shock-6b1dc6d6596f>