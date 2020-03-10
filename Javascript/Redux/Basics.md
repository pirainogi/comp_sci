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

## Reducers
* Specify how the application's state changes in response too actions sent to the store

### Designing State Shape
* state is stored in a single object
* likely need to store data and UI state in the tree (try to keep it separate)
```JS
{
  visibilityFilter: 'SHOW_ALL',
  todos: [
    {
      text: 'Consider using Redux',
      completed: true
    },
    {
      text: 'Keep all state in a single tree',
      completed: false
    }
  ]
}
```

### Handling Actions
* reducer is a _pure_ function that takes the previous state and an action, returns the next state
```JS
(prevState, action) => nextState
```
* never mutate arguments
* never perform side effects (API calls or routing transitions)
* call non-pure functions (`Date.now()` or `Math.random()`)
```JS
import {
  SET_VISIBILITY_FILTER,
  ADD_TODO,
  TOGGLE_TODO
  VisibilityFilters
} from './actions'

const initialState = {
  visibilityFilter: VisibilityFilters.SHOW_ALL,
  todos: []
}

/*function todoApp(state, action){
  if(typeof state === 'undefined'){
    return initialState
  }
  return state
}*/

function todoApp(state = initialState, action){
  switch(action.type){
    case SET_VISIBILITY_FILTER:
      return Object.assign({}, state, {
        visibilityFilter: action.filter
      })
    case ADD_TODO:
      return Object.assign({}, state, {
        todos: [
          ...state.todos,
          {
            text: action.text,
            completed: false
          }
        ]
      })
    case TOGGLE_TODO:
      return Object.assign({}, state, {
        todos: state.todos.map((todo, index) => {
          if(index === action.index){
            return Object.assign({}, todo, {
              completed: !todo.completed
            })
          }
          return todo
        })
      })
    default:
      return state
  }
}
```
* do not mutate state
  * create a copy (empty object first)
  * can also use spread operator: `{...state, ...newState}`
  * return a new object
    * new object created using the data from the action
* return the previous state in the `default` case

### Splitting Reducers
* possible to split your reducer into multiple functions
```JS
function todos(state = [], action){
  switch(action.type){
    case ADD_TODO:
      return [
        ...state,
        {
          text: action.text,
          completed: false
        }
      ]
    case TOGGLE_TODO:
      return state.map((todo, index) => {
        if(index === action.index){
          return Object.assign({}, todo, {
            completed: !todo.completed
          })
        }
        return todo
      })
    default:
      return state
  }
}

function visibilityFilter(state = SHOW_ALL, action){
  switch(action.type){
    case SET_VISIBILITY_FILTER:
      return action.filter
    default:
      return state
  }
}

function todoApp(state = {}, action){
  return {
    visibilityFilter: visibilityFilter(state.visibilityFilter, action),
    todos: todos(state.todos, action)
  }
}

/*
function todoApp(state = initialState, action){
  switch(action.type){
    case SET_VISIBILITY_FILTER:
      return Object.assign({}, state, {
        visibilityFilter: action.filter
      })
    case ADD_TODO:
      return Object.assign({}, state, {
        todos: todos(state.todos, action)
      })
    case TOGGLE_TODO:
      return Object.assign({}, state, {
        todos: todos(state.todos, action)
      })
    default:
      return state
  }
}
*/
```
* in order to combine your reducers, use Redux's utility `combineReducers()`
  * handles the `todoApp()` functionality in the above
```JS
import { combineReducers } from 'redux'

const todoApp = combineReducers({
  visibilityFilter,
  todos
})

export default todoApp

//ES6
/*
import { combineReducers } from 'redux'
import * from reducers from './reducers'

const todoApp = combineReducers(reducers)
*/
```
