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

#### Template Literals
* New syntax introduced for interpolation
  * `${NAME}`

#### Destructuring
tbd

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

#### Spread Operator
* Spread syntax `[...]` allows an iterable (such as an array expression or a string) to be expanded in places where zero or more arguments (function calls) or elements (array literals) are expected, or an object expression to be expanded where zero or more key-value pairs are expected

```JS
function sum(x, y, z){
  return x + y + z
}

const numbers = [1, 2, 3]

console.log(sum(...numbers)) //output is 6
```
  * Syntax
  ```JS
  //function calls
  myFunction(...iterableObj)

  //array literals or strings
  [...iterableObj, '4', 'five', 6]

  //object literals
  let objClone = {...obj} //ES2018
  ```

  * Replaces  `apply()`
    * when you want to use the elements of an array as the arguments of a function

    ```JS
    function myFunction(x, y, z){}
    const args = [0, 1, 2]
    myFunction.apply(null, args)

    //ES6
    function myFunction(x, y, z){}
    const args = [0, 1, 2]
    myFunction(...args)
    ```

    * any argument in the list can use spread syntax, and the syntax can be used multiple times

    ```JS
    function myFunction(v, w, x, y, z){}
    const args = [0, 1]
    myFunction(-1, ...args, 2, ...[3])
    ```

  * With `new`
    * when calling a constructor with `new` it's not possible to directly use an array and `apply()` because `apply()` does a `[[Call]]` and not a `[[Construct]]`
    * arrays can easily be used with new with the spread operator
    ```JS
    const dateFields = [1970, 0, 1] // 1 Jan 1970
    const d = new Date(...dateFields)  
    ```

    * otherwise you would have to do the same operation indirectly through partial application (don't do this it looks awful and v long to implement)

  * Array Literals
    * you can't create a new array using an existing array without implementing `push()`, `splice()`, `concat()` etc
    * spread operator allows you to just plug in the existing array
    ```JS
    const parts = ['shoulders', 'knees']
    const lyrics = ['head', ...parts, 'and', 'toes'] //  ["head", "shoulders", "knees", "and", "toes"]
    ```
    * you can also copy arrays
    ```JS
    const arr = [1, 2, 3]
    const copy = [...arr]
    copy.push(4)// copy is [1, 2, 3, 4]
    // arr is unchanged
    ```
      * the spread operator goes ONE level deep when copying an array and might be unsuitable for multi-dimensional arrays
      ```JS
      const a = [[1], [2], [3]]
      const b = [...a]
      b.shift().shift() // 1
      a // [[], [2], [3]]
      ```
    * Concatenating Arrays
      * `concat()` is often used to concatenate an array onto the end of another but can also be replaced with the spread operator
      ```JS
      const arr1 = [0, 1, 2]
      const arr2 = [3, 4, 5]
      arr1 = arr1.concat(arr2) // [0, 1, 2, 3, 4, 5]

      //ES6
      arr1 = [...arr1, ...arr2] // [0, 1, 2, 3, 4, 5]
      ```

      * `unshift()` is often used to insert an array of values at the start of an existing array but can be replaced with the spread operator
      ```JS
      const arr1 = [0, 1, 2]
      const arr2 = [3, 4, 5]
      // prepend all items from arr2 onto arr1
      Array.prototype.unshift.apply(arr1, arr2) // [3, 4, 5, 0, 1, 2]

      //ES6
      arr1 = [...arr2, ...arr1] // [3, 4, 5, 0, 1, 2]
      ```
  * Object Literals
    * With an object literal, it copies enumerable properties from a provided object to another (in stage 4)
    * shallow cloning or merging objects is now possible using shorter syntax than `Object.assign()`
    ```JS
    const obj1 = { foo: 'bar', x: 42 }
    const obj2 = { foo: 'baz', y: 13 }
    const clonedObj = {...obj1} // { foo: 'bar', x: 42 }
    const mergedObj = {...obj1, ...obj2} // { foo: 'baz', x: 42, y: 13 }
    ```

      * `Object.assign()` triggers `setters` but the spread syntax does not

      ```JS
      const obj1 = { foo: 'bar', x: 42 }
      const obj2 = { foo: 'baz', y: 13 }
      const merge = (...objects) => ({...objects})

      let mergedObj1 = merge(obj1, obj2)
      // { 0: { foo: 'bar', x: 42 }, 1: { foo: 'baz', y: 13 } }
      let mergedObj2 = merge({}, obj1, obj2)
      //{ 0: {}, 1: { foo: 'bar', x: 42 }, 2: { foo: 'baz', y: 13 } }
      ```

    * Objects themselves are not iterable, but they can become iterable when used in an array or with iterating functions (`map()`, `reduce()`, `assign()`)
      * when merging two objects together, it is assumed another iterating function is used when merging occurs

#### Promises
tbd

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
    * returns `false` for anything else
* Exponential Operator `**` raises the first operand to the power of the second
  * `x ** y` has the same result as `Math.pow(x, y)`

```JS
const x = 5
const z = x ** 2 // returns 25
```


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

### Modules
tbd 
