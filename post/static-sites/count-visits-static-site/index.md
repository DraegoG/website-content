---
title: "How to get the real number of pageviews of a static site"
date: 2019-07-01T07:00:00+02:00
description: "Given a static site, how do you get the real count of visitors?"
tags: lab
---

This is a static site. I use Google Analytics, and my audience is developers.

A perfect combination for inaccurate analytics data, since many developers use an ad blocker, which might (or might not, it depends) block the Google Analytics data from being transmitted to the servers. Some developers even completely block JavaScript, but I assume this is a smaller set of people, and so a less problematic thing.

I always had this doubt: what is the real number of visitors? What percentage of visitors am I looking at?

My hosting provider does not give any information about visits. I just know the bandwidth I consume.

So I decided to test an idea.

I include an image in every post, a very small image.

It's nothing new: email marketing software automatically uses this  "trick" to count open rates.

I used 1px x 1px SVG image, 141 bytes of data to have minimal impact.

I made a Node.js web server on Glitch: <https://glitch.com/~static-site-visitors-counter>. If you include the image in the website, like this:

```html
<img src="https://<name-of-the-project>.glitch.me/pixel.svg" />
```

the Node.js web server living on that `<name-of-the-project>.glitch.me` URL is going to send the image back.

But first, it increments a value:

```js
const express = require('express')
const app = express()
let counter = 0

app.use(express.static('public', {
  setHeaders: (res, path, stat) => {
    console.log(++counter)
  }
}))

const listener = app.listen(process.env.PORT, () => {
  console.log('Your app is listening on port ' + listener.address().port)
})
```

The important part of this app is the object we pass to `express.static()`. Normally we don't pass an additional object to this method, but in there the `setHeaders()` function is provided so we can set some additional headers for the file which is going to be served.

We add our `console.log()` there, misusing this function for our purpose.

It's very simple, and due to how Glitch works the counter will reset every time you update the app.

This is not supposed to be your analytics tool, of course. Just a way to quickly test if the analytics data matches the reality. Almost no one blocks images, normally.

And this can be done differently, since I use an SVG I could also just send a string back to the client, with the appropriate `Content-Type` header. I don't know if that would be faster or not, I haven't tried.

You could also serve a CSS file in the same way. I just happened to choose an image.

I let this run for 3-4 hours and the data, compared to the Google Analytics logs, showed me that about 10% of the people that visit my site don't send data to Google Analytics.

Not a lot. I expected much more, like 2x the visitors. Or 50% more. But just a 10% increment.

Which is actually best for me, since this means the Google Analytics data is still very useful.

Here's the full app code:

<!-- Copy and Paste Me -->
<div class="glitch-embed-wrap" style="height: 420px; width: 100%;">
  <iframe
    allow="geolocation; microphone; camera; midi; vr; encrypted-media"
    src="https://glitch.com/embed/#!/embed/static-site-visitors-counter?path=server.js&previewSize=0"
    alt="static-site-visitors-counter on Glitch"
    style="height: 100%; width: 100%; border: 0;">
  </iframe>
</div>