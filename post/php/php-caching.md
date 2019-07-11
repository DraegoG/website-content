---
title: "Basics of PHP Caching"
date: 2014-08-18T13:53:51+02:00

---

> Warning: this post is old and might not reflect the current state of the art

PHP is pretty fast, and with the release of PHP 7 it's dramatically faster, sometimes averaging to 2x speedier than PHP 5.5. HHVM is sometimes even faster. That said, caching is essential to the speed of a PHP application.

## OPCache

OPCache is a special caching mechanism that stores precompiled versions of the PHP files.
When executed, a PHP file is compiled to bytecode and once this process is done, the bytecode is executed.

99.9% of the times the opcodes are the same for days, as a file might not change for months, and still PHP by default recompiles it every time.

To improve this comes OPCache. OPCache improves the PHP performance by storing precompiled script bytecode in shared memory, removing the need for PHP to load and parse scripts on each request.

Since PHP 5.5 it's bundled in the core, and it's something that just needs to be installed to give us an enourmous speed improvement that it's nonsense not to use it.

[OPCache documentation](https://secure.php.net/book.opcache)

## APCu

APCu is the old APC without the opcode cache, which is now built provided officially by OPCache.
It is a user cache, which means it must be explicitly used by your PHP code to take advantage of it, while OPCache does all the work just after being installed.

When you perform an expensive operation, like reading a file or fetch a network resource, you can store the result in the user cache to speed up a later request of the same object.

The only downside of APCu is that it's local to the machine it runs on, AND local to the PHP process and system. This means that if you use PHP as a FastCGI process (e.g. Nginx and php-fpm) every PHP process will have its own cache.

Unless you expect to run your application on multiple servers or processes, this will be fine. Otherwise, Memcached and Redis can be a good solution.

## Using APCu

```php
<?php
function getData() {
    $data = apc_fetch('some_data');
    if ($data === false) {
        $data = $this->getSomeData();
        apc_add('some_data', $data);
    }
    return $data;
}
?>
```

[APCu documentation](https://secure.php.net/apcu)

## APC, XCache, Memcached, Redis and others

Since OPcache is now built-in, and the key value cache is now part of APCu, APC is no longer relevant.
XCache is not recommended any more, use APCu instead.
Memcached and Redis can be an alternative to APCu, just less convenient on a standalone system as they must be setup separately and provide no real advantage over APCu, BUT convenient if you run multiple PHP processes or setup a network of systems as they all can rely on a central cache location.
