# Virtual DOM
![react docs: virtual dom](https://reactjs.org/docs/faq-internals.html)
- VDOM is an ideal or virtual representation of a UI is kept in memory and synced with the real DOM by a library (such as ReactDOM)
  - reconciliation
- enables the declarative API of React
  - tell React what state you want the UI to be in and it makes the DOM match that state
  - abstracts out the attribute manipulation, event handling, and manual DOM updating
- VDOM is usually associated with React elements (objects representing the user interface)
  - also uses internal objects ("fibers") to hold additional information about the component tree

- **Shadow DOM and Virtual DOM are not the same thing**
  - Shadow DOM is a browser technology designed primarily for scoping variables and CSS in web components
  - virtual DOM is a concept implemented in libraries in JS on top of browser APIs

![real benefits of the virtual dom in react.js](https://www.accelebrate.com/blog/the-real-benefits-of-the-virtual-dom-in-react-js/)
- Updating the DOM (Document Object Model) is inefficient and slow
- React's Virtual DOM is more efficient

### UI Library  
- two primary ideas of reactive programming:
  1. systems should be event-driven
  2. responsive to state changes  
- DOM's UI components have internal state and updating the browser isn't as simple as regenerating the DOM whenever something changes
- **statefulness** is why we need UI libraries and solutions
  -  Ember uses key-value observation
  - Angular uses dirty checking
- handle watching for changes to the data model and updating the correct part of the DOM when these changes occur, or watching for changes in the DOM and updating the data model when they occur
  - two-way binding

### Why React
- Write pure JS that updates React components and React updates the DOM for you
  - data binding isn't intertwined in the application
- **one-way binding**
  - typing in an input field doesn't directly change the state of that component
  - it updates the data model, which causes the UI to be updated and the text you typed into the field appears in the field

### DOM Speed
- DOM is fast
  - adding and removing DOM nodes doesn't take more than setting a property on a JS object
  - simple operation
- Browser load is slow
  - recalculate the CSS
  - do layout
  - repaint the webpage
- Shortening the time to repaint the screen would increase efficiency
  - minimize and batch the DOM changes that make redraws necessary

### Virtual DOM
- node tree that lists elements and their attributes and content as objects and properties
- `render()` method creates a node tree from React components and updates this tree in response to mutations in the data model, caused by actions
- data change incites a new VDOM representation of the UI is created
  - entire UI will be rerendered in a new VDOM representation
  - difference between the prev VDOM and the new one is calculated
  - real DOM will be updated with what has actually changed (PATCH)

### Virtual DOM Speed
- rendering the VDOM is faster than rendering a UI in the actual browser
- user can't see the VDOM
  - VDOM calculates the different between changes and only updates what needs to be updated
- React attaches attributes to elements in your document and manipulates them individually (using specific ID attributes) after doing the diff to determine what needs updating
  - VDOM inserts addl steps into the process, but elegantly handles minimal updates to the browser window
- VDOM adds a layer of scripting on top of whatever optimizations  the browser has already made in order to make these minimized DOM manipulations transparent to the developer
  - abstraction makes React more CPU-intensive

### How to Use VDOM
- each change to the data model can trigger a complete refresh of the virtual user interface
  - different from other libraries that observe aspects of the document and update them when necessary
  - VDOM uses less memory than other systems because it doesn't need to hold observables in memory
  - inefficiencies when comparing two entire VDOMs each time an action occurs
- Devs need to tell React not to analyze components that will have no change depending on action
  - save resources and speed up application
