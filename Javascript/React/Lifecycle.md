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

# Updating
## Render Phase
### `getDerivedStateFromProps()`
### `shouldComponentUpdate()`
### `render()`
## Precommit Phase
### `getSnapshotBeforeUpdate()`
## Commit Phase
### `componentDidUpdate()`

# Unmounting
## Commit Phase
### `componentWillUnMount()`
