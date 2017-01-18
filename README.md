# How to JS

This document is about how I write JavaScript. Having programmed in ECMAScript and its variants (ActionScript) over many years, I've developed a rather idiosyncratic style. Programming tends to be more art than science, so this document might as well be about my art style.


## Introduction

JS was developed as a tiny scripting language to make web pages more dynamic, it is a strange twist of fate that it's being used for much more than that. Particularly, Node.js uses JS as a scripting language that calls `libuv`, the C library that makes the underlying system calls.

JS seems to be viable enough to use for high-level application development, and the best choice for writing shared code between web clients and servers.


## Programming Style

Most of my stylistic preferences can be statically checked, I have [my own lint rules](https://github.com/sapeien/eslint-config-boss) for that. I'd encourage people to discover their own preferences, there are no cons and only pros. After all, it is inconsequential how code is formatted anyways.

I think comments and more generally, [literate programming](https://en.wikipedia.org/wiki/Literate_programming) is a good idea. Prose is far more readable than code, anyone who says otherwise is a robot.

At a macro level, I try to write as little code as possible. [Code is a liability](http://wiki.c2.com/?SoftwareAsLiability). If there is a more laconic way to express the same thing, go for it.

### Prefer ECMAScript 5.1

This version of the specification seems to be the golden one, much like C89 was for C. It is syntax compatible with earlier versions unlike ES6, and it contains Object properties which were already part of the DOM API but not exposed in userland, so it is in a sense the most complete version. Some unnecessary introductions such as `Function.prototype.bind` and `Array.prototype` methods may be safely ignored.

### Prefer `require`, CommonJS style

Although ES6 introduces modules formally, they are not a backwards compatible change. Node.js will likely forever remain compatible with CommonJS, and standardized tooling such as [browserify](http://browserify.org/) works well enough, and is simple enough to implement on your own. By using `require` on nested paths, one can avoid the need for solutions seeking problems like *tree shaking* or *dead code elimination*.


## Asynchronous Behavior

Use callbacks while waiting for I/O in Node.js. This is the standard and is unlikely to change, sugar to wrap callbacks in Promises is a useless liability.

However, Promises in high-level interfaces are fine, callbacks are a lower-level approach. The performance cost could be compensated by using another language with a better abstraction, which is outside of the scope of this document.

Native ES6 Promise implementations tend to be not very performant, so use a userland implementation instead.


## Testing

All that is really needed for testing is a program that exits with exit code `0` if successful or any non-zero value in case of failure. I prefer formatting output with the [Test Anything Protocol](https://en.wikipedia.org/wiki/Test_Anything_Protocol) which has been around for longer than I have, and I've written a terse [test harness](https://github.com/sapeien/tapdance) which does just that.


## Utility Functions

There are tons of trivial `npm` modules that do something generic which could be written in a minute. Avoid them, they are more trouble than they're worth. The likelihood of the same utility re-used in multiple dependencies is negligible, and the savings in file size would be as well.


## Databases

Databases exist due to the physical differences between memory and disk. Whenever bulk storage or persistence is not needed, avoid databases entirely and just do everything in memory. When persistence and storage are needed, PostgreSQL is a good choice and has decades of development behind it.

IndexedDB is the one that works in the browser, it's backed by LevelDB in most implementations but its native API is garbage. It seems to have an asynchronous API but is actually blocking when run on the main thread, so an abstraction that uses Web Workers is needed. I've written [my own abstraction](https://github.com/fortunejs/fortune-indexeddb) on top of the native API.

Regardless of whether data is in disk or memory, database features such as relationships, referential integrity, transactions, and querying are often needed in real world applications, I've written [a database abstraction layer for that](http://fortune.js.org).


## DevOps

Any platform that is supported by Node.js should be all that is needed. I prefer [psy](https://github.com/substack/psy) for keeping Node.js processes running.

It's generally a good idea to cache dependencies locally so that deploying does not depend on remote servers being available, and using `npm shrinkwrap` for saving version information.


## Distributed Systems

See [fallacies of distributed computing](https://en.wikipedia.org/wiki/Fallacies_of_distributed_computing), it is best to avoid it altogether.

When it's absolutely necessary, there's plenty of viable options, ranging from in-memory databases, message queues, syncing algorithms that are all rather application specific.


## Web Servers

Just implement the listener function expected by Node.js without depending on frameworks. This is not only faster but also more reliable, and opens up alternative implementations and backends such as HTTP/2 and uWS.


## Static Typing

Most optimizing JS runtimes such as V8 which Node.js uses by default optimize for the same types being passed into functions. It is also generally a good idea to check the types of arguments for public interfaces.


## Front-End

Using the native DOM API is the fastest and simplest way to make web pages more interactive, although its ergonomics are lacking. I wrote [Simulacra.js](http://simulacra.js.org) to make the native DOM more usable.

I avoid styling anything in JS, it should be in the domain of CSS.


## License

[WTFPL](http://www.wtfpl.net/)
