---
title: "Properly document PHP code"
date: 2014-08-18T13:53:51+02:00

---

> Warning: this post is old and might not reflect the current state of the art

Documentation is key to any successful project. Here's a quick introduction to what you should document, and how.

## Classes

Start every class with

```
/**
 * Class description
 *
 * @author  Your organization or personal name
 * @license MIT (or other licence)
 */
```

## Properties

Document every property with

```
/**
 * Property brief description
 *
 * @var type
 */
```

## Methods

Document every method with

```
/**
 * Method brief description
 *
 * Method longer description and help
 */
```

If you method accepts parameters, add them

```
 * @param  type $param1 The param1 description
 * @param  type $param2 The param2 description
```

If your method returns something, describe the return value

```
 * @return $this
```

If your method throws an exception, describe the exception


```
 * @throws \Exception
```

## Code

Code inside methods needs to be documented if needed.

Dot not document what the code is doing, document what the code should do.
