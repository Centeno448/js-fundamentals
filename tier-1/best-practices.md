# Best Practices

## Use `===` comparison
``` js
const equalValue = 4 == '4'; // True

const equalValueAndType = 4 === '4'; // False
```


## Strict mode
```js
// Strict mode
function strictFunction() {
  'use strict';

  noGlobalVariables = true;

  var undefined = 4;
}
```

## Avoid using `eval`
``` js
function looseJsonParse(obj) {
  return eval('(' + obj + ')');
}

function saferLooseJsonParse(obj) {
  return Function('"use strict";return (' + obj + ')')();
}
``` 

## Avoid global variables
``` js
const equalValue = 4 == '4'; // True

const equalValueAndType = 4 === '4'; // False
```