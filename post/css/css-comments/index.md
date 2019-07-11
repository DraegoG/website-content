---
title: CSS Comments
date: 2019-06-25T07:00:00+02:00
description: "How to work with comments in CSS"
tags: css
---

CSS gives you the ability to write comments in a CSS file, or in the `style` tag in the page header

The format is the `/* this is a comment */` C-style (or JavaScript-style, if you prefer) comments.

This is a multiline comment. Until you add the closing `*/` token, the all the lines found after the opening one are commented.

Example:

```css
#name { display: block; } /* Nice rule! */

/* #name { display: block; } */

#name {
	display: block; /*
	color: red;
	*/
}
```

CSS does not have inline comments, like `//` in C or JavaScript.

Pay attention though - if you add `//` before a rule, the rule will not be applied, looking like the comment worked. In reality, CSS detected a syntax error and due to how it works it ignored the line with the error, and went straight to the next line.

Knowing this approach lets you purposefully write inline comments, although you have to be careful because you can't add random text like you can in a block comment.

For example:

```css
// Nice rule!
#name { display: block; }
```

In this case, due to how CSS works, the `#name` rule is actually commented out. You can find more details [here](https://www.xanthir.com/b4U10) if you find this interesting. To avoid shooting yourself in the foot, just avoid using inline comments and rely on block comments.