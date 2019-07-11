---
title: "The HTML `audio` tag"
seotitle: "How to use the HTML audio tag"
date: 2019-08-06T07:00:00+02:00
description: "Discover the basics of working with the HTML `audio` tag"
tags: html
---

The `audio` tag allows you to embed audio content in your HTML pages.

This element can stream audio, maybe using a microphone via `getUserMedia()`, or it can play an audio source which you reference using the `src` attribute:

```html
<audio src="file.mp3" />
```

By default the browser does not show any controls for this element. Which means the audio will play only if set to autoplay (more on this later) and the user can't see how to stop it, or control the volume or move through the track.

To show the built-in controls, you can add the `controls` attribute:

```html
<audio src="file.mp3" controls />
```

Controls can have a custom skin.

You can specify the MIME type of the audio file using the `type` attribute. If not set, the browser will try to automatically determine it:

```html
<audio src="file.mp3" controls type="audio/mpeg" />
```

An audio file by default does not play automatically. Add the `autoplay` attribute to play the audio automatically:

```html
<audio src="file.mp3" controls autoplay />
```

> Note: mobile browsers don't allow autoplay

The `loop` attribute restarts the audio playing at 0:00 if set, otherwise if not present the audio stops at the end of the file:

```html
<audio src="file.mp3" controls autoplay loop />
```

You can also play an audio file muted using the `muted` attribute (not really sure what's the usefulness of this):

```html
<audio src="file.mp3" controls autoplay loop muted />
```

Using JavaScript you can listen for various events happening on an `audio` element, the most basic of which are:

- `play` when the file starts playing
- `pause` when the audio playing was paused
- `playing` when the audio is resumed from a pause
- `ended`	when the end of the audio file was reached
