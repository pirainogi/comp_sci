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
  * variables inside will be available even after the outer function has finished running
* data privacy

```JS
const counter = function counter(){
  let count = 0
  return {
    getCount: function getCount(){
      return count
    },
    increment: function increment(){
      count += 1
    }
  }
}
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
