- Changes every time the execution context is changed
- By default, the execution context for an execution is global
- Function call methods pass this explicitly
  - it takes this as a value as its first argument
  - treats further arguments as normal parameters
- *Arrow functions are different*  
  - they do not bind their own this
  - can see the this binding of the scope around them
