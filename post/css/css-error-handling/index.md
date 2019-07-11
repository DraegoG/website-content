---
title: CSS Error Handling
date: 2019-06-13T07:00:00+02:00
description: "How CSS handles errors"
tags: css
---

CSS is resilient. When it finds an error, it does not act like JavaScript which packs up all its things and goes away altogether, terminating all the script execution after the error is found.

CSS tries very hard to do what you want.

If a line has an error, it skips it and jumps to the next line without any error.

If you forget the semicolon on one line:

```css
p {
  font-size: 20px
  color: black;
  border: 1px solid black;
}
```

the line with the error AND the next one will **not** be applied, but the third rule will be successfully applied on the page. Basically, it scans all until it finds a semicolon, but  when it reaches it, the rule is now `font-size: 20px color: black;`, which is invalid, so it skips it.

Sometimes it's tricky to realize there is an error somewhere, and where that error is, because the browser won't tell us.

This is why tools like [CSS Lint](http://csslint.net/) exist.