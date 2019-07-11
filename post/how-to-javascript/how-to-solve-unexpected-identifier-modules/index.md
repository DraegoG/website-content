---
title: How to solve the unexpected identifier error when importing modules in JavaScript
date: 2019-01-31T07:00:00+02:00
description: "My advice on solving this problem I encountered"
tags: js
---

If you are using the `import` statement to import different files in your JavaScript application, you might find the browser giving you this error: *Unexpected Identifier*.

![Unexpected identifier](Screen Shot 2019-01-15 at 16.30.56.png)

Why? And how can you make ES6 modules work in browsers?

You just have to do one tiny change: instead of loading your main entry point JavaScript file using

```html
<script src="index.js"></script>
```

add `type="module"`:

```html
<script type="module" src="index.js"></script>
```

and things should now work fine.