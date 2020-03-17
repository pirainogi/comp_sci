# React Fiber Architecture

## Background
- goal: increase suitability for areas like animation, layout, gestures
- headline feature is _incremental rendering_
  - ability to split rendering work into chunks and spread it out over multiple frames
- ability to pause, abort, or reuse work as new updates come in
- ability to assign priority to different types of updates
- new concurrency primitives

- central idea of React's API is to think of updates as if they cause the entire app to rerender
  - allows the developer to reason declaratively
  - don't have to worry about how to efficiently transition the  app from  any particular state to another
- re-rendering the whole app on each change is prohibitively costly in terms of performance
- React has optimizations that create the _appearance_ of whole-app re-rendering while maintaining performance
  - **reconciliation**

### Reconciliation  
- algorithm that React uses to diff one tree to another to determine what parts need to be changed
- process:
  - when you render a React app, a tree of nodes that describes the app is generated and saved in memory
  - tree is flushed to the rendering environment
    - in the browser, it's translated to a set of DOM operations
  - when updated, a new tree is generated
  - new tree is diffed to the previous tree to compute which operations are needed to update the rendered app
- ground-up rewrite of the  reconciler
- key points:
  - different component types are assumed to generate substantially different trees
    - React won't diff
    - React will replace the old tree completely

##### Update  
- change in the data used to render a React app
- usually the result of `setState()`
- eventually results in a rerender

#### Reconciliation vs Rendering
- different phases
- reconciler does the work of computing which parts of a tree have changed
- renderer uses that information to actually update the rendered app
- React and RN use their own renderers while sharing the same reconciler
- Fiber reimplements the reconciler
  - not primarily concerned with rendering but renderers need to change to support new architecture

### Scheduling
##### Scheduling
- the process of determining when work should be performed

##### Work
- any computations that must be performed
- usually the result of an update (`setState`)

- React walks the tree recursively and calls render functions of the whole updated tree during a single tick
  - might  start delaying some updates to avoid dropping frames
- computations are delayed until necessary
- if something is offscreen, possible to delay any logic related  to it
- if data arrives faster than frame rate, React will coalesce and batch the updates
- prioritize work coming from user interactions over background work (re-rendering new content just loaded from the network)

- key points:
  - not necessary for every update to be applied immediately
    - when applied immediately, it can be wasteful and cause frames to drop and degrade the user experience
  - different types of updates have different priorities
  - React uses a "pull-based" approach, the framework is smart enough to know how to schedule work
    - React currently re-renders the entire subtree when it recognizes an update

## Fibers
- goals
  - pause work and come back later
  - assign priorities to different kinds of work  
  - reuse previously completed work
  - abort work if unnecessary

##### a fiber is a unit of work

- using a React app is akin to calling a function whose body contains calls to other functions
- computers track a program's execution using the _call stack_
  - when a function is executed, a new stack frame is added to the stack
  - stack frame represents the work that is performed by that action 
- when dealing with UIs, if too much work is executed at once, animations can drop frames and loo
