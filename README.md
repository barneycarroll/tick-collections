# tick-collections

`TickMap` &amp; `TickSet` are subclasses of `Map` and `Set` whose contents are cleared every tick. Useful for eg memoization based on highly volatile data.

Their interfaces are identical to the classes they extend. Their only practical difference is to schedule an immediate `clear` whenever they receive state, such that they will be empty again at the next tick.

### Install

#### [from npm](https://www.npmjs.com/package/tick-collections)

```sh
npm i tick-collections
```

#### or grab the UMD module from a CDN

```html
<script src="https://cdn.rawgit.com/barneycarroll/tick-collections/1.0.2/umd.js"></script>
```

### Import

#### as ES6 modules

```javascript
import { TickMap } from 'tick-collections'
```

The NPM package caters for automatic ES6 module resolution via `jsnext:main` &amp; `module`. If you're not using a compliant ES6 module resolver (Rollup or Webpack, at the time of writing), simply point to the ES6 source file explicitly: `import { TickMap } from 'tick-collections/es6'`.

#### or using your favourite UMD method

```javascript
const { Map } = require( 'tick-collections' ) // CommonJS!

define( [ 'tick-collections' ], ( { Set } ) => { /**/ } ) // AMD!

true === ( window.Map === Map ) // Browser!
```

This package depends upon compliant native implementations of `class`, `Map` & `Set` - without `class` extension, neither native or any of the popular collection shims can be robustly or uniformly patched. `Promise.resolve` is used internally to clear collections on subsequent ticks of state being set - the internals have no opinion on whether that's a shim or not but obviously if you cannot depend on a runtime guarantee of next tick clearing if the runtime is incapable of reliably queuing tasks to execute in the next tick ;)
