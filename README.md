# `asyncro` [![NPM](https://img.shields.io/npm/v/asyncro.svg?style=flat)](https://www.npmjs.org/package/asyncro) [![travis-ci](https://travis-ci.org/developit/asyncro.svg?branch=master)](https://travis-ci.org/developit/asyncro)

The same `map()`, `reduce()` & `filter()` you know and love, but with async iterator functions!

Do `fetch()` networking in loops, resolve Promises, anything async goes. Performance-friendly _by default_.

**Here's what it looks like:**

<img src="https://i.imgur.com/GcykVyN.png" width="404" alt="Asyncro Example">

---

## What's in the Box

<img src="https://i.imgur.com/yiiq6Gx.png" width="275" alt="Asyncro Example 2">


---

<a target='_blank' rel='nofollow' href='https://app.codesponsor.io/link/WbARjbDRQz5y3N6VBEMPU4LW/developit/asyncro'>
  <img alt='Sponsor' width='888' height='68' src='https://app.codesponsor.io/embed/WbARjbDRQz5y3N6VBEMPU4LW/developit/asyncro.svg' />
</a>


## Installation

```sh
npm install --save asyncro
```

## Import and Usage Example

```js
import { map } from 'asyncro';

async function example() {
	return await map(
		['foo', 'bar', 'baz'],
		async name => fetch('./'+name)
	)
}
```

## API

<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

#### reduce

Invoke an async reducer function on each item in the given Array,
where the reducer transforms an accumulator value based on each item iterated over.
**Note:** because `reduce()` is order-sensitive, iteration is sequential.

> This is an asynchronous version of `Array.prototype.reduce()`

**Parameters**

-   `array` **[Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)** The Array to reduce
-   `reducer` **[Function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)** Async function, gets passed `(accumulator, value, index, array)` and returns a new value for `accumulator`
-   `accumulator` **\[Any]** Optional initial accumulator value

**Examples**

```javascript
await reduce(
	['/foo', '/bar', '/baz'],
	async (accumulator, value) => {
		accumulator[v] = await fetch(value);
		return accumulator;
	},
	{}
);
```

Returns **any** final `accumulator` value

#### map

Invoke an async transform function on each item in the given Array **in parallel**,
returning the resulting Array of mapped/transformed items.

> This is an asynchronous, parallelized version of `Array.prototype.map()`.

**Parameters**

-   `array` **[Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)** The Array to map over
-   `mapper` **[Function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)** Async function, gets passed `(value, index, array)`, returns the new value.

**Examples**

```javascript
await map(
	['foo', 'baz'],
	async v => await fetch(v)
)
```

Returns **[Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)** resulting mapped/transformed values.

#### filter

Invoke an async filter function on each item in the given Array **in parallel**,
returning an Array of values for which the filter function returned a truthy value.

> This is an asynchronous, parallelized version of `Array.prototype.filter()`.

**Parameters**

-   `array` **[Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)** The Array to filter
-   `filterer` **[Function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)** Async function. Gets passed `(value, index, array)`, returns true to keep the value in the resulting filtered Array.

**Examples**

```javascript
await filter(
	['foo', 'baz'],
	async v => (await fetch(v)).ok
)
```

Returns **[Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)** resulting filtered values

#### parallel

Invoke all async functions in an Array or Object **in parallel**, returning the result.

**Parameters**

-   `list` **([Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;[Function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)> | [Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)&lt;[Function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)>)** Array/Object with values that are async functions to invoke.

**Examples**

```javascript
await parallel([
	async () => await fetch('foo'),
	async () => await fetch('baz')
])
```

Returns **([Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) \| [Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object))** same structure as `list` input, but with values now resolved.

#### series

Invoke all async functions in an Array or Object **sequentially**, returning the result.

**Parameters**

-   `list` **([Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;[Function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)> | [Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)&lt;[Function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)>)** Array/Object with values that are async functions to invoke.

**Examples**

```javascript
await series([
	async () => await fetch('foo'),
	async () => await fetch('baz')
])
```

Returns **([Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) \| [Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object))** same structure as `list` input, but with values now resolved.
