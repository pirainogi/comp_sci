#Trivia

##Programming Paradigms
1. **OOP** by way of _imperative/procedural_ programming
  * **Prototypal Inheritance**
  * Pros:
    * Easy to understand/interpret
    * imperative style
  * Cons:
    * Depends on shared state
    * Objects and behaviors are tacked together on the same entity which may be accessed at random by any number of fns with non-deterministic order
    * Resistant to change/brittle
2. **Functional** programming
  * enabled by lambdas with closure, first class functions
    * also higher order functions, functions as arguments/values
  * programs built with small, reusable **pure** functions
    * idempotence (same input = same output)
    * free from side effects (do not mutate any shared state or mutable arguments)
    * stronger guarantees of encapsulation than objects without function purity
  * Pros:
    * avoid shared state or side-effects
      * eliminates bugs caused by multiple functions competing for the same resources
    * simplified functions and more reusable code
    * declarative style
      * _what_ to do, underlying functions take care of _how_
      * allows for refactoring/performance optimization
  * Cons:
    * reduces readability (more abstract, less concrete)
    * higher learning curve

## Classical Inheritance vs. Prototypal Inheritance
1. Class Inheritance
  * instances inherit from classes and create sub-relationships
    * hierarchical class taxonomies
  * instantiated via a constructor fn with the `new` keyword
  * Rarely a good choice (esp after multi-level)
    * Single level is okay, ie. `React.Component`
2. Prototypal Inheritance
  * Instances inherit directly from other objects
  * instantiated via factory functions or `Object.create()`
  * Multiple types:
    * Delegation (prototype chain)
    * Concatenative (mixins, `Object.assign()`)
    * Functional (function used to create a closure)
  * Useful in their ability to enable composition
    * compose objects from multiple sources
3. "Favor object composition over class inheritance"
  * code reuse should be achieved by assembling smaller units of functionality into new objects, instead of inheriting from classes and creating object taxonomies
    * avoid class hierarchies
    * avoid brittle base class
    * avoid tight coupling
    * make code more flexible     

##Closures
* mechanism for containing state
* created whenever a function accesses a variable defined outside the immediate function scope
  * define a function within a function and expose the inner scope (by returning or passing it into another function)
  * can access variables in it's own scope, variables in the enclosing scope, and global variabels
  * variables inside will be available even after the outer function has finished running
* data privacy

```JS
var globalVar = "xyz"
(function outerFunc(outerarg){
  var outerVar = 'a'
  (function innerFunc(innerarg){
    var innerVar = 'b'
    console.log(outerArg) // 123
    console.log(innerArg) // 456
    console.log(outerVar) // a
    console.log(innerVar) // b
    console.log(globalVar) // xyz
  })(456)
})(123)
```

## Two-Way Data Binding vs. One-Way Data Flow
1. Two-way data binding
  * **ANGULAR**
  * UI fields are bound to model data dynamically
  * can cause side-effects that are harder to follow
2. One-way data flow
  * **REACT**
  * model is the single source of truth
  * changes in the UI trigger messages that signal user intent to the model (`store` in Redux)
  * model has access to change app's state
  * _deterministic_

## Monolith vs. Microservice Architecture
1. Monolith Architecture
  * app is written as one cohesive unit of code
  * components are designed to work together sharing the same memory space and resources
  * Pros:
    * easy to hook up components to cross-cutting concerns (logging, rate limiting, security features)
    * potential performance advantages
      * shared-memory access is faster than inter-process communication (IPC)
  * Cons:
    * tightly coupled; difficult to isolate services for independent scaling or code maintainability
    * harder to understand
      * dependencies, side-effects that may not be obvious
