---
title: "React concepts: declarative"
date: 2018-11-03T07:00:00+02:00
description: "What does it mean when you read that React is declarative"
tags: react
---

You'll run across articles describing React as a **declarative approach to building UIs**.

React made its "declarative approach" quite popular and upfront so it permeated the frontend world along with React.

It's really not a new concept, but React took building UIs a lot more declaratively than with HTML templates:

- you can build Web interfaces without even touching the DOM directly
- you can have an event system without having to interact with the actual DOM Events.

The opposite of declarative is **imperative**. A common example of an imperative approach is looking up elements in the DOM using jQuery or DOM events. You tell the browser exactly what to do, instead of telling it what you need.

The React declarative approach abstracts that for us. We just tell React we want a component to be rendered in a specific way, and we never have to interact with the DOM to reference it later.
