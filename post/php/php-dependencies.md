---
title: "Managing PHP Dependencies using Composer"
date: 2014-07-16T13:53:51+02:00

---

> Warning: this post is old and might not reflect the current state of the art

[Composer](https://getcomposer.org) has proven to be the best modern dependency management solution for PHP.

Composer filled a need and now is on the same level as what [npm](/npm/) is for [Node.js](/nodejs/) packages.

Combined with [Packagist](https://packagist.org), the official repository for Composer packages, it's a utility you cannot avoid using.

## Installing Composer on OSX / Linux

`curl -sS https://getcomposer.org/installer | php`

and

`mv composer.phar /usr/local/bin/composer`

[More details on installation](https://getcomposer.org/doc/00-intro.md#installation-linux-unix-osx)

## Using Composer

Initialize Composer by typing

```
composer init
```

in the root of the project. Follow the instructions, you'll end up with a `composer.json` file. This is the file that contains all the project dependencies.

Now type

```
composer install
```

This command will download all the dependencies in the `vendor` folder and create a `composer.lock` file.

The `vendor` folder contains the packages folders, plus an `autoload.php` file and the `composer` folder, which are internal Composer files.

To include the dependencies include `vendor/autoload.php` in your PHP main file:

```
require 'vendor/autoload.php'
```

and all will just work.

## Adding dependencies

To add more dependencies to the project type

```
composer require packagename:1.0
```

Example:

```
composer require filp/whoops:2.0
```

## Updating dependencies

Run

```
composer update
```

Composer will search for updates for the packages you specified, taking into consideration any versions limit you added, and will update the `composer.lock` file.

## Package versions

Most used version formats:

- "1.0": will install that precise version
- "~1.0":  will install any update to 1.0, 1.0.1, 1.0.20 but will not install version 1.1 and later versions.

## composer.lock

Whenever you update the installed dependencies running `composer install` or `composer update`, the `composer.lock` file will be updated to reflect it. So if you add this file to the repository everyone that downloads the project and runs `composer install` will get the exact same versions you installed, even if a newer one satisfying the version limits in `composer.json` is available.

They need to run `composer update` to get the latest releases available.

## Package updates notifications

Add your project's `composer.json` and `composer.lock` to [VersionEye](http://versioneye.com) to be notified via email when your dependencies are updated, so you can update them in your project.

## Security issues in your dependencies

Add your `composer.lock` to [Security Advisories Checker](https://security.symfony.com/)

## A note on PEAR

PEAR was the older widely used package manager. The major disadvantage over Composer is that dependencies are installed globally, so there is no version fine-tuning allowed for projects. Once you update a PEAR package, every project on the system will use the new version, and depending on your scenario, this might be a problem.
