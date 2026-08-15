<!--

@license Apache-2.0

Copyright (c) 2026 The Stdlib Authors.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

-->


<details>
  <summary>
    About stdlib...
  </summary>
  <p>We believe in a future in which the web is a preferred environment for numerical computation. To help realize this future, we've built stdlib. stdlib is a standard library, with an emphasis on numerical and scientific computation, written in JavaScript (and C) for execution in browsers and in Node.js.</p>
  <p>The library is fully decomposable, being architected in such a way that you can swap out and mix and match APIs and functionality to cater to your exact preferences and use cases.</p>
  <p>When you use stdlib, you can be absolutely certain that you are using the most thorough, rigorous, well-written, studied, documented, tested, measured, and high-quality code out there.</p>
  <p>To join us in bringing numerical computing to the web, get started by checking us out on <a href="https://github.com/stdlib-js/stdlib">GitHub</a>, and please consider <a href="https://opencollective.com/stdlib">financially supporting stdlib</a>. We greatly appreciate your continued support!</p>
</details>

# gcircshift

[![NPM version][npm-image]][npm-url] [![Build Status][test-image]][test-url] [![Coverage Status][coverage-image]][coverage-url] <!-- [![dependencies][dependencies-image]][dependencies-url] -->

> Circularly shift the elements of a strided array by a specified number of positions.



<section class="usage">

## Usage

```javascript
import gcircshift from 'https://cdn.jsdelivr.net/gh/stdlib-js/blas-ext-base-gcircshift@esm/index.mjs';
```

You can also import the following named exports from the package:

```javascript
import { ndarray } from 'https://cdn.jsdelivr.net/gh/stdlib-js/blas-ext-base-gcircshift@esm/index.mjs';
```

#### gcircshift( N, k, x, strideX )

Circularly shifts the elements of a strided array by a specified number of positions.

```javascript
var x = [ 1.0, 2.0, 3.0, 4.0, 5.0 ];

gcircshift( x.length, 2, x, 1 );
// x => [ 4.0, 5.0, 1.0, 2.0, 3.0 ]
```

The function has the following parameters:

-   **N**: number of indexed elements.
-   **k**: number of positions to shift.
-   **x**: input array.
-   **strideX**: stride length.

The `N` and stride parameters determine which elements in the strided array are accessed at runtime. For example, to circularly shift every other element:

```javascript
var x = [ 1.0, 0.0, 2.0, 0.0, 3.0, 0.0, 4.0, 0.0 ];

gcircshift( 4, 1, x, 2 );
// x => [ 4.0, 0.0, 1.0, 0.0, 2.0, 0.0, 3.0, 0.0 ]
```

Note that indexing is relative to the first index. To introduce an offset, use [`typed array`][mdn-typed-array] views.

```javascript
import Float64Array from 'https://cdn.jsdelivr.net/gh/stdlib-js/array-float64@esm/index.mjs';

// Initial array...
var x0 = new Float64Array( [ 0.0, 1.0, 2.0, 3.0, 4.0, 5.0 ] );

// Create an offset view...
var x1 = new Float64Array( x0.buffer, x0.BYTES_PER_ELEMENT*1 ); // start at 2nd element

// Circularly shift elements in the view:
gcircshift( 5, 2, x1, 1 );
// x0 => <Float64Array>[ 0.0, 4.0, 5.0, 1.0, 2.0, 3.0 ]
```

#### gcircshift.ndarray( N, k, x, strideX, offsetX )

Circularly shifts the elements of a strided array by a specified number of positions using alternative indexing semantics.

```javascript
var x = [ 1.0, 2.0, 3.0, 4.0, 5.0 ];

gcircshift.ndarray( x.length, 2, x, 1, 0 );
// x => [ 4.0, 5.0, 1.0, 2.0, 3.0 ]
```

The function has the following additional parameters:

-   **offsetX**: starting index.

While [`typed array`][mdn-typed-array] views mandate a view offset based on the underlying buffer, the offset parameter supports indexing semantics based on a starting index. For example, to access only the last three elements of the strided array:

```javascript
var x = [ 1.0, 2.0, 3.0, 4.0, 5.0, 6.0 ];

gcircshift.ndarray( 3, 1, x, 1, x.length-3 );
// x => [ 1.0, 2.0, 3.0, 6.0, 4.0, 5.0 ]
```

</section>

<!-- /.usage -->

<section class="notes">

## Notes

