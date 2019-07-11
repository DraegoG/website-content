---
title: The Heroku Redis Maxmemory Policy
date: 2017-12-03T09:07:09+02:00

---

Heroku offers a great Redis addon, which provides 25MB of memory for free.

This amount of storage can be easily filled with just a few thousands items, depending on what you're storing.

Heroku has a configuration option called **maxmemory-policy** that determines how the system will behave when the Redis database memory is filled.

By default this property is set to `noeviction`, which means Redis will raise an error when trying to store more data.

This is done so you realize what is happening, and once you find out that you can change this behavior, it's time to determine *how*.

The various behaviors are provided by Redis itself, and they are:

- `noeviction`: return errors when the memory limit was reached and the client is trying to execute commands that could result in more memory to be used (most write commands, but DEL and a few more exceptions).
- `allkeys-lru`: evict keys by trying to remove the less recently used (LRU) keys first, in order to make space for the new data added.
- `volatile-lru`: evict keys by trying to remove the less recently used (LRU) keys first, but only among keys that have an expire set, in order to make space for the new data added.
- `allkeys-random`: evict keys randomly in order to make space for the new data added.
- `volatile-random`: evict keys randomly in order to make space for the new data added, but only evict keys with an expire set.
- `volatile-ttl`: evict keys with an expire set, and try to evict keys with a shorter time to live (TTL) first, in order to make space for the new data added.

It's up to you to find the best case for your needs. Once you do have a candidate, you can apply the change using the Heroku CLI, for example:

```
heroku redis:maxmemory YOUR_REDIS_INSTANCE_NAME --policy volatile-lru
```

