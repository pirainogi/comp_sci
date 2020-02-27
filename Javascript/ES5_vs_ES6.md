## ES6 (ECMAScript 2015)

### Variables

#### Let
* `let` allows variable declaration with block scope
  * variables declared with `let` can change their value

```JS
var x = 10; // x is 10
{
  let x = 2 // inside the block, x is 2
}
// x is 10 outside of the scope
```

#### Const
* `const` allows constant declaration (JS variable with a constant value)
  * as implied, the value of a `const` variable CANNOT change

  ```JS
  var x = 10; // x is 10
  {
    const x = 2 // inside the block, x is 2
  }
  // x is 10 outside of the scope
  ```

#### Numbers

* `EPSILON`, `MIN_SAFE_INTEGER`, and `MAX_SAFE_NUMBER` were all added to the Number object

* `isInteger()` and `isSafeInteger()` were added as new methods to the Number object
  * `isInteger()` returns `true` if the argument is an integer
  * `isSafeInteger()` returns `true` if the argument is a safe integer
    * Safe integers are all integers between -(2<sup>53</sup> -1) to +(2<sup>53</sup> - 1)
    * 9007199254740991 is safe
    * 9007199254740992 is not safe

### Functions

#### Arrow Functions
* Arrow functions allow a shorter syntax for writing function declarations
  * `function` keyword is excluded
  * `return` keyword isn't necessary if a single statement
  * curly brackets `{}` are also unnecessary if a one-liner
    * in the event that your function is either a multi-liner or has more than one statement, it is safer and to use `{}` and a `return` statement

```JS
//ES5
var x = function(x, y){
  return x * y
}

//ES6
const x = (x, y) => x * y

const x = (x, y) => { return x * y }
```

  * Arrow functions do not have `this`
    * not suited for defining object methods
  * NOT HOISTED
    * MUST be declared before they are invoked
  * `const` is the appropriate variable declaration because a function expression should always be a constant value

#### Default Parameter Values
* Function parameters can now include default values
  * declared within the argument `()` in the function declarationo

```JS
function myFunction(x, y = 10){
  //y is 10 unless otherwise passed in or undefined
  return x + y
}

myFunction(5) // will return 15
myFunction(5, 8) // will return 13
```

#### Array Methods
* `Array.find()` returns the value of the FIRST element that passes the callback function

```JS
let numbers = [4, 9, 16, 25, 29]
const first = numbers.find(myFunction) // returns 25

function myFunction(value, index, array){
  //accepts the element value, the element index, and the array itself
  return value > 18
}
```

* `Array.findIndex()` returns the index of the FIRST element that passed the callback function

```JS
let numbers = [4, 9, 16, 25, 29]
const first = numbers.findIndex(myFunction) // returns 3

function myFunction(value, index, array){
  //accepts the element value, the element index, and the array itself
  return value > 18
}
```

#### Global Methods
* Number Methods
  * `isFinite()` returns `false` if the argument is `Infinity` or `NaN`
    * returns `true` for any other Number
  * `isNan()` returns `true` if the argument is `NaN`
    * returns `false` for any other Number

### Classes

* Classes were introduced with ES6
  * initiated with the `class` keyword
  * properties are assigned inside a `constructor()` function

```JS
class Car {
    constructor(brand){
      this.carname = brand
    }
}
```

* Instances of the class are created with the `new` keyword

```JS
mycar = new Car("Ford")
```
