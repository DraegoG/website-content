---
title: CSS Cascade
date: 2019-04-25T07:00:00+02:00
description: "Learn what CSS Cascade means and why it's important"
tags: css
---

Cascade is a fundamental concept of CSS. After all, it's in the name itself, the first C of CSS - Cascading Style Sheets - it must be an important thing.

What does it mean?

**Cascade is the process, or algorithm, that determines the properties applied to each element on the page**.

Trying to converge from a list of CSS rules that are defined in various places.

It does so taking in consideration:

- [specificity](/css-specificity/)
- importance
- inheritance
- order in the file

It also takes care of resolving conflicts.

Two or more competing CSS rules for the same property applied to the same element need to be elaborated according to the CSS spec, to determine which one needs to be applied.

Even if you just have one CSS file loaded by your page, there is other CSS that is going to be part of the process. We have the browser (user agent) CSS. Browsers come with a default set of rules, all different between browsers.

Then your CSS come into play.

Then the browser applies any user stylesheet, which might also be applied by browser extensions.

All those rules come into play while rendering the page.
