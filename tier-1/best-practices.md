# Best Practices

## Use `===` comparison

The underlying comparison operation between the `==` and `===` operators is the same. the difference is that the `===` operator will not try to convert both values into the same 'type'before comparing them.

It is recommended to use the `===` operator to avoid potentially processing data that the code is not expecting


``` js
const equalValue = 4 == '4'; // True

const equalValueAndType = 4 === '4'; // False
```

## Strict mode

Strict mode is a way to opt-in to a restricted variant of JS that makes 3 general changes:
- Eliminates some JavaScript silent errors by changing them to throw errors.
- Fixes mistakes that make it difficult for JavaScript engines to perform optimizations.
- Prohibits some syntax likely to be defined in future versions of ECMAScript.

There are multiple ways to enable strict mode:

In the beginning of a file

```js
'use strict';

// ...code
```

At a function level
```js
function strictFunction() {
  'use strict';

  noGlobalVariables = true;

  var undefined = 4;
}
```

Modules are automatically in strict mode
``` js
function moduleFunction() {
  // will be strict by default
}

export default moduleFunction;
```

## Avoid using `eval`
Since the `eval` function executes the JS it's passed with the caller priviliges i.e the program, you could potentially be executing malacious code with elevated privileges. Use `window.Function` instead.

``` js
function looseJsonParse(obj) {
  return eval('(' + obj + ')');
}

function saferLooseJsonParse(obj) {
  return Function('"use strict";return (' + obj + ')')();
}
``` 

## Avoid global variables
It is recommended to avoid using global variables since, they are in global scope, any piece of code can access/change them and cause another piece of code to fail.

_variables.js_

``` js
var myGlobalVar = 'Global'
```

_oneFile.js_

``` js
// Logic assuming window.myGlobalVar is a string
```


_otherFile.js_
``` js
window.myGlobalVar = true // Next time oneFile.js is ran it will fail
```
