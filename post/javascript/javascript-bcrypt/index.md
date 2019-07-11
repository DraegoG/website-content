---
title: "How to use the JavaScript bcrypt library"
date: 2019-07-28T07:00:00+02:00
description: "Find out how to hash and check passwords in JavaScript with the bcrypt library"
tags: js
---

The bcrypt npm package is one of the most used packages to work with passwords in JavaScript.

This is security 101, but it's worth mentioning for new developers: you never store a password in plain text in the database or in any other place. You just don't.

What you do instead is, you generate a hash from the password, and you store that.

In this way:

```js
import bcrypt from 'bcrypt'
// or
// const bcrypt = require('bcrypt')

const password = 'oe3im3io2r3o2'
const rounds = 10

bcrypt.hash(password, rounds, (err, hash) => {
	if (err) {
    console.error(err)
    return
  }
  console.log(hash)
})
```

You pass a number as second argument and the bigger that is, the more secure the hash is. But also the longer it takes to generate it.

The library README tells us that on a 2GHz core we can generate:

```
rounds=8 : ~40 hashes/sec
rounds=9 : ~20 hashes/sec
rounds=10: ~10 hashes/sec
rounds=11: ~5  hashes/sec
rounds=12: 2-3 hashes/sec
rounds=13: ~1 sec/hash
rounds=14: ~1.5 sec/hash
rounds=15: ~3 sec/hash
rounds=25: ~1 hour/hash
rounds=31: 2-3 days/hash
```

If you run `bcrypt.hash()` multiple times, the result will keep changing. This is key because there is no way to reconstruct the original password from a hash.

Given the same password and a hash it's possible to find out if the hash was built from that password, using the `bcrypt.compare()` function:

```js
bcrypt.compare(password, hash, (err, res) => {
  if (err) {
    console.error(err)
    return
  }
  console.log(res) //true or false
})
```

If so, the password matches the hash and for example we can let a user log in successfully.

You can use the `bcrypt` library with its promise-based API too, instead of callbacks:

```js
const hashPassword = async () => {
  const hash = await bcrypt.hash(password, rounds)
  console.log(hash)
  console.log(await bcrypt.compare(password, hash))
}

hashPassword()
```

Check a couple examples [in this Glitch](https://glitch.com/~flavio-bcrypt-example):

<!-- Copy and Paste Me -->
<div class="glitch-embed-wrap" style="height: 420px; width: 100%;">
  <iframe
    allow="geolocation; microphone; camera; midi; vr; encrypted-media"
    src="https://glitch.com/embed/#!/embed/flavio-bcrypt-example?path=app.js&previewSize=0"
    alt="flavio-bcrypt-example on Glitch"
    style="height: 100%; width: 100%; border: 0;">
  </iframe>
</div>