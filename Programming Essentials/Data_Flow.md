## Two-way binding
- UI fields are bound to model data dynamically such that when a UI field changes, the model data changes with it and vice-versa
- Causes an issue with Browser performance, as applications scale
- Keeping track of data flow also becomes a problem
- Angular allows user input to directly modify what appears on the screen

## One-way data flow
- Model is the single source of truth
- Changes in UI trigger messages that signal user intent to the model
  - “store” in Redux)
- Data always flows in a single direction
- Build out presentational components  and wrapping them in Connect containers
- React does this natively, because React does not have a mechanism to allow the HTML to change the component.
  - The HTML can only raise events that the component can respond to. 
- One-way data binding means that React is more performant than Angular
- Redux is one such way to maintain this: Action → Dispatcher → Store → View
  - Action: “Change name to Jack”
  - Dispatcher: carries our action
  - Store: logs change
  - View: “Hi, Jack!”
