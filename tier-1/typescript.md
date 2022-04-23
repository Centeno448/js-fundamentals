# Typescript

## Basics

**What is TypeScript?**
TypeScript is a strongly typed super-set of JavaScript. In other words, Javascript with types

**Compiler options**
We can configure the TS compiler via the use of a `tsconfig.json` file. This allows us to fine-tune TS to our specific standards/environment/needs.

``` ts
// tsconfig.json

{
  "compilerOptions": {
    "module": "commonjs",
    "noImplicitAny": true,
    "removeComments": true,
    "preserveConstEnums": true,
    "sourceMap": true
  }
}
```

**JS Targets**
In the compiler options we can define the `target` JS version so that when the code is transpiled, functions and other features are downleveled according to the intended runtime platform.

``` ts
// tsconfig.json

{
  "compilerOptions": {
    "target":  "es5" // arrow functions will be converted to normal 'function' definitions
  }
}
```

**Declaration files**
Declaration files are files with the `d.ts` extension and serve the purpose of decribing an existing JS codebase to TS, so that you can get proper errors and editor autocompletion support.

``` ts
// example.d.ts

export function getTheThings(): string[];

export function doTheThing(condition: boolean): void;

export as namespace MyLibrary;
```

## Types
Basic, enum, type alias, string literal
TypeScript has out-of-the-box support for common Basic types such as `number`, `string`, `boolean` etc. You can also define custom types.

``` ts
// Basic types
let imANumber: number;
let imAString: string;
let imABool: boolean;
let imAnArray: [];
let imAnObject: {};

// Enums
enum MyEnum {
  OptionOne = 'One',
  OptionTwo = 'Two',
  OptionThree = 'three',
}

MyEnum.OptionTwo; // 'Two'

// Type alias

type Numeric = number;

let imNumeric: Numeric = 2;

type Container<T> = { value: T }; // can be generic

let myContainer: Container<number> = { value: 2 };

// String literals
let stringLiteral: 'Literal' = 'Literal'; // not really useful by itself

let status: 'InProgress' | 'Done' | 'Failed' = 'Done'; // Useful combined with unions 
```

## Interfaces
With TS we can define interfaces. The properties we define in these interfaces can also be optional or readonly. The interfaces can also be indexable and hybrids.

``` ts
interface MyInterface {
  imNormal: number;
  imOptional?: string;
  readonly imReadOnly: number;
}

let normalInterface: MyInterface = { imNormal: 2, imReadOnly: 3 };

let normalInterfaceWithOptional: MyInterface = {
  imNormal: 2,
  imReadOnly: 3,
  imOptional: 'Im here!',
};

interface IndexableInterface {
  [indexable: number]: string;
}

let indexable: IndexableInterface = ['Bunch', 'Of', 'Strings'];
indexable[1]; // Of

interface HybridInterface {
  (hybrid: number): string;
  alsoAnObject: string;
}

function createHybrid(): HybridInterface {
  let hybrid = function (hybrid: number) {
    return `result is ${hybrid}`;
  } as HybridInterface;

  hybrid.alsoAnObject = 'Got a string';

  return hybrid;
}

let hybridInterface = createHybrid();

hybridInterface(7); // result is 7
hybridInterface.alsoAnObject; // Got a string

```

## Classes

TS classes use the standard access modifiers `public` (default) `protected` and `private`

``` ts
class Greeter {
  public sayHi() {
    console.log('hi!');
  }

  sayHello() {
      console.log('Hello, ' + this.protectedMethod());
  }

  protected protectedMethod() {
      return 'protected!';
  }

  private privateHi() {
      console.log('private Hi!');
  }
}

class SpecialGreeter extends Greeter {
    public helloThere() {
    // OK to access protected member here
    console.log("Hello there, " + this.protectedMethod());
  }
}

const greeter = new Greeter();

greeter.sayHi(); // hi!
greeter.sayHello(); // Hello, protected!
greeter.privateHi(); // TS error
greeter.protectedMethod(); // TS error

const specialGreeter = new SpecialGreeter();

SpecialGreeter.helloThere(); // Hello there protected!
specialGreeter.protectedHi(); // TS Error

```

Class properties can also be readonly, blocking assingment to the property outside of the constructor

``` ts
class Person {
    readonly name: string = 'default';

    constructor(name?: string) {
        if(name){
            this.name = name;
        }
    }

    changeName() {
        this.name = 'changed' // TS Error
    }
}

let person = new Person('diego');
person.name = 'other'; // TS Error
```

Classes can also have accessors (getters and setters)

``` ts
class Person {
    _name: string = 'default';
    _age: number = 22;


    constructor(age: number, name: string) {
        this._name = name;
        this._age = age;
    }

    get name() {
        return this._name;
    }

    get age() {
        return this._age;
    }

    set age(age: number) {
        this._age = age;
    }
}

let person = new Person(22, 'diego');

person.name;
person.age
person.age = 24;
person.name = 'a'; // TS error. Since no setter is found it treats property as readonly
```

Classes may also have static members

``` ts
class MyClass {
  static x = 0;
  private static y = 3;
  static printX() {
    console.log(MyClass.x);
  }
}

class AnotherClass extends MyClass {
    myPrintX = AnotherClass.printX();
}

console.log(MyClass.x);
MyClass.printX();
console.log(MyClass.y); // TS Error
```


## Functions
Functions in TS can be asigned to types, have default and optional parameters and can accept an undefined number of parameters (rest parameters)

``` ts
// Function types

type SayHelloFunction = (name: string) => void;

function greeter(fn: SayHelloFunction){
  // ...
}

// optional and default params

function myFunction(
  normalParam: string,
  defaultParam: boolean = true,
  optional?: number
) {
  // ...
}


// rest parameters
function acummulator(...numbers: number[]) {
  return numbers.reduce((prev, current) => prev + current, 0);
}

acummulator(2, 5, 6, 8); // 21

```

## Modules
Namespaces, re-exports, default exports, module resolution

``` ts

```

## Generics
Generic type variables, types classes and constraints
``` ts

```

## Type inference
Best common type, contextual type, type compatibility
``` ts

```

## Advanced types
Union and intersection types, type guards, nullable types, keyof and Lookup, Mapped types
``` ts

```