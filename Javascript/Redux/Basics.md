# Basics

## Actions
* **Actions** are payloads of information that send data from your application to your store
  * _only_ source of information for the store
  * `store.dispatch()`
* POJOs (plain old JS objects)
* _must_ have a type property
  * defined as string constants
  * move to a separate file/module when app is sufficiently large and import
* pass as little info as possible

```JS
const ADD_TODO = "ADD_TODO"

{
  type: ADD_TODO,
  text: 'Build my first Redux App'
}
```

## Action Creators
* functions that create actions
* can be async 
```JS
function addTodo(text){
  return {
    type: ADD_TODO,
    text
  }
}
```
* to initiate a dispatch, pass the result to the dispatch() function
  * `dispatch()` can be accessed directly from the store as `store.dispatch()`
  * also access via `connect()`
```JS
dispatch(addTodo(text))
```
