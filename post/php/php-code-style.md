---
title: "Modern PHP coding style guide"
date: 2014-09-18T13:53:51+02:00

---

The PSR-1 and PSR-2 coding standards define how code should look like.

PSR-1 is the basic coding standard for PHP.
PSR-2 is the coding style guide.

Prior to their definition one would copy a coding standard from one of the popular frameworks around, but now that PHP has an official coding standard, we should all aim to adhere to it.

## PSR-1 in a nutshell

- Files SHOULD either declare symbols (classes, functions, constants, etc.) or cause side-effects (e.g. generate output, change .ini settings, etc.) but SHOULD NOT do both
- Namespaces and classes MUST follow an “autoloading” PSR: [PSR-0, PSR-4]
- Class names MUST be declared in StudlyCaps
- Method names MUST be declared in camelCase

## PSR-2 in a nutshell

- Code MUST use 4 spaces for indenting, not tabs
- There MUST NOT be a hard limit on line length; the soft limit MUST be 120 characters; lines SHOULD be 80 characters or less.
- There MUST be one blank line after the namespace declaration, and there MUST be one blank line after the block of use declarations.
- Visibility MUST be declared on all properties and methods; abstract and final MUST be declared before the visibility; static MUST be declared after the visibility.
- Opening parentheses for control structures MUST NOT have a space after them, and closing parentheses for control structures MUST NOT have a space before.

## Enforcing standards

It's essential to know and understand the coding standards. Having your IDE or editor enforce it automatically is a big step towards complying with it.

### On PHPStorm

It's built-in. Go in Preferences -> Editor -> Code Style -> PHP, on the right click "Set from.." and choose "Predefined Style" -> "PSR1/PSR2"

### On Sublime Text

Use [sublime-phpfmt](https://packagecontrol.io/packages/phpfmt)