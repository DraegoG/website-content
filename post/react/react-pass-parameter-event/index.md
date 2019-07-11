---
title: "How to pass a parameter to event handlers in React"
date: 2019-01-18T07:00:00+02:00
description: "Find out how to pass a parameter to onClick events for example, without invoking the method on mount"
tags: react
---

When you work on a React function component you might have the need to attach an event to onClick (or other events).

You usually do:

```js
<button onClick={addBill}>Add</button>
```

But what if you have to pass a parameter? Say you have a list of bills, and you want to remove one by clicking the "X" next to it.

You can't do:

```js
<button onClick={removeBill(index)}>𝗫</button>
```

because the expression inside onClick is going to be executed on mount. This is going to delete all the bills in the list, as soon as the app is started.

Instead, this is what you need to do, using arrow functions:

```js
<button onClick={() => removeBill(index)}>𝗫</button>
```
