Puncher
=======

[![Build Status](https://secure.travis-ci.org/nodeca/puncher.png)](http://travis-ci.org/nodeca/puncher)

Library to collect timing `data` for your node.js application.
Simplifies bottlenecks search.

1. Easy interface.
2. Nesting support with coverage info.

See [API documentation](http://nodeca.github.com/puncher/) and example.


Usage overview
--------------

``` javascript
// require Puncher library
var Puncher = require('puncher');


// start profiler
var p = new Puncher();


p.start('Total');
setTimeout(function () {

  p.start('Block 1');
  setTimeout(function () {
    p.stop(); // Stop Block 1

    p.start('Block 2');
    setTimeout(function () {
      p.stop(); // Stop Block 2

      p.stop(); // Stop Total
      console.log(require('util').inspect(p.result, false, 10, true));
    }, 300);
  }, 200);
}, 100);
```

Example above will show you something like this:

``` javascript
[ { message: 'Total',
    start: 1342643670524,
    stop: 1342643671130,
    elapsed: { total: 606, missed: 105 },
    meta: {},
    childs: 
     [ { message: 'Block 1',
         start: 1342643670629,
         stop: 1342643670829,
         elapsed: { total: 200.56, missed: 0 },
         meta: {},
         childs: [] },
       { message: 'Block 2',
         start: 1342643670829,
         stop: 1342643671130,
         elapsed: { total: 301.14, missed: 0 },
         meta: {},
         childs: [] } ] } ]
```