2. Microservice Architecture
  * app is made up of smaller, independent applications
  * capable of running in their own memory space and scaling independently from each other across potentially many separate machines
  * Pros:
    * Better organized
    * Decoupled services are easier to recompose and reconfigure to serve different apps
    * potential performance advantages
      * possible to isolate hot services and scale them independently
  * Cons:
    * likely to discover cross-cutting concerns
      * either need to incur the overhead of separate modules for each concern OR encapsulate cross-cutting concerns into another service layer that all traffic gets routed through
    * frequently deployed on their own VM or containers
      * requires VM work (can be automated with container fleet management tools)

## Asychronous Programming
1. Synchronous Programming
  * Barring conditionals and function  calls, code is executed sequentially from top to bottom, blocking long-running tasks such as network requests and disk I/O
2. Async Programming
  * Engine runs in an event loop
    * when blocking operations are needed, request is started and the code keeps running without blocking for the  result
    * when response is ready, interrupt is fired
    * causes the event handler to run
  * program thread can handle many concurrent operations
* User interfaces are async by nature
  * wait for user input to interrupt the event loop and trigger event handlers

### `typeof bar === "object"`
* `null` is also considered an object in Javascript
  * also need to compare for this
  * `console.log( (bar !== null) && (typeof bar === "object") )`
* if `bar` is a function, it will return `false`
  * `console.log( (bar !== null) && ((typeof bar === "object") || (typeof bar === "function")) )`
  * will return `true` for an array because an array is an object
  * to determine if an array with ES6
    * `console.log(Array.isArray(bar))`

### `NaN`
* represents a value that is not a number
* results from an operation that could not be performed either because one of the operands was non-numeric or because the result was non-numeric
* `NaN` is classified as a `Number`
  * compared to anything else, it returns `false`
* ES6 solution for testing:
  * `Number.isNan()`

### Determine if x is an Integer
* with ES6
  `Number.isInteger(x)`
* prior to ES6
  `function isInteger(x){ return (x^0) === x }`
* `parseInt()` doesn't work for very large values of x
  * `parseInt()` coerces its first parameter into a string before parsing digits
  * when a number becomes sufficiently large, it will be presented in exponential form and then cannot parse the `e` character and return a value of `1`

## Return Values of Code Snippets
### Variable Based
```JS
(function(){
  var a = b = 3
})()

console.log(typeof a !== 'undefined') // false
console.log(typeof b !== 'undefined') // true
```
* `var a = b = 3` can be understood as `b = 3` and `var a = b`
* without strict mode, `b` is a global variable because it isn't preceded by `var`
  * accessible even outside of the enclosing function
* with strict mode, you would get a runtime error

```JS
var myObject = {
  foo: "bar";
  func: function(){
    var self = this;
    console.log('outer fn, this:', this.foo)
    console.log('outer fn, self:',self.foo)
    (function(){
      console.log('inner fn, this:',this.foo)
      console.log('inner fn, self:',self.foo)
    })();
  }
}
myObject.func()
// outer fn, this: bar
// outer fn, self: bar
// inner fn, this: undefined
// outer fn, self: bar
```
* in the outer function, `this` and `self` refer to `myObject` and can access `foo`
* in the inner function, `this` refers to the current scope and `this.foo` is undefined within it
* in the inner function, `self` still remains in scope and can access `foo`

```JS
console.log(0.1 + 0.2) // 0.30000000000000004
console.log(0.1 + 0.2 === 0.3) // false
```
* JS treats numbers with floating precision
* in order to compare the absolute difference between the two:
  * `return Math.abs(0.1 - 0.2) < Number.EPSILON`

```JS
var d = {}
['zebra', 'horse'].forEach(function(k){
  d[k] = undefined
})
// d = {'zebra': undefined, 'horse': undefined}
```
* adds the elements from the array to the hash as keys pointing to the value of `undefined`
* `Object.keys` will return an array with those keys set


### Function Based
```JS
function foo1(){
  return {
    bar: "hello"
  };
}
function foo2(){
  return
  {
    bar: "hello"
  }
}
```
* `foo1` returns `Object {bar: "hello"}`
* `foo2` returns `undefined`
  * doesn't throw an error
  * JS adds a semicolon after the `return` statement when there isn't anything else included on the same line
  * rest of the code isn't invoked but isn't invalid and therefore never throws an error

