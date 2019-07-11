---
title: "How to estimate programming time"
date: 2019-01-10T07:00:00+02:00
description: "The fine art of estimating how long it takes to create software"
tags: lab
---

I really want to tell everyone how I estimate the time needed to build software projects.

In the past 10 years I've been asked this hundreds of times.

- "We need to implement this feature. How long is it going to take you?"
- "Give me a detailed overview of how much time this project is going to take in terms of time. 1 month? 2 months?"
- "I want you to ship this. 50 hours of billable time are enough?"

The answer to those questions have either been a **bet**, in the most optimistic case. Or a **leap of faith**, knowing that if I promised a number, that would probably have been my paycheck regardless of the actual time it took.

Sometimes with long term clients I was able to amortize the projects that exceeded my estimations with projects where I completed the work earlier than I expected, letting the client know.

Ultimately I ended up saying "**I can't estimate**".

So, the answer to "I really want to tell everyone how I estimate the time needed to build software projects" is: **I don't**.

But I can estimate that **no one is really able to estimate** when it comes to building software, because of the inner complexities that this field can put against you.

"Real engineers" are going to find this hard to admit, but I've never been your typical real engineer type.

Estimating is probably the hardest thing when working as a developer.

Here's a cool reference table you can use when you need to estimate a task

Task | You Estimate | You Forgot |  Actual Time Needed
-----|--------------|------------|--------------------|
A small bugfix | 2 minutes | We need to find the function that has the bug in the source code, git pull, check that we didn't break any other function, we need to add some tests, run the tests, fix the tests we broke, deploy, update the bug tracker | 2 hours
A minor feature | 2 hours | You need to fix that TODO left in the code in the function you are going to edit, and see why there is a `//don't touch this` comment. You need to carefully do manual testing, plus browser testing, and check why on Edge is not working like expected. Oh we need to update all the screenshots in the docs | 10 hours
Improve the performance of an endpoint | 10 hours | You need precise benchmarks which you can use to prove your new implementation is working correctly, and add 10 more tests that were not present before, otherwise you risk breaking production code used by 10000s of clients | 5 days
Rewrite the whole frontend code | 3 weeks | You just start with the new _more scalable_ framework you were experimenting with, without touching the UI, but you run into a whole new set of issues but this time there is no StackOverflow or Google to help, as the framework is too new. You are having unique problems, and you'd need to hire the library maintainer to work with you, but he already moved on to the next great thing. While you are at it, the UI team decides to work on a complete rewrite of the interface, 2 times. The product managers at mid time wants to pivot to a slightly different product| 12 months

This might be a good estimation of our lack of estimation, but of course things can also work in the reverse: a thing you estimate might take 5 days might only take 1 day because you find everything is already in place to add it, and it takes much less than anticipated.

Some might overestimate, projecting they might have difficulties, adding a 30% more of what they think.

Team projects estimation is even harder, I won't even try.

What to do then?

Instead of detailed estimating, I propose continuous communication with the client or boss or whoever commissioned your work, and do weekly checkups on the project progress. Without pre-defining when the process will end.

Because after all the process will never end.