---
title: "Using SASS in React"
date: 2018-12-26T07:00:00+02:00
description: "How to use SASS to style a React application"
tags: react
---

When you build a React application using [`create-react-app`](https://flaviocopes.com/react-create-react-app/), you have many options at your disposal when it comes to styling.

> Of course, if not using `create-react-app`, you have all the choices in the world, but we limit the discussion to the `create-react-app`-provided options.

You can style using plain classes and CSS files, using the style attribute or CSS Modules, to start with.

SASS/SCSS is a very popular option, a much loved one by many developers.

You can use it without any configuration at all, starting with `create-react-app` 2.

All you need is a `.sass` or `.scss` file, and you just import it in a component:

```js
import './styles.scss'
```

You can see an example of it working at <https://codesandbox.io/s/18qq31rp3>.

<iframe src="https://codesandbox.io/embed/18qq31rp3" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>
