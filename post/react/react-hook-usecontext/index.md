---
title: How to use the useContext React hook
date: 2019-07-22T07:00:00+02:00
description: "Find out what the useContext React hook is useful for, and how to work with it!"
tags: react
---

> Check out my [React hooks introduction](/react-hooks/) first, if you're new to them.

One React hook I sometimes use is `useContext`.

```js
import React, { useContext } from 'react'
```

This hook is used in combination with the React Context API.

In particular, this hook allows us to get the current context value:

```js
const value = useContext(MyContext)
```

which refers to the nearest `<MyContext.Provider>` component.

Calling `useContext` will also make sure the component rerenders when the context value changes.

I recommend you to read my [Context API tutorial](/react-context-api/) to know more about it.