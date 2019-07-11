---
title: "HTML container tags"
seotitle: "How to use container tags in HTML"
date: 2019-08-07T07:00:00+02:00
description: "Discover how to use container tags in HTML and find out which one to choose"
tags: html
---

## Container tags

HTML provides a set of container tags. Those tags can contain an unspecified set of other tags.

We have:

- `article`
- `section`
- `div`

and it can be confusing to understand the difference between them.

Let's see when to use each one of them.

### `article`

The article tag identifies a *thing* that can be independent from other *things* in a page.

For example a list of blog posts in the homepage.

Or a list of links.

```html
<div>
	<article>
		<h2>A blog post</h2>
		<a ...>Read more</a>
	</article>
	<article>
		<h2>Another blog post</h2>
		<a ...>Read more</a>
	</article>
</div>
```

We're not limited to lists: an article can be the main element in a page.

```html
<article>
	<h2>A blog post</h2>
	<p>Here is the content...</p>
</article>
```

Inside an `article` tag we should have a title (`h1`-`h6`) and

### `section`

Represents a section of a document. Each section has a heading tag (`h1`-`h6`), then the section _body_.

Example:

```html
<section>
	<h2>A section of the page</h2>
	<p>...</p>
	<img ... />
</section>
```

It's useful to break a long article into different **sections**.

Shouldn't be used as a generic container element. `div` is made for this.

### `div`

`div` is the generic container element:

```html
<div>
	...
</div>
```

You often add a `class` or `id` attribute to this element, to allow it to be styled using CSS.

We use `div` in any place where we need a container but the existing tags are not suited.

## Tags related to page

### `nav`

This tag is used to create the markup that defines the page navigation. Into this we typically add an `ul` or `ol` list:

```html
<nav>
	<ol>
		<li><a href="/">Home</a></li>
		<li><a href="/blog">Blog</a></li>
	</ol>
</nav>
```

### `aside`

The `aside` tag is used to add a piece of content that is related to the main content.

A box where to add a quote, for example. Or a sidebar.

Example:

```html
<div>
  <p>some text..</p>
  <aside>
    <p>A quote..</p>
  </aside>
  <p>other text...</p>
</div>
```

Using `aside` is a signal that the things it contains are not part of the regular flow of the section it lives into.

### `header`

The `header` tag represents a part of the page that is the introduction. It can for example contain one or more heading tag (`h1`-`h6`), the tagline for the article, an image.

```html
<article>
  <header>
	  <h1>Article title</h1>
  </header>
  ...
</div>
```

### `main`

The `main` tag represents the main part of an article:

```html
<article>
  ....
  <main>
    <p>....</p>
  </main>
</div>
```

### `footer`

The `footer` tag is used to determine the footer of an article, or the footer of the page:

```html
<article>
 ....
	<footer>
    <p>Footer notes..</p>
  </footer>
</div>
```

