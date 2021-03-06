# `dlv(obj, keypath)` [![NPM](https://img.shields.io/npm/v/dlv.svg)](https://npmjs.com/package/dlv) [![Build](https://travis-ci.org/developit/dlv.svg?branch=master)](https://travis-ci.org/developit/dlv)

> Safely get a dot-notated path within a nested object, with ability to return a default if the full key path does not exist or the value is undefined

### Why?

Smallest possible implementation: only **128 bytes.**

You could write this yourself, but then you'd have to write [tests].

Supports ES Modules, CommonJS and globals.

### Installation

`npm install --save dlv`


### Usage

`delve(object, keypath, [default])`

```js
import delve from 'dlv';

let obj = {
	a: {
		b: {
			c: 1
			d: undefined
			e: null
		}
	}
};

//use string dot notation for keys
delve(obj, 'a.b.c') === 1;

//or use an array key
delve(obj, ['a', 'b', 'c']) === 1;

delve(obj, 'a.b') === obj.a.b;

//returns undefined if the full key path does not exist and no default is specified
delve(obj, 'a.b.c.f') === undefined;

//optional third parameter for default if the full key in path is missing
delve(obj, 'a.b.c.f', 'foo') === 'foo';

//or if the key exists but the value is undefined
delve(obj, 'a.b.c.d', 'foo') === 'foo';

//Non-truthy defined values are still returned if they exist at the full keypath
delve(obj, 'a.b.c.e', 'foo') === null;

//undefined obj or key returns undefined, unless a default is supplied
delve(undefined, 'a.b.c') === undefined;
delve(undefined, 'a.b.c', 'foo') === 'foo';
delve(obj, undefined, 'foo') === 'foo';
```

### License

MIT


[preact]: https://github.com/developit/preact
[tests]: https://github.com/developit/dlv/blob/master/test.js
