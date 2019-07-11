---
title: CSS Selectors
date: 2019-04-24T07:00:00+02:00
description: "Learn all the most important things about CSS Selectors"
tags: css
---

A selector allows us to associate one or more declarations to one or more elements on the page.

## Basic selectors

Suppose we have a `p` element on the page, and we want to display the words into it using the yellow color.

We can **target** that element using this selector `p`, which targets all the element using the `p` tag in the page. A simple CSS rule to achieve what we want is:

```css
p {
  color: yellow;
}
```

Every HTML tag has a corresponding selector, for example: `div`, `span`, `img`.

If a selector matches multiple elements, all the elements in the page will be affected by the change.

HTML elements have 2 attributes which are very commonly used within CSS to associate styling to a specific element on the page: `class` and `id`.

There is one big difference between those two: inside an HTML document you can repeat the same `class` value across multiple elements, but you can only use an `id` once. As a corollary, using classes you can select an element with 2 or more specific class names, something not possible using ids.

Classes are identified using the `.` symbol, while ids using the `#` symbol.

Example using a class:

```html
<p class="dog-name">
  Roger
</p>
```

```css
.dog-name {
  color: yellow;
}
```

Example using an id:

```html
<p id="dog-name">
  Roger
</p>
```

```css
#dog-name {
  color: yellow;
}
```

## Combining selectors

So far we've seen how to target an element, a class or an id. Let's introduce more powerful selectors.

### Targeting an element with a class or id

You can target a specific element that has a class, or id, attached.

Example using a class:

```html
<p class="dog-name">
  Roger
</p>
```

```css
p.dog-name {
  color: yellow;
}
```

Example using an id:

```html
<p id="dog-name">
  Roger
</p>
```

```css
p#dog-name {
  color: yellow;
}
```

Why would you want to do that, if the class or id already provides a way to target that element? You might have to do that to have more [specificity](/css-specificity/). We'll see what that means later.

### Targeting multiple classes

You can target an element with a specific class using `.class-name`, as you saw previously. You can target an element with 2 (or more) classes by combining the class names separated with a dot, without spaces.

Example:

```html
<p class="dog-name roger">
  Roger
</p>
```

```css
.dog-name.roger {
  color: yellow;
}
```

### Combining classes and ids

In the same way, you can combine a class and an id.

Example:

```html
<p class="dog-name" id="roger">
  Roger
</p>
```

```css
.dog-name#roger {
  color: yellow;
}
```

## Grouping selectors

You can combine selectors to apply the same declarations to multiple selectors. To do so, you separate them with a comma.

Example:

```html
<p>
  My dog name is:
</p>
<span class="dog-name">
  Roger
</span>
```

```css
p, .dog-name {
  color: yellow;
}
```

You can add spaces in those declarations to make them more clear:

```css
p,
.dog-name {
  color: yellow;
}
```

## Follow the document tree with selectors

We've seen how to target an element in the page by using a tag name, a class or an id.

You can create a more specific selector by combining multiple items to follow the document tree structure. For example, if you have a `span` tag nested inside a `p` tag, you can target that one without applying the style to a `span` tag not included in a `p` tag:

```html
<span>
  Hello!
</span>
<p>
  My dog name is:
  <span class="dog-name">
    Roger
  </span>
</p>
```

```css
p span {
  color: yellow;
}
```

See how we used a space between the two tokens `p` and `span`.

This works even if the element on the right is multiple levels deep.

To make the dependency strict on the first level, you can use the `>` symbol between the two tokens:

```css
p > span {
  color: yellow;
}
```

In this case, if a `span` is not a first children of the `p`  element, it's not going to have the new color applied.

Direct children will have the style applied:

```html
<p>
  <span>
    This is yellow
  </span>
  <strong>
    <span>
      This is not yellow
    </span>
  </strong>
</p>
```

Adjacent sibling selectors let us style an element only if preceded by a specific element. We do so using the `+` operator:

Example:

```css
p + span {
  color: yellow;
}
```

This will assign the color yellow to all span elements preceded by a `p` element:

```html
<p>This is a paragraph</p>
<span>This is a yellow span</span>
```

We have a lot more selectors we can use:

- attribute selectors
- pseudo class selectors
- pseudo element selectors

More on those on future posts.