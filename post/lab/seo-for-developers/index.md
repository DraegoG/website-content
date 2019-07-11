---
title: SEO for developers writing blogs
date: 2018-08-07T07:07:09+02:00
updated: 2018-08-14T07:07:09+02:00
description: "How do you win at SEO as a technical blogger? You know you want more visits, you want Google to send you more people every day"
tags: lab
---

<!-- TOC -->

- [Introduction](#introduction)
- [Content is king](#content-is-king)
- [Share your content](#share-your-content)
- [Play the long game](#play-the-long-game)
- [Write evergreen content](#write-evergreen-content)
- [Have an optimized structure for your content](#have-an-optimized-structure-for-your-content)

<!-- /TOC -->

## Introduction

Every time I post something on my blog, I know that there are already dozens if not hundreds of posts covering the same topic. This is perfectly normal: I might talk about technologies 10 years old, if not much older, and over time people wrote everything about them.

MDN, Google Developers, Smashing Magazine, CSS Tricks, Stack Overflow and many other big sites take the top positions of Google, whatever the topic might be. This is ok, and there is no way to change it.

It's the status quo, you have very few chances to get to the top spots in the Google search results, but there's an infinite long tail that you can still climb.

## Content is king

Someone once said "content is king". As a blogger, this is your truth: nothing is more important than content.

Focus on your content.

Write quality content made for your users. Forget about keyword research, keyword density and all that crap. Write things that your audience wants to read.

How do you know that? They will let you know over time. If you're just starting out, start writing everything you know about something you think people are interested in.

For example I'm a frontend developer and when I started, I first wrote about React and its ecosystem, something I knew everyone was interested into, or would be interested in the future.

Does every post I write rank well on Google? No!

3-4 posts get probably 30% of all visits. One post out of 5 will rank definitely better than the others. Sometimes it's a shot in the dark.

Some posts get very few visits per week, but I am confident that with proper linking of the articles I write, over time the posts that rank better will elevate the other posts to a higher ranking.

## Share your content

It's hard. You write the perfect piece of content and you just "hit the publish button" but now you're afraid to put in the battlefield called Reddit, or (gasp!) on Hacker News.

It's the same for everyone. Everyone has fear of having their work seen by the public.

One thing that helps me in this case is:

1. 95% of the times no one will pick up the post, and you're "fine".
2. in case the post picks up some good discussion and gets pushed to the front page, you'll get lots of great feedback.

Sometimes I hesitate at looking to comments because sometimes people on those sites are not kind 😆, but more often than not this is not really an issue, and the post is welcomed rather than criticized.

If I write things that are inaccurate, more experienced people don't hesitate to write a harsh comment (and this makes me correct it!).

Visitors coming from Reddit and Hacker News are regularly the worst "performers" in terms of retention and pageviews, according to Google Analytics, so gauging comments for me is the #1 reason I post things there.

What about Medium? Medium is a very cool platform,but remember, it's not your platform.

Always write posts on your own site under your own domain name, then import them in Medium using the import story functionality.

And most importantly, try to publish them in a publication that already has an audience. Publications want your content because they have a daily need for good written pieces to give to their knowledge-hungry people.

## Play the long game

Nothing is more important than content.

After that, nothing is more important than playing the long game.

I calculate that every post I write, unless some kind of _star alignment_ happens, will take at least 6 months before starting to rank well. How do I know this? **Experience**.

I started my first technical blog in 2007 and I ran it for 4 years until the content got obsolete. I was targeting technology that's now dead in the water, I wrote in italian (which was a mistake because my target audience was ~50x less than if I wrote in english) and I did some technical errors that cut my traffic in half and made my motivation sink (tip: never move to a different domain, even if your current domain sucks - even with all the correct redirects in place).

I re-started my blog in 2012, under the current domain, and I wrote a few posts over time, nothing fancy. In summer 2017 I started learning about the Go programming language with the intentions of getting a "real job" and I decided to blog every day about what I was learning, doing little tutorials in order to build up a "portfolio", and hopefully impress employers. Turns out I could not find a good Go remote opportunity that interested me, and I stopped blogging about it.

I switched to learning React, which was one of the things I always wanted to learn. I started writing about my new learnings on another website, which I called _writesoftware.org_. The domain was cool, and I had an ambitious project in mind. I wanted to write about all I knew and learned.

After a few months however I noticed my Go blog posts started to rank on Google. Week after week, the number nearly doubled until they got noticeably high. I thought "well, the domain must have some authority after all, and being old (5 years) it's more equipped to rank than my brand new domain here that no one knows". So in January 2018 I decided to gradually move my writesoftware.org posts to the flaviocopes.com blog, and rewrite them to be long-form content.

My blog posts about Go started ranking consistently about 5-6 months after I wrote them. And in the following months, they ranked even higher, leading to lots of people looking for Go tutorials on my website.

My new posts rarely rank fine. Sometimes one goes up to the top for the first 2 days, but then moves down in the rankings, only to slowly climb back up and consistently attract visitors for months.

## Write evergreen content

Notice the top ranking posts in each query. Those are blogs and sites that have been around forever.

Envision the future: what will happen if 5 or 10 years from now you're "one of the sites that have been around forever", and you stick in the top spot for many popular search terms?

Are your posts going to be relevant 5 years from now?

10 years from now?

Write evergreen content, don't write about news, conferences, what's in the last version of library X or anything like that.

## Have an optimized structure for your content

Content is king, right, but it must be served well.

Any CMS or site generator (I use Hugo) will let you apply a set of common techniques that make your content more prone to being

1. optimized for sharing
2. optimized for search engines

By optimized for sharing I mean you should have the `og` meta properties, that will show a proper card when shared on Twitter. Twitter is big for developers, and every post should have a custom image.

Optimized for search engines means that you should apply everything you can to make search engines like your content more. Nothing crazy, but

- have your site mobile first
- definitely make your site server-side rendered
- make the site as quick as possible. A static site is great
- use as little CSS and JavaScript as possible
- use schema.org microdata
- set the post published date and updated date as microdata
- add as much links as possible to other posts you have on your blog to increase on-site links

This should be enough to start with, without going too crazy.
