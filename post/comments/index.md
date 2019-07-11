---
title: "Should I write comments?"
date: 2019-01-28T07:00:00+02:00
description: "Thoughts on commenting code, and on commenting the right way"
---

We're often told that comments are very important. Comments are a big and important part of programming.
As a beginner it's difficult to judge and determine how many comments you should add, and what to write in comments!

That's one of the things that are not fixed in stone, everyone seems to have a different and contrasting opinion, and so this leaves you in a limbo filled with insecurity.

This is my line of thinking: *you should write comments, as few as you possibly can, to explain your decisions*.

Let's dissect this.

Your code should be self explanatory, as much as you can.

High level languages like JavaScript or Python are very readable. You can almost read the code aloud and think it's plain english, if you name your variables and methods correctly.

Some things are going to require some more thinking, but even if code is a bit complex, as long as a programmer can read it and determine 100% what the code does, it should not need comments.

You need comments when you have to explain the *why* of a particular instruction or block. Not the _what_, that should be inferred from the code. We call it high level for a reason: it's code we can think about. It's not machine language or assembly, which is very very hard to read and understand.

Some blocks of your code will need comments to explain others, or *even yourself*, *why* you are doing a particular thing. Not always of course, not when it's obvious.

By even 6 months down the line, if you work on a separate part of the codebase and then come back to that line of code, you will most likely not remember everything that was at stake when you edited it. You might recall 90% of the reasons you added something, but there was that something else you can't find out.. a comment would be great for that.

Code is not just instructions and comments. A lot of times you can see why a line of code was added thanks to source control ([Git](/git/)). You look the line up in your Git app, and the history of that line will tell you why you or your coworker edited that 10 months ago. If the Git commit message was helpful and detailed, not "Fix the bug". That's also a good documentation, especially good in Open Source projects which can have lots of people touching the codebase.

If you're at a job interview, and you ask yourself "should I add comments in my exercise?" the answer is always *yes*.

Will they most likely judge you for your comments as well as for your code. And what you write in the comments, too.

I would certainly do it. No matter how much a code wizard you can be, maybe the company needs to fire you in 3 months and the next person coming to replace you will need to understand your code, as that's a company asset. They can't really afford to hire someone that is not willing, or able, to have empathy for other people trying to read the source code.