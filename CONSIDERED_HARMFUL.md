# JavaScript Considered Harmful

Like all code, the best JavaScript is as little JavaScript as possible. But if you must use JS, this list will inform what to avoid.

| Package | Reason | Less Harmful Alternatives |
|:--------|:-------|:--------------------------|
| Lodash, Underscore, Ramda | Functional programming is all the hype, but comes with overhead even in optimal cases. | `for` loop, `while` loop. |
| Grunt, Gulp | Reinventing the wheel with JavaScript. What could go wrong? | Shell scripts, GNU Make, vanilla Node.js scripts. |
| WebPack, Rollup | Unnecessary configuration and complexity. | Browserify + CommonJS. |
| Babel, TypeScript | Trivial additions to the language that are more trouble than they're worth. | Plain ES5, Sweet.js, ParenScript, CoffeeScript. |
| Express, Koa, Hapi, Restify, Node.js frameworks | Killing performance and adding incidental complexity. | libr3, RegExp, URI templates, implement the request listener function yourself. |
| React, Angular, browser frameworks | Skinner boxes that make sure that you stay within the limits of the box. | Simulacra.js, DOM API. |
| Redux | Marketing fluff turned into a few trivial lines of code. | This package is so superfluous that it needs no alternative. |
| RxJS | Avoid these corporate snake oil salesmen. | No alternative is needed. |
| jQuery | Obsolete fixes for obsolete browsers. | Simulacra.js, DOM API. |
| Ava, Mocha, Jasmine, test frameworks | Use these if you want test code to look as superfluous as possible. | Tape, Tapdance, TAP. |
| Socket.io | Forces you to use a proprietary application protocol, extremely slow. | uWebSocket, ws. |
| PostCSS, inline CSS generators | Unnecessary build tooling. | Plain CSS. |
| Async | Needless complexity. | Callbacks, Promises. |
| Request, sugary HTTP wrappers | Useless bloat. | Node.js `http.request`, `XmlHttpRequest`. |
| Moment | Useless bloat. | Native `Date` object. |
| Mongoose, Bookshelf, ORMs | ORMs are one of the worst abstractions one could possibly use. | Fortune.js, database drivers. |
