# Reconciliation
- React provides a declarative API so that you don't have to worry about exact changes on every update

## Motivation
- when you use react, at a single time you can think of the `render()` function as creating a tree of React elements
- on next state or props update, `render()` function will return a different tree of React elements
  - efficiently update the UI to match the most recent tree
- state of the art algorithms to generate the minimum number of operations to transform one tree into another is O(n<sup>3</sup>)
