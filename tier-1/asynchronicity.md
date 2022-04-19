# Asynchronicity

## Event loop
The stack keeps track of all operations to be executed, once its empty the event loop will check the message queue for messages to be processed and add them to the stack.

<p align="center">
<img src="./images/javascript_runtime_environment_example.svg">   
</p>
<p align="center">
<i></i>
</p>

```js
(function() {

  console.log('this is the start'); // stack - 1

  setTimeout(function cb() {
    console.log('Callback 1: this is a msg from call back'); // gets added to queue - 1
  });

  console.log('this is just a message'); // stack - 2

  setTimeout(function cb1() {
    console.log('Callback 2: this is a msg from call back'); // gets added to queue - 2
  }, 0);

  console.log('this is the end'); // stack - 3

})();

// "this is the start"
// "this is just a message"
// "this is the end"
// "Callback 1: this is a msg from call back"
// "Callback 2: this is a msg from call back"
```
## Callbacks
Callback functions are functions that are passed into another function as an argument, and will eventually be invoked inside of this other function to complete a routine.
They are useful in asynchronous operations so that the main program thread is not blocked.

``` js
function myCallbackFunction {
    console.log('Callback');
}

setTimeout(myCallbackFunction, 3000); // will run myCallbackFunction after 3000ms
```

## Promises
A promise is an object that may produce a resolved value or an error in the future.

``` js
function complexPositiveAdd(numA, numB) {
  const promise = new Promise((resolve, reject) => {
        if (numA >= 0 && numB >= 0) {
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

## `async`/`await` to simulate `Promise.then`, `Promise.all`, etc

``` js
fetch('https://jsonplaceholder.typicode.com/users')
  .then((response) => response.json())
  .then((json) => console.log(json[0])); 


// using async / await 
async function fetchAndPrintFirstUser() {
  const response = await fetch("https://jsonplaceholder.typicode.com/users");

  const jsonResponse = await response.json();

  const firstUser = jsonResponse[0];

  console.log(firstUser);
}

fetchAndPrintFirstUser();
```

## Promise library

_TODO_