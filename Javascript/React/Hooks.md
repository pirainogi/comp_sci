# Hooks
* New as of React 16.8
* let you use state and other React features without writing a class
  * opt-in
  * backwards compatible
  * no plans to remove classes from react
* react doesn't have a way to attach reusable behavior to a component
  * render props and higher-order components try to solve, but requires component restructure
  * **hooks allow you to use stateful logic without changing component hierarchy**
    * you can split up one component into smaller functions based on what pieces are related (ie. setting up a subscription or fetching data) rather than forcing a split with lifecycle methods (`useEffect()`)
  * classes are hard
    * hooks let you use more of react without classes
* hooks are functions that let you 'hook' into react state and lifecycle methods inside functional components
  * few built-in methods but you can also create your own Hooks to reuse stateful behavior btw components

Example:
```JS
import React, { useState } from 'react';

function Example() {
  //declare a new state variable, which we'll call 'count'
  const [count, setCount] = useState(0)

  return(
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  )
}
```
## State Hook
* `useState()` is a Hook
  * call it inside a function component to add local state
  * react preserves this state btw rerenders
* returns a pair of values: 1. current state value and 2. function that lets you update it
  * function is similar to `this.setState()` except it doesn't merge the old and new state together
* **argument is the initial state**
* array destructuring syntax allows us to give different names to the state variables declared by calling `useState()`
  * react assumes that if you call `useState()` many times, you do it in the same order during every render
* can call on the state directly
  * `{count}` in the above example
* to update state, use the function and pass in new state value as argument
  * `setCount(count + 1)`

## Effect Hook
* side effects: data fetching, subscriptions, or manually changing the DOM into react components
  * those that require cleanup
  * those that don't require cleanup
    * network requests, DOM manipulations, logging
* `useEffect()` adds the ability to perform side effects from a functional component
  * serves the same purpose as `componentDidMount()`, `componentDidUpdate()`, and `componentWillUnMount()`
  * react remembers the function passed and call it later after performing the DOM updates
* called inside the component because we have access to state variables/props from the effect
  * JS closure
* runs after **every** render (even first)
  * `useEffect()` will be different on every render
  * read the state value from inside the effect without it going stale
  * schedule a different effect every time we render (replaces the previous--each effect "belongs" to a particular render

```JS
import React, { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0)

  useEffect(() => {
    document.title = `You clicked ${count} times`
  })

  return(
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  )
}
```
* in the above example, you're telling react to run your effect function after flushing changes to the DOM
  * in order to skip applying an effect if values haven't changed between renders, pass an array as an optional second argument
  ```JS
  useEffect(() => {
    document.title = `You clicked ${count} times`
  }, [count])
  ```
  * make sure the array includes all values from the component scope (props/state) that change over time and are used by the effect
    * if you want to run an effect and clean it up only once (mount and unmount), pass  in an empty array
    * effect doesn't depend on any values from props/state so it never needs to re-run


```JS
import React, { useState, useEffect } from 'react';

function FriendStatus(props){
  const [isOnline, setIsOnline] = useState(null)

  function handleStatusChange(status){
    setIsOnline(status.isOnline)
  }

  useEffect(() => {
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange)
    return () => {
      ChatAPI.unsubscribeToFriendStatus(props.friend.id, handleStatusChange)
    }
  })

  if(isOnline === null){
    return 'Loading...'
  }
  return isOnline ? 'Online' : 'Offline'

}
```
* in the above, react unsubscribes from `ChatAPI` when the component unmounts, as well as before rerunning the effect due to a subsequent render
* can use more than a single effect in a component (like `useState()`)

```JS
import React, { useState, useEffect } from 'react';

function FriendStatusWithCounter(props){
  const[count, setCount] = useState(0)

  useEffect(() => {
    document.title = `You clicked ${count} times`
  })

  const [isOnline, setIsOnline] = useState(null)

  function handleStatusChange(status){
    setIsOnline(status.isOnline)
  }
//etc
}
```
* hooks let you organize side effects in a component by what pieces are related, rather than forcing a split based on lifecycle methods

## Rules of Hooks
* only call Hooks at the top level
  * not inside of loops, conditions, or nested functions
  * you can put conditions inside of a hook instead 
* only call Hooks from react function components
  * don't call from regular JS functions

## Building Your Own Hooks
* abstract the logic needed into a custom Hook

```JS
import React, { useState, useEffect } from 'react';

function useFriendStatus(friendID){
  const [isOnline, setIsOnline] = useState(null)

  function handleStatusChange(status){
    setIsOnline(status.isOnline)
  }

  useEffect(() => {
    ChatAPI.subscribeToFriendStatus(friendID, handleStatusChange)
    return () => {
      ChatAPI.unsubscribeToFriendStatus(friendID, handleStatusChange)
    }
  })

  return isOnline
}
```
* takes in a `friendID` and returns whether they're online or not

```JS
function FriendStatus(props){
  const isOnline = useFriendStatus(props.friend.id)

  if(isOnline === null){
    return 'Loading...'
  }
  return isOnline ? 'Online' : 'Offline'
}

function FriendListItem(props){
  const isOnline = useFriendStatus(props.friend.id)

  return (
    <li style={{ color: isOnline ? 'green' : 'black'}}>
      {props.friend.name}
    </li>
  )
}
```
* the state of these components is independent
* each call to a Hook has a completely isolated state
  * could use the same custom Hook twice in the same component
* convention is to add `use` before the name of the Hook component

## Other Hooks
* `useContext()`
  * lets you subscribe to react context without introducing nesting

```JS
function Example(){
  const locale =  useContext(LocaleContext)
  const theme = useContext(ThemeContext)
  //etc
}
```

* `useReducer()`
  * lets you manage local state of complex components with a reducer

```JS
function Todos(){
  const [todos, dispatch] = useReducer(todosReducer)
  //etc
}
```
