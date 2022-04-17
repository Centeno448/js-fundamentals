# ES6

## Built in promises
ES6 introduced built in promise objects and `Promise.prototype.then()` / `Promise.prototype.catch()` methods to handle them.

``` js
function complexPositiveAdd(numA, numB) {
  const promise = new Promise((resolve, reject) => {
        if (numA >= 0 && numB >= 0) {
          // complex logic that takes time
          resolve(numA + numB)
        }
        else {
          reject('NOT_POSITIVE_NUMBER') 
        }
  });

  return promise;
};

complexPositiveAdd(1, 2)
  .then(result => console.log(result))
  .cath(error => console.log('Error:', error));
```

## How transpiling affects the code
Transpilation between ES6 and older versions of JS is tipically done by transpilers such as [Babel](https://babeljs.io/). It takes the new features available and converts them into older javascript so that compatibility between devices is maximized

_before.js_
``` js
const name = "Sam";

console.log(`Hello ${name}`);
```

_after.js_
``` js
const name = "Sam";

console.log("Hello" + name);
```

## Arrow functions
ES6 added the hability to declare/pass functions compactly using arrow function expressions

``` js
const simpleAdd = (a, b) => a + b;

fetch('https://jsonplaceholder.typicode.com/users')
  .then((response) => response.json()) // arrow function as callback
  .then((json) => console.log(json[0])); // arrow function as callback
```

## ES6 syntax classes
ES6 also formalizes class declarations, built on prototypes

``` js
class Shape {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
}
```

or with the class expression

``` js
let Shape = class {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
}
```

## `const` over `let`
The `const` keyword is used to declare constants that once initialized cannot be changed. `let`, on the other hand is how you declare block-scoped variables whose value can change at any given time.

``` js
const wontChange = 'I Will not change';

wontChange = 'Changed' // throws error

let mayChange = 'I can change if need be';

mayChange = 'Changed' // all good
```

## Spread operator
The spread operator expands iterables (arrays, strings, etc) in places where zero or more arguments (for function calls) or elements (for array literals) are expected, or an object expression to be expanded in places where zero or more key-value pairs (for object literals) are expected.

``` js
function sum(x, y, z) {
  return x + y + z;
}

const numbers = [1, 2, 3];

console.log(sum(...numbers)); // 6

// Clone objects
let obj = {
  name: 'Diego',
  age: 22
}

const clonedObj = {...obj}

// replace object values
obj = {...obj, age: 24}
```

## Default parameter values
With ES6 we can now define default parameter values for functions, when no value is passed or `undefined` is passed
``` js
function multiply(a, b = 1) {
  return a * b;
}

console.log(multiply(5, 3)); // 15

console.log(multiply(5)); // 5

console.log(multiply(5, undefined)); // 5
```

## Destructure values
We can destructure arrays and objects to unpack values into distinct variables.

Array desctructuring
``` js
const [a, b] = [10, 20];
```

Object destructuring
``` js
const user = {
    id: 42,
    isVerified: true
};

const {id, isVerified} = user;
```

## Concise properties and methods
QoL feature to save keystrokes while assigning values into objects when the name of the object property is the same as the variable name that we wish to assign it to.

``` js
const username = 'diego';
const id = 2;

const user = {
  username,
  id,
  getInfo() {
    return `Id: ${id}; username: ${username}`
  }
}

user.getInfo() // Id: 2; username: diego;
```

## Array helper functions
ES6 includes some Array helper functions to manipulate data stores in these structures, some being:

``` js
const arr = [1, 2, 3, 4];

arr.forEach(element => console.log(element)) 
// 1
// 2
// 3
// 4

arr.map(element => element * 2) // [2, 4, 6, 8]

arr.filter(element => element >= 3) // [3, 4]

arr.find(element => element === 3); // 3

arr.reduce((acum, element) => acum + element, 0) // 10

arr.some(element => element === 5) // false

arr.every(element => element > 0) // true

Array.from('Hello') // ['H', 'e', 'l', 'l', 'o']
```

## Collections (TypedArrays, Map, Sets)

TypedArrays
``` js
let typedArray = new Uint8Array([0,1,2]);
console.log(typedArray.length); // 3

for(let item of typedArray){
  console.log(item);
}// 0, 1, 2

let normalArray = [...typedArray]; // [0,1,2]
```

Maps
``` js
let front = {name: 'Frontend Guide'},
    back = {name: 'Backend Guide'},
    general = {name: 'General Guidelines'};

let documentStatus = new Map([
  [front, 'draft'],
  [back, 'awaiting approval'],
  [general, 'approved']
]);

documentStatus.get(general) // approved
```

Sets
``` js
const passedLessons = new Set()

passedLessons.add(1); // Set [1]
passedLessons.add(3); // Set [1, 3]
passedLessons.add(3); // Set [1, 3]
passedLessons.add(5); // Set [1, 3, 5]

passedLessons.has(3) // true

passedLessons.delete(1)
passedLessons.has(1) // false
```

## Format strings and multi-line strings

``` js
const name = 'Diego';

console.log(`My name is ${name}!`); // My name is Diego!

console.log(`first line 1
second line 2`);
// first line 1
// second line 2
```

## Custom interpolation

_TODO_

## Transpiling

_TODO_