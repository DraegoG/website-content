---
title: How to use the useMemo React hook
date: 2019-07-20T07:00:00+02:00
description: "Find out what the useMemo React hook is useful for, and how to work with it!"
tags: react
---

> Check out my [React hooks introduction](/react-hooks/) first, if you're new to them.

One React hook I sometimes use is `useMemo`.

```js
import React, { useMemo } from 'react'
```

This hook is used to create a memoized value.

> This hook is very similar to [useCallback](/react-hook-usecallback/), the difference is that `useCallback` returns a memoized callback and `useMemo` returns a memoized value, the result of that function call. The use case is different, too. `useCallback` is used for callbacks passed to child components.

Sometimes you have to compute a value, either through a complex calculation or by reaching to the database to make a costly query or to the network.

Using this hook, this operation is done only once, then the value will be stored in the memoized value and the next time you want to reference it, you'll get it much faster.

Here's how to use it:

```js
const memoizedValue = useMemo(() => expensiveOperation())
```

Make sure you add that empty array as a second parameter to `useMemo()`, otherwise no memoization will happen at all.

If you need to pass arguments, you also need to pass them in the array:

```js
const memoizedValue = useMemo(() => expensiveOperation(param1, param2), [param1, param2])
```

If one of the parameters change when you try to access the value, the value of course will be calculated without memoization.
