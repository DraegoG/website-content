---
title: CSS Vendor Prefixes
date: 2019-05-26T07:00:00+02:00
description: "An overview of the CSS Vendor Prefixes, Autoprefixer and why they are not much relevant going forward"
tags: css
---

Vendor prefixes are one way browsers use to give us CSS developers access to newer features not yet considered stable.

Before going on keep in mind this approach is declining in popularity though, in favour of using **experimental flags**, which must be enabled explicitly in the user's browser.

Why? Because developers instead of considering vendor prefixes as a way to preview features, they shipped them in production - something considered harmful by the CSS Working Group.

Mostly because once you add a flag and developers start using it in production, browsers are in a bad position if they realise something must change. With flags, you can't ship a feature unless you can push all your visitors to enable that flag in their browser (just joking, don't try).

That said, let's see what vendor prefixes are.

I specifically remember them for working with CSS Transitions in the past. Instead of just using the `transition` property, you had to do this:

```css
.myClass {
	-webkit-transition: all 1s linear;
	-moz-transition: all 1s linear;
	-ms-transition: all 1s linear;
	-o-transition: all 1s linear;
	transition: all 1s linear;
}
```

Now you just use

```css
.myClass {
	transition: all 1s linear;
}
```

since the property is now well supported by all modern browsers.

The prefixes used are:

- `-webkit-` (Chrome, Safari, iOS Safari / iOS WebView, Android)
- `-moz-` (Firefox)
- `-ms-` (Edge, Internet Explorer)
- `-o-` (Opera, Opera Mini)

Since Opera is Chromium-based and Edge will soon be too, `-o-` and `-ms-` will probably go soon out of fashion. But as we said, vendor prefixes as a whole are going out of fashion, too.

Writing prefixes is hard, mostly because of uncertainty. Do you actually need a prefix for one property? Several online resources are outdated, too, which makes it even harder to do right.
Projects like [Autoprefixer](https://github.com/postcss/autoprefixer) can automate the process in its entirety without us needing to find out if a prefix is needed any more, or the feature is now stable and the prefix should be dropped. It uses data from caniuse.com, a very good reference site for all things related to browser support.

If you use React or Vue, projects like `create-react-app` and Vue CLI, two common ways to start building an application, use `autoprefixer` out of the box, so you don't even have to worry about it.