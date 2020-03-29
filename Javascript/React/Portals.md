# Portals
* first-class way to render children into a DOM node that exists outside the DOM hierarchy of the parent component
```JS
ReactDOM.createPortal(child, container)
```
* first argument is any renderable React child (element, string, fragment)
* second argument is a DOM element

## Usage
* typically when you return element from component's `render()` method, it is mounted into the DOM as a child of the parent node
* may be useful to insert child into a different location
```JS
render(){
  // does not create new div
  // renders child into domNode - any valid DOM node regardless of its location i the DOM  
  return ReactDom.createPortal(
    this.props.children,
    domNode
  )
}
```
* typically used when parent component has `overflow: hidden` or `z-index` styling, but you need the child to visually break out of its container
  * dialogs, hovercards, tooltips

## Event Bubbling
* even though a portal can be anywhere in the DOM tree, it behaves like a normal React child in every way
* context works exactly the same regardless of whether the child is a portal
  * _portal still exists in the React tree regardless of position in the DOM tree_
* event fired from inside a portal will propagate to ancestors in the containing React tree, even if those elements are not ancestors in the DOM tree

```HTML
<html>
  <body>
    <div id="app-root"></div>
    <div id="modal-root"></div>
  </body>
</html>
```

```JS
//sibling containers
const appRoot = document.getElementById('app-root')
const modalRoot = document.getElementById('modal-root')

class Modal extends React.Component {
  constructor(props){
    super(props)
    this.el = document.createElement('div')
  }

  // portal element is inserted into the DOM tree after the Modal's children are mounted
  // children are mounted on a DETACHED DOM NODE
  // if a child component requires to be attached to the DOM immediately when mounted, add state to Modal and only render the children when Modal is inserted into the DOM tree
  componentDidMount(){
    modalRoot.appendChild(this.el)
  }

  componentWillUnMount(){
    modalRoot.removeChild(this.el)
  }

  render(){
    return ReactDOM.createPortal(
      thiis.props.children,
      this.el
    )
  }

}

class Parent extends React.Component {
  constructor(props){
    super(props)
    this.state = {
      clicks: 0
    }
    this.handleClick = this.handleClick.bind(this)
  }

  //this will fire when the button in Child is clicked, updating the parent's state, even though the button isn't a direct descendant in the DOM
  handleClick(){
    this.setState(state => ({
      clicks: state.clicks + 1
    }))
  }

  render(){
    return(
      <div onClick={this.handleClick}>
        <p>Number of Clicks: {this.state.clicks}</p>
        <p>
          Open the DevTools to observe that the button is not a child of the div with the onClick handler
        </p>
        <Modal>
          <Child />
        </Modal>
      </div>
    )
  }
}

function Child(){
  //click event on this button will bubble up to the parent because there is no onClick attribute defined 
  return (
    <div className="modal">
      <button>Click</button>
    </div>
  )
}

ReactDOM.render(<Parent/>, appRoot)
```
