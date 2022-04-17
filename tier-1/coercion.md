# Coercion

## Explicit coersion
We can explicit convert between types with some of the following methods

``` js
Number("32") // 32

String([]) // ""

Boolean(0) // false

parseInt("1") // 1

parseFloat("2.43") // 2.43
```

## Implicit coercion (`==` vs `===`)
Conversion can happen implicitly before comparison while using the `==`, `-`, `+`, `*`, `/` operators. The `===` operator will not try to implicitly convert values before comparing.

``` js
"" == false // true

"1" == 1 // true

null == undefined // true

"5" - "3" // 2

"3" * "2" // 6

"10" / "2" // 5

"test" + null // "testnull"

true + true // 2

null === undefined // false

"1" === 1 // false
```

## Implicit coercion: Logical operators
With the execption of the `!==` & `===` operators, logical operators will always try implicit coercion if the value types do not match

``` js
2 > "3" // false

true < true // false

true <= true // true

"hello" >= "world" // false

"a" < "b" // true
```

## Truthy and falsy values
Since implicit coercion is also done by the `if` expression, then there are values that will evaluate to false (falsy) and others that will evaluate to true (truthy).

Everything that is not falsy, is truthy. Falsy values are as follow

``` js
if("") {
    // ...
}

if(0) {
    // ...
}

if(-0) {
    // ...
}

if(undefined) {
    // ...
}

if(null) {
    // ...
}

if(NaN) {
    // ...
}
```