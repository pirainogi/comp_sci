## ES6 (ECMAScript 2015)

### Variables
* `let` allows variable declaration with block scope
  * variables declared with `let` can change their value

```JS
var x = 10; // x is 10
{
  let x = 2 // inside the block, x is 2
}
// x is 10 outside of the scope
```

* `const` allows constant declaration (JS variable with a constant value)
  * as implied, the value of a `const` variable CANNOT change

  ```JS
  var x = 10; // x is 10
  {
    const x = 2 // inside the block, x is 2
  }
  // x is 10 outside of the scope
  ```

### Functions

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
