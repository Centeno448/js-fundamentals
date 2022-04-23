# Prototyping

## Object links
Object links refers to the "Prototypal Delegation" that happens when creating a new object. This occurs behind the scenes with simple object creations `var obj = {}` or more explicitly with the `Object.create` method

``` js
var Car = {
    startCar: function() {
        console.log('vroom vroom!');
    },
    describe: function() {
        console.log(`This is ${this.owner}'s car and it is ${this.color}`);
    }
}

var diegoCar = Object.create(Car);

diegoCar.owner = 'Diego';
diegoCar.color = 'blue';

diegoCar.startCar() // vroom vroom!
diegoCar.describe() // This is Diego's car and it is blue

Object.getPrototypeOf(diegoCar) === Car // true
Object.getPrototypeOf(diegoCar); // {startCar: ƒ, describe: ƒ}
Object.getOwnPropertyNames(diegoCar) // ["owner", "color"]
```

## Inspect classes relationships
We can inspect relationships between classes by following the protoype delegation chain

``` js
function Car() {
    this.color = '';
}

function Ferrari() {
    Car.call(this);
    this.ferrariOrnaments = [];
}

Ferrari.prototype = Object.create(Car.prototype);
Ferrari.prototype.constructor = Car;

function BMW() {
    Car.call(this);
    this.BMWSpecialFeatures = [];
}
BMW.prototype = Object.create(Car.prototype);
BMW.prototype.constructor = Car;


// Car is the parent of both Ferrari and BMW Classes
Ferrari.prototype // Car
BMW.prototype // Car

```

## Inheritance using prototyping
Using prototyping we can implement inheritance, due to the fact that with prototype delegation each 'child' created with Object.create will have access to the parent's properties and methods

``` js
function Car(color = 'pink') {
    this.color = color; // default color of red
    this.turnOn = function() {
        console.log('vrooom');
    }
}

function Ferrari(color) {
    Car.call(this, color);
    this.ferrariOrnaments = [];
}

Ferrari.prototype = Object.create(Car.prototype);
Ferrari.prototype.constructor = Car;

function BMW(color) {
    Car.call(this, color);
    this.BMWSpecialFeatures = [];
}
BMW.prototype = Object.create(Car.prototype);
BMW.prototype.constructor = Car;


let myFerrari = new Ferrari('red');
let myBMW = new BMW('blue');

myFerrari.turnOn() // vrooom
myFerrari.color // red

myBWM.turnOn() // vrooom
myBWM.color // blue
```

## Mixins
Mixins are simple objects which define methods that extend a given objects functionality using the `Object.assign` method. They are useful since an object can only inherit from 1 parent, but we can implement as many mixins as we want

``` js
let greetMixin = {
    greet() {
        console.log(`Hello there, I'm ${this.name}`);
    }
}

function User(name) {
    this.name = name;
}

function RegularUser(name) {
    User.call(this, name);
    this.role = 'regular';
}

RegularUser.prototype = Object.create(User.prototype);
RegularUser.prototype.constructor = User.prototype.contructor;

Object.assign(RegularUser.prototype, greetMixin);

let user = new RegularUser('diego');

user.greet() // Hello there, I'm diego
```

## Classes with prototyping
Classes are syntactic sugar over prototypes. Behind the scenes these code samples are the same.

_Classes_
``` js
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
  describe() {
    return `${this.name} : ${this.age}`;
  }
};

let diego = new Person("Diego", 22);
diego.describe() // Diego : 22

class Employee extends Person {

  constructor(name, age, height) {
    super(name, age);
    this.height = height;
  }
  info() {
    return `${this.name} : ${this.age} : ${this.height}`;
  }
};

let pedro = new Employee("Pedro", 46, 7.5);
noomi.info() // Pedro : 46 : 7.5
```

_Prototypes_
``` js
let Person = function(name, age) {
  this.name = name;
  this.age = age;
};
Person.prototype.describe = function() {
  return `${this.name} : ${this.age}`;
};

let diego = new Person("Diego", 22);

diego.getDetails() // Diego : 22

let Employee = function(name, age, height) {
  Person.call(this, name, age);
  this.height = height;
};

Object.setPrototypeOf(Employee.prototype, Person.prototype);

EmployeeP.prototype.info = function() {
  return `${this.name} :: ${this.age} :: ${this.height}`;
};

let pedro = new EmployeeP("pedro", 46, 7.5);
pedro.info() // Pedro : 46 : 7.5
```

##  Object.assign
This method copies all enumerable own properties from one or more source to a target object. Usefull for extending object functionality

``` js
const target = { name: 'diego'};
const source = { age: 22 };

const result = Object.assign(target, source);


result // { name: 'diego', age: 22 }
target // { name: 'diego', age: 22 } (target object is modified & returned)
```

## Enumerate properties in an object
To enumerate all properties in an object we can iterate through the object with a for loop.

``` js
const object = { name: 'diego', age: 22 };

for(let prop in object) {
    console.log(`Prop name: ${prop}\tProp value: ${object[prop]}`);
}
// Prop name: name  Prop value: diego
// Prop name: age  Prop value: 22
```

## `hasOwnProperty()`
`Object.hasOwnProperty` is a method that checks if a given property was defined in the current object (not in it's prototype)

``` js
var Car = {
    startCar: function() {
        console.log('vroom vroom!');
    },
    describe: function() {
        console.log(`This is ${this.owner}'s car and it is ${this.color}`);
    }
}

var diegoCar = Object.create(Car);

diegoCar.owner = 'Diego';
diegoCar.color = 'blue';

diegoCar.hasOwnProperty('startCar')  // false
diegoCar.hasOwnProperty('describe')  // false
diegoCar.hasOwnProperty('owner')  // true
diegoCar.hasOwnProperty('color')  // true
```

## Arguments

_TODO_

## get, set
We can define getters and setters in JS objects using the `get` and `set` keywords. These are methods that are executed by accessing them as properties and are useful for doing extra work before accessing/modifying an object property

``` js
let student = {
    name: 'Diego',

    get getName() {
        return this.name + "s"; 
    },

    set setName(newName) {
        if(newName !== 'pedro')
            this.name = newName
    }
}

student.getName // Diegos
student.setName = 'David';
student.getName // Davids
```