-   If `N <= 0`, both functions return the strided array unchanged.
-   If `k` is a multiple of `N`, both functions return the strided array unchanged.
-   If `k > 0`, elements are shifted to the right.
-   If `k < 0`, elements are shifted to the left.
-   Depending on the environment, the typed versions ([`dcircshift`][@stdlib/blas/ext/base/dcircshift], [`scircshift`][@stdlib/blas/ext/base/scircshift], etc.) are likely to be significantly more performant.

</section>

<!-- /.notes -->

<section class="examples">

## Examples

<!-- eslint no-undef: "error" -->

```html
<!DOCTYPE html>
<html lang="en">
<body>
<script type="module">

import discreteUniform from 'https://cdn.jsdelivr.net/gh/stdlib-js/random-array-discrete-uniform@esm/index.mjs';
import gcircshift from 'https://cdn.jsdelivr.net/gh/stdlib-js/blas-ext-base-gcircshift@esm/index.mjs';

var x = discreteUniform( 10, -100, 100, {
    'dtype': 'generic'
});
console.log( x );

gcircshift( x.length, 3, x, 1 );
console.log( x );

</script>
</body>
</html>
```

</section>

<!-- /.examples -->

<!-- Section for related `stdlib` packages. Do not manually edit this section, as it is automatically populated. -->

<section class="related">

</section>

<!-- /.related -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->


<section class="main-repo" >

* * *

## Notice

This package is part of [stdlib][stdlib], a standard library with an emphasis on numerical and scientific computing. The library provides a collection of robust, high performance libraries for mathematics, statistics, streams, utilities, and more.

For more information on the project, filing bug reports and feature requests, and guidance on how to develop [stdlib][stdlib], see the main project [repository][stdlib].

#### Community

[![Chat][chat-image]][chat-url]

---

## License

See [LICENSE][stdlib-license].


## Copyright

Copyright &copy; 2016-2026. The Stdlib [Authors][stdlib-authors].

</section>

<!-- /.stdlib -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="links">

[npm-image]: http://img.shields.io/npm/v/@stdlib/blas-ext-base-gcircshift.svg
[npm-url]: https://npmjs.org/package/@stdlib/blas-ext-base-gcircshift

[test-image]: https://github.com/stdlib-js/blas-ext-base-gcircshift/actions/workflows/test.yml/badge.svg?branch=main
[test-url]: https://github.com/stdlib-js/blas-ext-base-gcircshift/actions/workflows/test.yml?query=branch:main

[coverage-image]: https://img.shields.io/codecov/c/github/stdlib-js/blas-ext-base-gcircshift/main.svg
[coverage-url]: https://codecov.io/github/stdlib-js/blas-ext-base-gcircshift?branch=main

<!--

[dependencies-image]: https://img.shields.io/david/stdlib-js/blas-ext-base-gcircshift.svg
[dependencies-url]: https://david-dm.org/stdlib-js/blas-ext-base-gcircshift/main

-->

[chat-image]: https://img.shields.io/badge/zulip-join_chat-brightgreen.svg
[chat-url]: https://stdlib.zulipchat.com

[stdlib]: https://github.com/stdlib-js/stdlib

[stdlib-authors]: https://github.com/stdlib-js/stdlib/graphs/contributors

[umd]: https://github.com/umdjs/umd
[es-module]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules

[deno-url]: https://github.com/stdlib-js/blas-ext-base-gcircshift/tree/deno
[deno-readme]: https://github.com/stdlib-js/blas-ext-base-gcircshift/blob/deno/README.md
[umd-url]: https://github.com/stdlib-js/blas-ext-base-gcircshift/tree/umd
[umd-readme]: https://github.com/stdlib-js/blas-ext-base-gcircshift/blob/umd/README.md
[esm-url]: https://github.com/stdlib-js/blas-ext-base-gcircshift/tree/esm
[esm-readme]: https://github.com/stdlib-js/blas-ext-base-gcircshift/blob/esm/README.md
[branches-url]: https://github.com/stdlib-js/blas-ext-base-gcircshift/blob/main/branches.md

[stdlib-license]: https://raw.githubusercontent.com/stdlib-js/blas-ext-base-gcircshift/main/LICENSE

[@stdlib/blas/ext/base/dcircshift]: https://github.com/stdlib-js/blas-ext-base-dcircshift/tree/esm

[@stdlib/blas/ext/base/scircshift]: https://github.com/stdlib-js/blas-ext-base-scircshift/tree/esm

[mdn-typed-array]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/TypedArray

<!-- <related-links> -->

<!-- </related-links> -->

</section>

<!-- /.links -->
