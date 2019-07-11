---
title: "Should you use jQuery or React?"
date: 2018-11-09T07:00:00+02:00
description: "The tl;dr is, it depends!"
tags: react
---

First, you might not need jQuery at all, and just use the Web Platform APIs, but this is another story.

Let's focus on the question. Should you use jQuery or React?

My answer is this. If you are building a Single Page Application, React is the obvious choice. React was built for this, and will take care of generating the views and rendering the elements in the page without you having to even think about the DOM, aka the nitty-gritty details of how to present the content on the page.

React follows a declarative approach, and using it you can work at a much higher level.

jQuery (or the native browser APIs) should not really be used when building an SPA, as things might get complicated very quickly.

It's best suited at adding interactive parts to a page that's most likely server-rendered, although it can co-exist within a React app.

With jQuery you interact directly with the DOM to select elements, using selectors to find the thing in the page you want to act upon.

It's both much lower level, and more prone to complications as the size of your application grows.