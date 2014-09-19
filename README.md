# Sass-respond

Sass-respond is a [Sass](https://github.com/nex3/sass)-based tool that simplifies dealing with CSS3 Media Queries.

### Requirements

Sass 3.2.0+

### Browser support

Every browser which supports CSS3 Media Queries supports Sass-respond as well. See compatibility table: http://caniuse.com/#feat=css-mediaqueries

## Installation

### Bower

- Terminal: `bower install sass-respond`
- SCSS: `@import 'path/to/bower_components/sass-respond/respond';`

### Vanilla Sass

- Copy `_respond.scss` into your project
- SCSS: `@import 'path/to/respond';`

## Getting started

1. Set *breakpoints*:

   ```scss
   @include respond-init(
     small 0 479px,
     medium 480px 939px,
     large 940px -1
   );
   ```

2. Include Media Queries:

   ```scss
   @include respond(small) {
      // rules for "small" breakpoint-range go here
   };
   ```

## Naming conventions

### Sass-respond's *breakpoint-expression* definition:

```
(papa-bear 640px 720px) - bp-exp (breakpoint-expression)
 papa-bear              - bp-name (breakpoint-name), in a display area's width
                          context also called a "breakpoint-range"
           640px 720px  - bp-range (breakpoint-range)
           640px        - bp-min (breakpoint-minimum)
                 720px  - bp-max (breakpoint-maximum)
 papa-bear 640px        - bp (breakpoint) at a "breakpoint-minimum"
 papa-bear       720px  - bp (breakpoint) at a "breakpoint-maximum"
```

### Sass-respond's lists definitions:

```
(lorem 640px 720px, ipsum 240px 480px) - bp-exp-list (breakpoint-expression-list,
                                         a list of breakpoint-expressions)
(alpha, beta, gamma, delta, epsilon)   - bp-name-list (breakpoint-name-list
                                         a list of breakpoint-names)
```

## Guide

### `respond-init()`

`respond-init()` mixin takes a *breakpoint-expression-list* as an argument. It doesn't output any CSS rules, so it should be invoked outside any selector, e.g. right before the `html` selector.

```scss
@include respond-init(
  small 0 479px,
  medium 480px 939px,
  large 940px -1
);
```

A *breakpoint-max* isn't necessary, if you want it to be precisely a 1 unit lower than the *breakpoint-min* of the next *breakpoint-expression*. You can also omit the `-1` at the very end, so the last *breakpoint-expression* of the *breakpoint-expression-list* will generate only a `min-width` Media Feature.

```scss
@include respond-init(
  small 0,
  medium 480px,
  large 940px
);
```

### `respond()`, `respond-not()`, `respond-gt()`, `respond-gte()`, `respond-lt()`, `respond-lte()`

`respond()` mixin takes a *breakpoint-name-list* as an argument.

All other mixins above take a single *breakpoint-name*.

```scss
@include respond(small) {
  // rules for "small" breakpoint-range go here
}
```

You can include the same rules for multiple *breakpoint-names* ( *breakpoint-ranges* ):

```scss
@include respond(medium large) {
  // rules for "medium" and "large" breakpoint-ranges go here
}
```

Above statement (in respect of `respond-init()` from *Getting started*) equals:

```scss
@include respond-gte(medium) {
  // rules for "medium" breakpoint-range and greater display area's width go here
}
```

or:

```scss
@include respond-gt(small) {
  // rules for greater display area's width than "small" breakpoint-range go here
}
```

or:

```scss
@include respond-not(small) {
  // rules for whole display area's width but "small" breakpoint-range go here
}
```

### Special mixins

Special mixins take no arguments.

```scss
@include respond-webkit {
  // WebKit only rules go here
}
```

```scss
@include respond-ie9-10 {
  // IE9 & IE10 only rules go here
}
```

```scss
@include respond-ie10-11 {
  // IE10 & IE11 only rules go here
}
```
### Setting Media Type

Sass-respond includes Media Queries with the `all` Media Type by default. `respond-set-media-type()` mixin takes a Media Type keyword as an argument to change this behavior, for example:

```scss
@include respond-set-media-type(print);
```

or:

```scss
@include respond-set-media-type(tv);
```

## License

Sass-respond is released under the MIT License.

```
Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
"Software"), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE
LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION
OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION
WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
```
