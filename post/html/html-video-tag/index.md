---
title: "The HTML `video` tag"
seotitle: "How to use the HTML video tag"
date: 2019-08-05T07:00:00+02:00
description: "Discover the basics of working with the HTML `video` tag"
tags: html
---

The `video` tag allows you to embed audio content in your HTML pages.

This element can stream video, using a webcam via `getUserMedia()` or **WebRTC**, or it can play a video source which you reference using the `src` attribute:

```html
<video src="file.mp4" />
```

By default the browser does not show any controls for this element, just the video.

Which means the audio will play only if set to autoplay (more on this later) and the user can't see how to stop it, pause it, control the volume or skip at a specific position in the video.

To show the built-in controls, you can add the `controls` attribute:

```html
<video src="file.mp4" controls />
```

Controls can have a custom skin.

You can specify the MIME type of the video file using the `type` attribute. If not set, the browser will try to automatically determine it:

```html
<video src="file.mp4" controls type="video/mp4" />
```

A video file by default does not play automatically. Add the `autoplay` attribute to play the audio automatically:

```html
<video src="file.mp4" controls autoplay />
```

Some browsers also require the `muted` attribute to autoplay. The video autoplays only if muted:

```html
<audio src="file.mp3" controls autoplay muted />
```

The `loop` attribute restarts the video playing at 0:00 if set, otherwise if not present the video stops at the end of the file:

```html
<video src="file.mp4" controls autoplay loop />
```

You can set an image to be the poster image:

```html
<video src="file.mp4" poster="picture.png" />
```

If not present, the browser will display the first frame of the video as soon as it's available.

You can set the `width` and `height` attributes to set the space that the element will take, so that the browser can account for it and it does not change the layout when it's finally loaded.
It takes a numeric value, expressed in pixels.

Using JavaScript you can listen for various events happening on an `video` element, the most basic of which are:

- `play` when the file starts playing
- `pause` when the video was paused
- `playing` when the video is resumed from a pause
- `ended`	when the end of the video file was reached
