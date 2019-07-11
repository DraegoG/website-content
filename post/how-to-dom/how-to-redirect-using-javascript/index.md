---
title: "How to redirect to another web page using JavaScript"
date: 2018-05-21T07:06:15+02:00
description: "JavaScript offers many ways to redirect the user to a different web page. Learn the canonical way, and also find out all the options you have, using plain JavaScript"
tags: js
---

JavaScript offers many ways to redirect the user to a different web page, if during the execution of your program you need to move to a different page.

The one that can be considered canonical to navigate to a new URL is

```js
window.location = 'https://newurl.com'
```

If you want to redirect to a different path, on the same domain, use:

```js
window.location.pathname = '/new'
```

This is using the `location` object offered by the [History API](/history-api/).

## Other options to redirect

As with most things in programming, there are many ways to perform the same operation.

Since `window` is implicit in the browser, you can also do:

```js
location = 'https://newurl.com'
```

Another way is to set the `href` property of `location`:

```js
window.location.href = 'https://newurl.com'
```

`location` also has an `assign()` method that accepts a URL, and performs the same thing:

```js
window.location.assign('https://newurl.com')
```

The `replace()` method is different than the previous ways because it rewrites the current page in the history. The current page is wiped, so when you click the "back" button, you go back to the page that _now_ is the last visited one.

```js
window.location.replace('https://newurl.com')
```

This can be convenient in some situations.

## Different ways to reach the `window` object

The browser exposes the `self` and `top` objects, which all reference the `window` object, so you can use them instead of `window` in all the examples above:

```js
self.location = 'https://newurl.com'

top.location = 'https://newurl.com'
```

## 301 redirect using a server-side directive

The above examples all consider the case of a programmatic decision to move away to a different page.

If you need to redirect because the current URL is old, and move the a new URL, it's best to use server-level directive and set the 301 HTTP code to signal search engines that the current URL has permanently moved to the new resource.

This can be done via `.htaccess` if using Apache. [Netlify](/netlify/) does this through a [`_redirects` file](https://www.netlify.com/docs/redirects/).

## Are 301 redirects possible using JavaScript?

Unfortunately not.

That's not possible to do on the client-side.

The 301 HTTP response code must be sent from the server, well before the JavaScript is executed by the browser.

Experiments say that JavaScript redirects are interpreted by the search engines like 301 redirects. See [this Search Engine Land post](https://searchengineland.com/tested-googlebot-crawls-javascript-heres-learned-220157) for reference.

[Google says](https://support.google.com/webmasters/answer/2721217?hl=en):

> Using JavaScript to redirect users can be a legitimate practice. For example, if you redirect users to an internal page once they’re logged in, you can use JavaScript to do so. When examining JavaScript or other redirect methods to ensure your site adheres to our guidelines, consider the intent. Keep in mind that 301 redirects are best when moving your site, but you could use a JavaScript redirect for this purpose if you don’t have access to your website’s server.

## Use an HTML meta tag

Another option is using a meta tag in your HTML:

```html
<html>
  <head>
    <meta http-equiv="refresh" content="0;URL=https://newurl.com/">
  </head>
</html>
```

This will cause the browser to load the new page once it has loaded and interpreted the current one, and not signal search engines anything. The best option is always to use a 301 server-level redirect.