```JS
var a = {},
b = {key: 'b'},
c = {key: 'c'}

a[b] = 123
a[c] = 456
console.log(a[b]) // 456
```
* When setting an object property, JS will implicitly stringify the parameter value
  * `b` and `c` are both objects that will be converted to `[object Object]`
  * a[b] and a[c] evaluate to the same and can be used interchangably
  * reference point is the same, so `a[c]` with overwrite `a[b]`

```JS
(function(){
  console.log(1)
  setTimeout(function(){console.log(2)}, 1000)
  setTimeout(function(){console.log(3)}, 0)
  console.log(4)
})()
//1
//4
//3
//2
```
* `1` and `4` will log without delay because they are not invoked with a `setTimeout()`
* `3` will log next because it has a 0ms delay
* `4` will log last because it has a 1 second delay
* `3` logs after both `1` and `4` because the `setTimeout()` will be popped off the stack and added to the event queue. The 0 value as the second argument allows the function to run as soon as possible (next), but after the `4` is logged

```JS
for(var i = 0; i < 5; i++){
  setTimeout(function() { console.log(i)}, i * 1000)
}
```
* it will log `5` five times
* each function executed within the loop will be executed _after_ the entire loop has completed
* in order to log every number each time, wrap the timeout function in a closure to store every unique value of the variable `i`
```JS
for(var i = 0; i < 5; i++){
  (function(x) {
    setTimeout(function() { console.log(i)}, i * 1000)
  })(i)
}
```
* or just use `let` inistead of `var`

```JS
for(var i = 0; i < 5; i++){
  var btn = document.createElement('button')
  btn.appendChild(document.createTextNode('Button' + i))
  btn.addEventListener('click', function(){console.log(i)})
  document.body.appendChild(btn)
}
```
* `5` will always be logged because when the `onClick` method is invoked for _any_ button, the entire loop has already run and `i` will always resolve to `5`
  * different execution contexts
* Ways to solve:
```JS
for(var i = 0; i < 5; i++){
  var btn = document.createElement('button')
  btn.appendChild(document.createTextNode('Button' + i))
  btn.addEventListener('click', function(i){return function(){console.log(i)}(i)})
  document.body.appendChild(btn)
}
//capture the value of i every loop by creating a new function object and pass i into the immediately invoked function

for (var i = 0; i < 5; i++) {
  var btn = document.createElement('button');
  btn.appendChild(document.createTextNode('Button ' + i));
  (function (i) {
    btn.addEventListener('click', function() { console.log(i); });
  })(i);
  document.body.appendChild(btn);
}
//wrap the entire call to create the eventListener in an anonymous function

['a', 'b', 'c', 'd', 'e'].forEach(function (value, i){
  var btn = document.createElement('button')
  btn.appendChild(document.createTextNode('Button' + i))
  btn.addEventListener('click', function(){console.log(i)})
  document.body.appendChild(btn)
})
// replace the `for` loop with a `forEach` loop to call the array's objects

for(let i = 0; i < 5; i++){
  var btn = document.createElement('button')
  btn.appendChild(document.createTextNode('Button' + i))
  btn.addEventListener('click', function(){console.log(i)})
  document.body.appendChild(btn)
}
// use `let` instead of `var`
```

#### Palindrome Function
```JS
function palindrome(string){
  string = string.replace(/\W/g, "").toLowerCase()
  return (string === string.split(" ").reverse().join(""))
}
```

```JS
var arr1 = "john".split("") // ["j", "o", "h", "n"]
var arr2 = arr1.reverse() // ["n", "h", "o", "j"]
var arr3 = "jones".split("") // ["j", "o", "n", "e", "s"]
arr2.push(arr3) // ["n", "h", "o", "j", ["j", "o", "n", "e", "s"]]
```
* calling `reverse()` returns the array in the reverse order but also mutates the original array
* `arr2` is only a reference to `arr1` that has been mutated
* passing an array into the `push()` method pushes the _entire_ array as a **single element** onto the end of the array

