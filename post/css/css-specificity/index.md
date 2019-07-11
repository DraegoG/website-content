---
title: CSS Specificity
date: 2019-04-26T07:00:00+02:00
description: "Learn what CSS Specificity means and why it's important"
tags: css
---

What happens when an element is targeted by multiple rules, with different selectors, that affect the same property?

For example, let's talk about this element:

```html
<p class="dog-name">
  Roger
</p>
```

We can have

```css
.dog-name {
  color: yellow;
}
```

and another rule that targets `p`, which sets the color to another value:

```css
p {
  color: red;
}
```

And another rule that targets `p.dog-name`. Which rule is going to take precedence over the others, and why?

Enter specificity. **The more specific rule will win**.
If two or more rules have the **same specificity, the one that appears last wins**.

Sometimes what is more specific in practice is a bit confusing to beginners. I would say it's also confusing to experts that do not look at those rules that frequently, or simply overlook them.

## How to calculate specificity

Specificity is calculated using a convention.

We have 4 slots, and each one of them starts at 0: `0 0 0 0 0`. The slot at the left is the most important, and the rightmost one is the least important.

Like it works for numbers in the decimal system: `1 0 0 0` is higher than `0 1 0 0`.

### Slot 1

The first slot, the rightmost one, is the least important.

We increase this value when we have an **element selector**. An element is a tag name. If you have more than one element selector in the rule, you increment accordingly the value stored in this slot.

Examples:

```css
p {} 					    /* 0 0 0 1 */
span {} 				  /* 0 0 0 1 */
p span {} 			  /* 0 0 0 2 */
p > span {} 			/* 0 0 0 2 */
div p > span {} 	/* 0 0 0 3 */
```

### Slot 2

The second slot is incremented by 3 things:

- class selectors
- pseudo-class selectors
- attribute selectors

Every time a rule meets one of those, we increment the value of the second column from the right.

Examples:

```css
.name {}				  /* 0 0 1 0 */
.users .name {}		/* 0 0 2 0 */
[href$='.pdf'] {}	/* 0 0 1 0 */
:hover {}				  /* 0 0 1 0 */
```

Of course slot 2 selectors can be combined with slot 1 selectors:

```css
div .name {}			  	  /* 0 0 1 1 */
a[href$='.pdf'] {}		  /* 0 0 1 1 */
.pictures img:hover {}  /* 0 0 2 1 */
```

One nice trick with classes is that you can repeat the same class and increase the specificity. For example:

```css
.name {}				    /* 0 0 1 0 */
.name.name {}		    /* 0 0 2 0 */
.name.name.name {}	/* 0 0 3 0 */
```

### Slot 3

Slot 3 holds the most important thing that can affect your CSS specificity in a CSS file: the `id`.

Every element can have an `id` attribute assigned, and we can use that in our stylesheet to target the element.

Examples:

```css
#name {}					/* 0 1 0 0 */
.user #name {}		/* 0 1 1 0 */
#name span {}			/* 0 1 0 1 */
```

### Slot 4

Slot 4 is affected by inline styles. Any inline style will have precedence over any rule defined in an external CSS file, or inside the `style` tag in the page header.

Example:

```css
<p style="color: red">Test</p> /* 1 0 0 0 */
```

Even if any other rule in the CSS defines the color, this inline style rule is going to be applied. Except for one case - if `!important` is used, which fills the slot 5.

## Importance

Specificity does not matter if a rule ends with `!important`:

```css
p {
  font-size: 20px!important;
}
```

That rule will take precedence over any rule with more specificity

Adding `!important` in a CSS rule is going to make that rule be more important than any other rule, according to the specificity rules. The only way another rule can take precedence is to have `!important` as well, and have higher specificity in the other less important slots.

## Tips

In general you should use the amount of specificity you need, but not more.  In this way, you can craft other selectors to overwrite the rules set by preceding rules without going mad.

`!important` is a highly debated tool that CSS offers us. Many CSS experts advocate against using it. I find myself using it especially when trying out some style and a CSS rule has so much specificity that I need to use `!important` to make the browser apply my new CSS.

But generally, `!important` should have no place in your CSS files.

Using the `id` attribute to style CSS is also debated a lot, since it has a very high specificity. A good alternative is to use classes instead, which have less specificity, and so they are easier to work with, and they are more powerful (you can have multiple classes for an element, and a class can be reused multiple times).

## Tools to calculate the specificity

You can use the site <https://specificity.keegan.st/> to perform the specificity calculation for you automatically.

It's useful especially if you are trying to figure things out, as it can be a nice feedback tool.