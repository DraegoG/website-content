---
title: "Why Go is a powerful language to learn as a PHP developer"
date: 2017-08-22T10:46:52+02:00
tags: go
---

I’ve been programming using PHP professionally since 10 years now. After my Computer Engineering degree, all I knew was that Java was not my piece of cake any more (after 6+ years using it for personal and academic projects), I wanted a _much_ simpler stack and I figured out that a quick way to market myself as an independent developer was getting into the rising PHP CMS market.

Over the years PHP has changed _a lot_ and while many people like to bash or criticize it, many do it based on very old and very little experience. Modern PHP, especially if you have the luxury to use PHP 7 types and leave behind PHP 5.x, is very nice to work with, and of course PHP has the advantage of being, for some reason, the language that you can deploy nearly everywhere, which is why many CMS are built in PHP, and why they are so successful _because_ they are PHP-based ([Grav](https://getgrav.org) included).

Of course PHP is just one tool, and recently I've been delving into Go head first.

Compared to PHP, Go is a completely different language and environment.

This is not a rant or an article aimed at moving you away from PHP, but rather to introduce you, PHP developer, at why Go is a good language to learn as a complementary tool.

## First things first: what is Go?

Go is an imperative, object-oriented programming language designed at Google 10 years ago.

The combined knowledge of the founding members, and the original philosophy in creating the best language for the needs they had, led to Go.

Go is a compiled language, statically typed, with garbage collection and concurrent programming features built-in.

## It’s nothing new

The way Go goes about innovating is quite interesting. It completely ignores the hype about what supposed new features a modern language should have, and what other programming languages provide, but instead cherry-pick core concept from battle-tested languages, aggregating decades of programming experience into a beautiful tool to use.

> The task of the programming language designer is consolidation not innovation -- Hoare, 1973

Go has many unique features, of course, it’s not just a mashup language. Go introduced **goroutines**, which are an amazing way to handle concurrency. Go introduced **defer**, a great way to execute something when the outer function returns (now added into Swift, as well).

Go was the first language to introduce a formatter in the standard tools. And the ability to compile for other platforms without friction, plus many more “new” things.

Go has strong roots. A beautiful presentation at GopherCon 2015 by Robert Griesemer illustrates it: Go merges many principles of both C and Oberon-2, which is a language coming from the Pascal family. Both these languages originate from Algol 60, which was introduced in 1960.

So the next time [someone ask why Go looks like a language from 20 years ago](https://www.quora.com/Why-has-Google-elected-to-rewind-the-software-engineering-clock-at-least-20-years-with-the-Go-programming-language-Same-goes-for-every-corporate-language), you can just as well answer that it actually has over 60 years of experience under its belt.
As Robert Griesemer once said, it takes 10 years for a programming language to become mainstream.

Go is just getting started, which is pretty exciting thinking about its future and what people can build with it!

## Go is complementary to PHP

If you ever used Ruby or Python in addition to PHP, you might have realized that they more or less boil down to a different version of PHP, if you remove fanboyism and personal preferences from the equation, as all are interpreted, loosely typed languages.

One could switch to Ruby to PHP and Python and do the same things. The only "web language" that differs quite substantially is [JavaScript](/javascript/), which is different because of the non-blocking model (but that’s been migrated to other languages, including PHP as well through libraries) and because it’s the only language currently running natively in the browser, which gives it an enourmous advantage. Also, it's a much more wild ecosystem of uncontrolled executing environments, all different in possibly subtle ways.

Go on the other hand is a completely different beast. It’s a system language, like C. And unlike dynamic languages, Go is fast.

PHP is built in C, and you can write and run PHP C extensions, so the concept of a system language should not be _that_ alien to you.

Go is capable of replacing your web stack, and there are web frameworks available for that, making it easy, but PHP still has its place, especially when prototyping and you still don't know what part of your code will need heavy optimization, and if your code will be really used after all.

So, when should you use Go? When you’re using PHP but PHP is not really the best tool for the job. If PHP is consuming too much memory or resources for a particular piece of functionality, and a highly optimized Go program will perform much better. Simple as that. PHP 7 has been amazing at improving the PHP performance. That was a free gift. But when you need to process millions of database entries, or fetch Gigabytes of data from an API with a long running process, PHP might not be the right tool.

I’ve relied on [Node.js](/nodejs/) for quite a few years to solve this problem, but as I got to know Go, so far anything that I come up with Go is a far simpler and better solution.

And it does not stop there, of course. With Go you build cross-platform, concurrent applications in a breeze, and this is very different from PHP web development, way more challenging, but also — personally speaking — more interesting, and it could open up for you many rewarding jobs.

So, as a PHP developer you could start handing off demanding tasks to Go, while becoming skilled at it will surely enrich your career choices.

## Why Go and not C C++ or Java?

Any language has its place. Surely Go can’t beat C and C++ performances. There are many benchmarks you can find.

Go sits in the middle between those 2 mainstream and historic languages and dynamic languages: you want more performance than what you can get from an interpreted language, but you’re not ready or not willing to use C or C++, which are faster but they are too low level, and you’d need to manually manage memory, and it would take way more time to develop.
Go fits that place.

For a heavily optimized piece of code — C or C++ might be a better solution, if you’re highly proficient with them. I could say the same for Assembly.

In comparison to Java, it’s a completely different situation. Java requires a lot of overhead in terms of environment, while Go programs are a single file, light, portable and native.

And we’re probably comparing apples to oranges, you’d never use Go where you use Java, and the opposite stands true.

## Go is simple at heart

(And remember: simple does not mean easy)
Avoiding feature creep was clearly one of the goals of the designers of Go. Legendary Ken Thompson, one of the 3 original designers of Go, also creator of UNIX and the B language (among many other things), once said

> When the three of us [Thompson, Rob Pike, and Robert Griesemer] got started, it was pure research. The three of us got together and decided that we hated C++. [laughter] … [Returning to Go,] we started off with the idea that all three of us had to be talked into every feature in the language, so there was no extraneous garbage put into the language for any reason.

This resulted in a language that is amazingly simple for any experienced developer that’s been coding in any language.

Java, C++, C, C#, Erlang, JavaScript, Swift, almost all modern programming languages are way more complex than Go.

And here I mean complex to use for the programmer, complex to read, complex to become a master. Inside, Go hides all the complexity and exposes a simple API. Not only Go has garbage collection, but there is no exposed memory management functionality at all.

Just think that PHP has 67 keywords, while Go has 25.

> The key point here is our programmers are Googlers, they’re not researchers. They’re typically, fairly young, fresh out of school, probably learned Java, maybe learned C or C++, probably learned Python. They’re not capable of understanding a brilliant language but we want to use them to build good software. So, the language that we give them has to be easy for them to understand and easy to adopt. — Rob Pike

This is core to the Go philosophy, and explains why Go choses to avoid implementing features (avoiding feature creep), and why many concepts of functional programming are left out, as they are complex to reason about, opening debates.
Pure functional programming is too much away from the machine concepts to be relevant to Go, which is an imperative language at heart.

That said, Go has many concepts of functional programming implemented, like first-class functions (allowing functions to be assigned to variables), closures, recursion.

But compared to PHP or JS, you don’t have functional operations like map, reduce or filter, you must rely on loops. Why? Because those operations are inefficient, and Go must find a balance.

Speaking of things missing, there are no exceptions to handle errors. There are no classes (even though it’s object-oriented, with structs with associated methods, forcing [composition over inheritance](https://en.wikipedia.org/wiki/Composition_over_inheritance) — if you have knowledge of JavaScript’s prototype object implementation, this will be familiar, but very different), no generics (although PHP does not have them too), and [here is why](https://youtu.be/0ReKdcpNyQg?t=1520).

[Less is more](https://gettingreal.37signals.com/ch10_Less_Software.php), or (even better!) [less is exponentially more](http://commandcenter.blogspot.com/2012/06/less-is-exponentially-more.html).

> [The “secret” to good software design wasn’t in knowing what to put into the code; it was in knowing what to leave OUT! It was in recognizing where the hard-spots and soft-spots were, and knowing where to leave space/room rather than trying to cram in more design](http://bradapp.blogspot.it/2005/02/there-is-no-code-that-is-more-flexible.html)

There’s just one way to write a loop: `for`. Forget `while` and `do — while` and `foreach` (something more?).

> [[…] what makes Go successful is what has been left out of the language, just as much as what has been included.](http://dave.cheney.net/2015/03/08/simplicity-and-collaboration)

The ability to return multiple values from a function avoids lot of tricks (the simplest example is returning an array containing 2 values, and having to extract them without knowing the exact type passed).

Simplicity is inherited by the tooling. [gofix automatically fixes breaking API changes in new Go releases](https://blog.golang.org/introducing-gofix).

And Go is simple by design, and will always stay simple.

[As Rob Pike says](https://youtu.be/rFejpH_tAHM?t=64), many other languages are copying features from each other, losing their unique aspects (think about JavaScript introducing the classes syntax to please Java and PHP developers) and they are all ideally converging to a conceptually unique language.

Go does not compete in features. This reminds me of [this Getting Real article](https://gettingreal.37signals.com/ch02_Build_Less.php).

## Beware: Go is polarizing

Go has lots of fans, and lots of haters too. As a PHP developer I’m sure you developed a thick skin on this kind of flame wars, and we can quickly move on to the next point. It’s very popular and developers have strong opinions.

> [No matter what trade-offs you make, there will always be criticisms, because no programming language can be perfect](https://medium.com/@richardeng/the-little-language-that-could-61eaa62b5e0a)

Go solves a problem, beautifully. And you don’t need to be a genius to start using it, although this might hurt your feelings.

## Go is very opinionated and has clear conventions

One of the first things you’ll notice about Go is that almost all the code you can find looks almost the same.

This is because Go has clear and forced conventions. The built-in tooling provides 2 commands related to conventions (**gofmt** and **golint**, with the first auto-formatting code, and the second just printing warnings), and they can check if your code complies, and even automatically adjusting your style to the Go guidelines.

This is different than JS [ESLint](/eslint/) / JSHint, as those tools are team-wide application. As in everything JS, you can customize anything in the preferences. `gofmt` is one, no configuration, that-is-the-way-to-go-style.

This is great to provide cnsistency on your own code (code you wrote 5 years ago in PHP or JavaScript might be **very** different from your current conventions and preferences) and on code that _everyone_ distributes.

Imagine no more internal team discussions on the best code styling, imagine all PRs to your open source project formatted and linted in the same way. Spaces vs0 tabs, save mind cycles - it’s tabs. Braces on same line or in the next? One the same line, always (there’s a reason for this, and it’s to allow to omit semicolons).

Go raises a compile error if a variable or import is not used, preventing your programs to accumulate garbage over time.

Naming conventions are so important that the access modifiers has been totally removed from the equation. Lowercase variable? Private. Capitalized variable? Public. Simple as that, a simple conventions removes tons of useless screen space usage, plus it’s immediately understandable.

Comments serve a special need, and you write them in a special syntax so your package can be inspected using `go doc` and you have all the documentation you need without searching for it on Google.

`go get` is at your disposal, built-in (which is great for open source and distribution).
Although PHPland is much more advanced in my opinion in terms of dependencies management.

PHPUnit/Codeception? No need, `go test` is already there for your `*_test.go` files.

## It makes you a better programmer

If you’re coming from PHP, learning Go will make you think in a different, new way. It will make you a better programmer much like learning any different language will: it introduces you to new concepts. If it feels strange and alien, it’s a good sign you’re learning and growing as a developer.

To start with, Go is compiled instead of interpreted. Completely different workflow and deployment.

If you don’t have experience with strong typing, that’s a paradigm change. PHP 7 comes with typing checking, and it’s a great help if you don’t have to support older PHP versions. Go is strongly typed. Many if not all types issues are solved at compile time.

Go is amazingly simple, designed to be simple, and being a Go developer means recognizing this simplicity and taking advantage of it, and not try to write Java-like Go, but embrace it.

And by simple I don't mean Go is a toy language, it certainly isn't, and it's not a language I'd introduce someone to coding.

By simplicity I mean more **minimalism** and **no-fluff**.

When a language offers you many ways to do the same thing, you are forced to think which is best, distracting from the problem you’re trying to solve.

## You can run Go code from PHP

So one way I suggest to start with is to code some heavy routine or long-running piece of code that consumes too much memory as a Go service.

There [are](https://github.com/arnaud-lb/php-go) [many](https://github.com/kitech/php-go) [ways](https://github.com/deuill/go-php) to directly call Go programs from PHP, but you might also choose to implement a [service queue through ZeroMQ](https://stackoverflow.com/a/37526304/205039), or access a long-lived go program through exposing an API endpoint through a reverse proxy. You have many options.

## Go’s special weapon: concurrency

PHP-FPM is known to handle concurrent requests very well, spawning a new process that execute the actual PHP code for each user. And usually in a web application the database is the bottleneck. But what about long-running processes (something that you don’t really want to build in PHP), or when you need to start a heavy computational loop within a PHP request, where you need to run tens of thousands of concurrent processes?

PHP has threads support, so it can do concurrent processing, but while PHP (or even C and others) can do concurrency using the help of libraries external to the language, Go is **designed** with built-in concurrent programming, and provides native ways to communicate between goroutines.

Threads are heavy, compared to **goroutines**. A system could support 10k threads, and the same system could support millions of goroutines, because of the internal implementation of the memory consumption of goroutines is much lighter, like in Java or Erlang.

So even if you don’t need millions of concurrent requests, the performance gains are clear.

Plus, it’s very easy to digest goroutines and understand what the code does from a quick look.

No need to extend classes or include special extensions, which might not be always available (this effectively limits the extent that we can use PHP concurrency for self-installed distributed code)

Just type `go someFunction()` and that function will be executed in a goroutine.

## Conclusion

If you’re a PHP developer new to Go, I hope you’re now curios about this tool, and thinking about where it could have been useful, or if it’s the right choice for you.

If you’re a programmer that prefers simplicity over complexity, favour direct and readable code over abstractions, then I’m sure you’ll find Go really interesting.
