# Reconciliation
- React provides a declarative API so that you don't have to worry about exact changes on every update

## Motivation
- when you use react, at a single time you can think of the `render()` function as creating a tree of React elements
- on next state or props update, `render()` function will return a different tree of React elements
  - efficiently update the UI to match the most recent tree
- state of the art algorithms to generate the minimum number of operations to transform one tree into another is O(n<sup>3</sup>)
  - 1000 elements would require one billion comparisons
- O(n) algorithm:
  - two elements of a different type will produce different trees
  - developer can hint at which child elements may be stable across different renders with `key` prop

## Diffing Algorithm
- when diffing two trees, react first compares the two root elements
  - behavior different depending on types of the root elements

### Elements of Different Types
- when root elements have different types, React will tear down the old tree and build a new tree from scratch
  - `<a>` to `<img>` or `<Article>` to `<Comment>` etc
- old DOM nodes are destroyed
- component instances receive `componentWillUnmount()`
- when building new tree, DOM nodes are inserted into the DOM
- component instances receive `componentWillUnmount()` and then `componentDidMount()`
- any state associated with the old tree is lost
- any components below the root are unmounted and have their state destroyed

### Elements of the Same Type
- react looks at the attributes of both, keeps the same underlying DOM node, and only updates the changed attributes
- react recurses the children

### Components of the Same Type
- when a component updates, the instance stays the same so that the state is maintained across renders
- react updates the props of the underlying component instance to match the new element and calls `componentWillReceiveProps()` and `componentWillUpdate()` on the underlying instance
- `render()` is called and the diff algorithm recurses on the previous result and the new result

### Recursing on Children
- By default: React iterates over both lists of children at the same time and generates a mutation whenever there is a difference
- add a new element at the end of a list instead of inserting in the beginning because the entire subtree will be remade even though some nodes are the same as previously

## Keys
- when children have keys, React uses the key to match children in the original tree with children in the subsequent tree
- adding keys resolves the above inefficiency
- unique key
- key only needs to be unique among its siblings, not globally unique
- reorders cause issues with component state when indexes are used as keys
  - component instances are updated and reused based on their key
  - if a key is an index, moving an item changes it
  - component state for uncontrolled inputs can get mixed up and updated in unexpected ways

## Tradeoffs
- reconciliation algorithm is an implementation detail
- react could rerender the whole app on every action
  - rerender means calling `render()` for all components, not unmounting and remounting
- algorithm will not try to match subtrees of different component types
  - if you're alternating between two component types with similar output, may want to make the same type (in practice, not an issue)
- keys should be stable, predictable, and unique
  - unstable keys will cause many component instances and DOM nodes to be unnecessarily recreated
  - performance degredation and lost state in child components 
