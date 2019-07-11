---
title: "The pros of using a boring stack"
date: 2019-01-08T07:00:00+02:00
description: "Why I think choosing a boring stack is important in programming"
tags: lab
---

A person asked me a question a few days ago. The person wanted to start a blog, and they decided to write their own platform for it, using Angular in the frontend.

My reply was that if the goal was blogging, then they had to scratch that idea, and use an off the shelf solution.

That must have been badly received, as I didn't get a reply, but my point is this: if you want to create a blog and be serious at it, then use the most boring and bulletproof thing you can find.  Definitely **don't work on your blog infrastructure if you want to do any serious blogging**.

**The tech must go out of the way**, you should only **focus on the content**.

Otherwise you'll spend most of your free time tweaking the blog platform (which - let's be clear - **no one except you cares about**) instead of writing content. No one cares about that infrastructure.

If you want to make a video, are you going to write a YouTube clone first? Can it handle 100M simultaneous visitors? Reminds me of people wanting to write video games and starting to build a physics engine first, never ending the game in the process.

I use Hugo, a static site generator.

Hugo is the best one for me as it's focused on blogging and markdown. It is **boring**. Its templating language is boring. It's so boring that when I have to tweak something I fall asleep. I love it.

The best feature of Hugo is that it's **fast**, I think mostly thanks to the use of Go under the hoods. Looks like a boring feature these days.

> "Look at Gatsby, it's so fancy and shiny!"

[Gatsby](/gatsby/) (just used as an example, nothing against it) is already too much fancy for my taste, even though it's a great tech. Why? It makes you focus too much on the tech and less on the outcome. As a developer, you might feel that is awesome, but it's not. React, GraphQL, it's all a bit too exciting.

It reminds me of Redux, and people excited about the demo with "time travel", a really useful feature for day to day coding [end of joke]. People happily overcomplicated their apps just to use a shiny tech.

Let's talk about prefetching for example. Do we really need prefetching when a static site is already as fast as possible? Are our blog visitors asking for it? What are the cons? What can go wrong?

> Remember Murphy's law: "Anything that can go wrong will go wrong"

I once talked to a person that started a blog using Gatsby only to realize they didn't enable server side rendering, even though they though they had it enabled, which made the blog nearly invisible to Google (yes I know they execute JS *sometimes*, but bear with me, **stick to boring server side rendering**).

In an average blog, you get an average of 1.1 / 1.2 page view per user. This means the vast majority of your users are going to come to your site, probably via Google, take a quick look and go away. Do you really need to prefetch all your links? Why waste all that data and power?

Let's stop going against Gatsby, I really like it as a tool to make websites and apps.

My point was that to start a simple blog, you don't need probably 80% of what it does. Use a simpler tool, a tool made just for blogging, and definitely don't write your own.

This applies to more complex applications. Should you use the technology you know since 10 years, or should you jump on that cool tech you know nothing about, but everyone talks nicely about? Should you use Rails, or Elixir? Should I write my next app in [TypeScript](/typescript/) or Reason? C, Go or Rust?

Lots and lots of man hours are lost forever as we collectively jump from old library to new library and from old framework to new framework. Think jQuery, Backbone and Ember, plus all the gazillions ones that came before or after them. Think AngularJS vs Angular. Think all the PHP frameworks that came before Laravel took the PHP world by storm. Remember the NoSQL "revolution" that made us all reconsider using MySQL in favor of fancier and more flexible database systems? Turns out SQL is still going strong.

> "Just use MySQL, the boring tech revolution is here" Marty Weiner, Reddit CTO, 2016

Most of the tools that developers consider industry standards are build in huge companies like Google and Facebook and they are perfect for their needs. A small team or solo developer might happen to have the same needs, but is that likely? Or is it all driven by the peer pressure and hype? Or by marketing?

Is the thing you want to do perfectly achievable with plain JavaScript and the [DOM](/dom/) APIs, or do you really need to rewrite all your application in [React](/react/) and spend days trying to make [Webpack](/webpack/) do what you want? Sometimes that's a great choice, sometimes a less than perfect one. Working with the DOM APIs feels boring, but that might make your app much faster, while everyone else in the engineering circle says it's going to be a mess, you might ship it in 10x less time and it might work 10x better.

One rule is that you know the pitfalls of your platform, the grass is always greener on the other side of the fence, and you like to imagine new platforms being 100% perfect. That never happens, and the devil is in the details.

Details that maybe you mastered in years of investing in that stack that now looks boring to you, because you are an engineer! You like challenges! You don't want to miss out on the opportunity to learn new things!

You can still do it.

I think that you should always experiment, create side projects, but when it comes to critical platforms (like your blog platform, that's critical if you are serious at it), the boring tech is better. And understanding this concept is part of becoming a senior developer.

