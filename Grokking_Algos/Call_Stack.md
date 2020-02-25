## Call Stack
* A linked list or an array can be used to demonstrate a _stack_
  * Elements are added to the TOP of the list (**push**)
  * Elements are removed from the TOP of the list (**pop**)
  * **LAST IN, FIRST OUT**
  * The call stack can get very large, which will take up large amounts of memory

* The _call stack_ is how your computer completes units of work in a specific order

```JS
function greet(name){
  console.log(`hello, ${name} !`)
  greet2(name)
  console.log(“getting ready to say bye...”)
  bye()
}

function greet2(name){
  console.log(`how are you ${name}?`)
}

function bye(){
  console.log("okay, bye!")
}
```
* THE CALL STACK IS EMPTY
* `greet("maggie")` is invoked
  * It allocates a box of memory for the first function call
  * The argument `name` is set to `"maggie"` and saved to memory
    * the computer saves the values for all arguments in memory every time you invoke a function
* It logs `hello, maggie`
* `greet2("maggie")` is invoked and added to the TOP of the call stack
  * `greet("maggie")` has NOT yet been removed from the stack
  * memory is allocated for the value of the argument `name`
* It logs `how are you, maggie?`
*  `greet2("maggie")` returns and pops off the stack
  *  `greet("maggie")` is still on the stack
* It logs `getting ready to say bye`
* `bye` is invoked and added to the TOP of the call stack
  * `bye` sits on the stack above `greet("maggie")`
* It logs `okay, bye!`
* `bye` returns and pops off the stack
* `greet("maggie")` finally returns and pops off the stack
* THE STACK IS EMPTY