```JS
console.log(1 + "2" + "2") //"122"
//right to left: 1 + "2" and will concat because one is a string
//"12" + "2" = "122"
console.log(1 + +"2" + "2") //"32"
//reads +"2" as a positive 2 integer
// 1 + 2 = 3
// 3 + "2" will concat the two and result in "32"
console.log(1 + -"1" + "2") //"02"
//reads -"1" as a negative 1 integer
//1 + -1 = 0  
//0 + "2" = "02" because of coercion and concatenation
console.log(+"1" + "1" + "2") //"112"
//reads +"1" as a positive integer
//1 + "1" will still coerce and concat to "11"
//"11" + "2" = "112"
console.log("A" - "B" + "2") //"NaN2"
//`-` operator cannot be applied to strings and "A" and "B" cannot be converted to numeric values
//NaN + "2" will coerce NaN into a string and concat "2"
console.log("A" - "B" + 2) // NaN
//"A" and "B" cannot be coerced into numeric values to subtract one from the other, so NaN
// NaN - 2 is still NaN
```

```JS
console.log("0 || 1 = " + (0 || 1)) // 1
console.log("1 || 2 = " + (1 || 2)) // 1
console.log("0 && 1 = " + (0 && 1)) // 0
console.log("1 && 2 = " + (1 && 2)) // 2
```
* `X || Y` - `x` is evaluated and interpreted as a boolean value
  * if `true` is returned, `y` isn't evaluated
  * if `false` is returned, `y` has to be evaluated
* `X && Y` - `x` is first evaluated and interpreted as a boolean value
  * if `false`, then `false` is returned and `y` is not evaluated  
  * if `true`, then we evaluate `y`
  * if the entire expression is `true`, then the expression itself is returned

```JS
console.log(false == '0') //true
console.log(false === '0') //false
```
* `==` loose equality operator tries to coerce the value so it evaluates `0` the integer as  false
* `===` strict equality operator does not coerce and evaluates as is written

```JS
var list = readHugeList()

var nextListItem = function(){
  var item = list.pop()
  if(item){
    //process the item
    nextListItem()
  }
}
// this will cause a stack overflow if the list is too large
// fix below
var list = readHugeList()

var nextListItem = function(){
  var item = list.pop()
  if(item){
    //process the item
    setTimeout(nextListItem, 0)
  }
}
```
* Event Loop handles the recursion with the `setTimeout()` instead of the call stack
  * if `item` isn't null, the timeout function is pushed to the event queue
  * function exits and leaves the call stack clear
  * when the event queue runs its timed-out method, the next `item` is processed and the timer is set again
  * processed from start to finish without a direct recursive call so the stack remains clear regardless of the number of iterations

#### Sum Method (Multi or Single Argument)
```JS
function sum(x){
  if(arguments.length === 2){
    return arguments[0] + arguments[1]
  } else {
    return function(y) {return x + y}
  }
}
//OR
function sum(x, y){
  if(y !== undefined){
    return x + y
  } else {
    return function(y) {return x + y}
  }
}
```


##### What is the significance/reason for wrapping the entire content of a JS source file in a function block
* creates a closure around the entire contents of the file
* prevents name clashes
  * private namespace
* easily referenceable alias for a global variable

##### Significance/Benefits of `use strict`
* Voluntarily enforce stricter parsing/error handling at runtime
  * makes debugging easier
    * errors that would have otherwise silently failed will generate errors
  * prevents accidental globals
  * eliminates `this` coercion
    * a value of `this` that is `null` or `undefined` is automatically coerced to the global
  * disallows duplicate parameter values
  * makes `eval()` safer
    * variables and functions declared inside of an `eval()` statement are **not** created in containing scope
  * throws error on invalid usage of `delete`
    * `delete` operator cannot be used on non-configurable properties of the object
