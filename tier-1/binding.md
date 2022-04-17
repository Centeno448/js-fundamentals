# Binding

## Regular and arrow functions
In regular functions, the `this` keyword is binded to the object that called the function, meanwhile, arrow functions bind the `this` keyword to the object who defined the function

``` js
var Person = function(name) {
    this.name = name;
    this.getInfo = function() {
        callback = function() {
            console.log('name:', this.name);
        }
        // since this will be called in the global execution context, 
        // 'this' wont have refence to the name property of this object
        setTimeout(callback, 2000); 
    }
}

const me = new Person('diego');

me.getInfo() // name: undefined

var ArrowPerson = function(name) {
    this.name = name;
    this.getInfo = function() {
        callback = () => console.log('name:', this.name);
        
        // since arrow functions bind `this` to the object where the function
        // is defined, it will have the `name` property
        setTimeout(callback, 2000); 
    }
}

const me = new ArrowPerson('diego');

me.getInfo() // name: diego
```

## Explicit binding functions (`call()`, `apply()` & `bind()`)
All JS functions have access to the `call()`, `apply()` & `bind()` functions that allow us to change the binding of the `this` keyword for that given execution.

``` js
const obj = { name: 'Diego' };

function sayHello(greeting) {
    console.log(`${greeting} ${this.name}!`);
}

// Implicit binding (since the function has no reference to a 'name' property)
// it will remain undefined
sayHello('Hello'); // Hello !

// Explicit binding with call()
sayHello.call(obj, 'Hello'); // Hello Diego! 

// Explicit binding with apply()
sayHello.apply(obj, ['Salutations']); // Salutations Diego!

// Explicit binding with bind() will return a new function with the updated 'this' context 
const updatedSayHello = sayHello.bind(obj)

updatedSayHello('Hey there') // Hey there Diego!
```