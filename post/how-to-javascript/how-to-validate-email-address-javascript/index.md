---
title: "How to validate an email address in JavaScript"
date: 2018-09-27T07:00:00+02:00
description: "There are lots of ways to validate an email address. Learn the correct way, and also find out all the options you have, using plain JavaScript"
tags: js
---

Validation of an email address is one of the common operations one does when processing a form.

It's useful in contact forms, signup and login forms, and much more.

> Some people suggest that [you should not validate emails](https://davidcel.is/posts/stop-validating-email-addresses-with-regex/) at all. I think a little bit of validation, without trying to be over-zealous, is better.

## What are the rules that email validation should follow?

An email address is composed by 2 parts the local part, and the domain part.

The local part can contain

- any alphanumeric character: `a-zA-Z0-9`
- punctuation: `"(),:;<>@[\]`
- special characters: `!#$%&'*+-/=?^_``{|}~`
- a dot `.`, if it's not the first or last character. Also, it can't be repeated

The domain part can contain

- any alphanumeric character: `a-zA-Z0-9`
- the hyphen `-`, if it's not the first or last character. It can be repeated

## Use a Regex

The best option to validate an email address is by using a [**Regular Expression**](/javascript-regular-expressions/).

There is no _universal_ email check regex. Everyone seems to use a different one, and most of the regex you find online will fail the most basic email scenarios, due to inaccuracy or to the fact that they do not calculate the newer domains introduced, or internationalized email addresses

Don't use any regular expression blindly, but check it first.

I made [this example on Glitch](https://glitch.com/edit/#!/flavio-email-validation) that will check a list of email addresses considered valid against a regex. You can change the regex and compare it with other ones you want to use.

The one that's currently added is the one I consider the most accurate I found, slightly edited to fix an issue with multiple dots.

> Note: I did not came up with it. I found it in a Quora answer but I am not sure that was the original source.

This is a function that validates using that regex:

```js
const validate = (email) => {
    const expression = /(?!.*\.{2})^([a-z\d!#$%&'*+\-\/=?^_`{|}~\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF]+(\.[a-z\d!#$%&'*+\-\/=?^_`{|}~\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF]+)*|"((([ \t]*\r\n)?[ \t]+)?([\x01-\x08\x0b\x0c\x0e-\x1f\x7f\x21\x23-\x5b\x5d-\x7e\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF]|\\[\x01-\x09\x0b\x0c\x0d-\x7f\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF]))*(([ \t]*\r\n)?[ \t]+)?")@(([a-z\d\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF]|[a-z\d\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF][a-z\d\-._~\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF]*[a-z\d\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])\.)+([a-z\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF]|[a-z\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF][a-z\d\-._~\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF]*[a-z\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])\.?$/i;

    return expression.test(String(email).toLowerCase())
}
```

All the common cases are satisfied, one can assume that 99.9% of the email addresses people will add are validated successfully.

<!-- Copy and Paste Me -->
<div class="glitch-embed-wrap" style="height: 793px; width: 100%;">
  <iframe src="https://glitch.com/embed/#!/embed/flavio-email-validation?path=script.js&previewSize=47&previewFirst=true&sidebarCollapsed=true" alt="flavio-email-validation on glitch" style="height: 100%; width: 100%; border: 0;"></iframe>
</div>

The code of the glitch contains other regular expressions that you can easily try by remixing the project.

Although pretty accurate, there are a couple issues with some edge cases with this regex, which you can live with (or not) depending on your needs.

False negative for weird addresses like

```
"very.(),:;<>[]".VERY."very@\ "very".unusual"@strange.example.com

one."more\ long"@example.website.place
```


False negative for local addresses:

```
admin@mailserver1
user@localserver
```

of little use in publicly accessible websites (actually a plus in publicly accessible websites to have those denied)

Also, false negative for IP-based emails:

```
user@[2001:DB8::1]
user@128.0.0.1
```

There is a false positive for addresses with the local part too long:

```
1234567890123456789012345678901234567890123456789012345678901234+x@example.com
```

## Do you want a simpler regex?

The above regex is very complicated, to the point I won't even try to understand it. Regular expressions masters created it, and it spread through the Internet until I found it.

Using it at this point is a matter of copy/pasting it.

A much simpler solution is just to check that the address entered contains something, then an `@` symbol, and then something else.

In this case, this regex will do the trick:

```js
const expression = /\S+@\S+/
expression.test(String('my-email@test.com').toLowerCase())
```

This will cause many false positives, but after all **the ultimate test on an email address validity happens when you ask the user to click something in the email to confirm the address**, and I'd rather try to send to an invalid email than reject a valid email because of an error in my [regex](/javascript-regular-expressions/).

This is listed in the above Glitch, so you can easily try it.

## Validate the HTML field directly

HTML5 provided us the `email` field type, so don't forget you can also validate emails using that:

```html
<input type="email" name="email" placeholder="Your email">
```

Depending on the browser implementation also this validation will give you different results.

[This Glitch](https://flavio-input-email-chrome.glitch.me/) shows the same emails I tested the regex with, and their result when validated through the HTML form.

<!-- Copy and Paste Me -->
<div class="glitch-embed-wrap" style="height: 793px; width: 100%;">
  <iframe src="https://glitch.com/embed/#!/embed/flavio-input-email-chrome?path=README.md&previewSize=100&previewFirst=true" alt="flavio-input-email-chrome on glitch" style="height: 100%; width: 100%; border: 0;"></iframe>
</div>

The results are interesting, and here as well we have invalid emails that pass, and valid emails that don't. Our regex actually does a more accurate job than the HTML filtering built into the browser.

## Validate server-side

If your app has a server, the server needs to validate the email as well, because you can never trust client code, and also JavaScript might be disabled on the user browser.

Using Node.js you have the advantage of being able to reuse the frontend code as-is. In this case the function that validates can work both client-side and server-side.

You can also use pre-made packages like [isemail](https://github.com/hapijs/isemail), but also in this case results vary. Here is the isemail benchmark on the same emails we used above: <https://flavio-email-validation-node-isemail.glitch.me/>

<!-- Copy and Paste Me -->
<div class="glitch-embed-wrap" style="height: 793px; width: 100%;">
  <iframe src="https://glitch.com/embed/#!/embed/flavio-email-validation-node-isemail?path=server.js&previewFirst=true&sidebarCollapsed=true" alt="flavio-email-validation-node-isemail on glitch" style="height: 100%; width: 100%; border: 0;"></iframe>
</div>