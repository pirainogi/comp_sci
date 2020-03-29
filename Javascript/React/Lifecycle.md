# Lifecycle Methds
* special methods on the component class to run some code when a component mounts or unmounts

# Mounting
## Render Phase
### `constructor()`
* if you don't initialize state and don't bind methods, don't need to implement `constructor()`
* called before component is mounted
* when implementing, call `super(props)` before any other statement
  * might be deprecated??
* initialize local state by assigning an object to `this.state`
* binding event handler methods to an instance
* should **not** call `setState()` in the constructor
  * assign `this.state` directly inside `constructor()`
  * **only** place you should assign `this.state` directly
* avoid side-effects or subscriptions inside `constructor()`
  * use `componentDidMount()` instead
* don't copy props inside your state
  * only use case is to intentionally ignore prop updates
  * force component to 'reset' state by changing the key
### `getDerivedStateFromProps()`
### `render()`
* only required method in a class component
* should examine `this.props` and `this.state` and return one of the following types
  * react elements
    * elements that instruct react to render a DOM node (`div`) or another user-defined component (`<MyComponent />`)
  * arrays/fragments
    * return multiple elements from render
  * portals
    * render children into a different DOM subtree
  * string/number
    * rendered as text nodes in the DOM
  * boolean/null
    * render nothing
* should be a pure function (doesn't modify state, returns the same result every time invoked, and doesn't directly interact with the browser)
* if interaction w browser needed, use `componentDidMount()` or other lifecycle methods

## Commit Phase
### `componentDidMount()`
* invoked immediately after a component is mounted (inserted into the tree)
* initialization that requires DOM nodes should go here
* good place to instantiate network requests or set up subscriptions
  * also need to unsubscribe in `componentWillUnMount()`
* can `setState()` immediately
  * will trigger an extra rendering, but it will happen before the browser updates the screen
    * guarantees that even though `render()` is called twice, user won't see the intermediate state
    * can cause performance issues
    * should assign initial state in `constructor()` instead

# Updating
## Render Phase
### `getDerivedStateFromProps()`
### `shouldComponentUpdate()`
* use to let react know if a component's output is not affected by the current change in state or props.
  * default behavior is to rerender on every state change
* invoked before rendering when new props/state are being received
* defaults to `true`
* method is noto called foor the initial render or when `forceUpdate()` is used
* only exists for performance optimizatioon
* **not** to be used to "prevent" a rendering
  * consider using built-in `PureComponent`
    * performs a shallow comparison of props/state and reduces the chances that you'll skip a necessary update
  * may want to compare `this.props` with `nextProps`, and `this.state` with `nextState` and return `false` to indicate to react the update can be skipped
    * false does **not** prevent child components from rerendering when their state changes
* not recommended to do deep equality checks or using `JSON.stringify()`
  * inefficient and will harm performance
* if `false` returned from this method, `UNSAFE_componentWillUpdate()`, `render()`, and `componentDidUpdate()` will not be invoked 
### `render()`
## Precommit Phase
### `getSnapshotBeforeUpdate()`
## Commit Phase
### `componentDidUpdate()`
* `componentDidUpdate(prevProps, prevState, snapshot)`
* invoked immediately after the updating occurs
* not called for the initial render
* opportunity to operate on the DM when the component has been updated
* good place for network requests as long as you compare current props to previous props (to prevent unnecessary network requests)
  * `componentDidUpdate(prevProps){ if(this.props.userID !== prevProps.user.ID){ this.fetchData(this.props.userID)}}`
* can call `setState()` immediately but it **must** be wrapped in a condition
  * otherwise it'll cause an infinite loop
  * will also cause extra re-rendering which, while not visible to the user, can affect the component performance
* if trying to mirror state to a prop coming from above, consider using the prop directly instead
* `componentDidUpdate()` will **not** be invoked if `shouldComponentUpdate()` returns `false`
* if component implements `getSnapshotBeforeUpdate()`, value it returns will be passed as a third "snapshot" parameter into `componentDidUpdate()`
  * otherwise, `undefined`

# Unmounting
## Commit Phase
### `componentWillUnMount()`
* invoked immediately before a component is unmounted and destroyed
* perform any necessary cleanup in this method
  * invalidate timers, cancel network requests, clean up subscriptions
* should **not** call `setState()` because the component will never be rerendered
* once unmounted, it will never be mounted again
