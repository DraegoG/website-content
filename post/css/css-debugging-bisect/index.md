---
title: "How to debug CSS by bisecting"
description: "One of the workflows I use to debug CSS"
date: 2019-03-06T07:00:00+02:00
tags: css
---

I had this problem today.

I added the Paddle button to my new online course page, so people could click the "Buy now" button and the nice Paddle popup would show up.

The popup has a loading indicator, a circle with a spinner inside, and there was an issue: when clicking the "Buy now" button, the spinner indicator was not centered inside the circle, as show in this gif:

![](cmjPX6hjLm.gif)

I didn't really know what was causing the issue, so I was thinking how to solve it.

The principle I use in these cases is **bisect**. I also call it [divide et impera](https://en.wikipedia.org/wiki/Divide_and_rule).

I opened the DevTools and moved to the Sources panel, which showed all the files loaded in the page. I searched for one of my CSS files, as my intuition was that the page CSS was interfering with the Paddle own CSS rules.

So I removed *all* the content of that file.

Chrome automatically changes the appearance of the page when you alter the CSS files in the Sources panel, so I was able to check and see that the spinner was now working fine!

![](whJvrttQeJ.gif)

So, one of the rules in that CSS is the problem.

How do I find out which line?

The file has 312 lines. I select from line 150 to 312 and delete it. Try again. The problem is still there, so it must originate from the first 149 lines.

I hit cmd-Z (*undo*) to put back those lines I removed, and delete lines 70-149.

The problem is gone, so the problematic line is in there. I hit cmd-Z again to restore the lines I deleted.

And so on, you got the idea. Rinse and repeat until you find the line that gives you the problem.