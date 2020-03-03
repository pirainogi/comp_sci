# Dijkstra Algorithm
* Fastest Path algorithm
  * find the "cheapest" node
  * update the costs of the neighbors of this node
  * repeat until visited every node
  * calculate final path
  * based on the weight of every edge; not the shortest number of edges
* only works with **DIRECTED, ACYCLIC GRAPHS that are weighted**
* can't use Dijkstra's algorithm on graphs with negative weights
  * Bellman-Ford algorithm handles these

## Pseudocode
* make a table to track the cost for every node
  * cost is how expensive it is to get to
* also need to track the parent
* find the cheapest neighbor for the starting node
* find the cost to get to the neighbors of the cheapest node
  * set the intermediary node as the parent
* go back to other neighbors of the starting node
* update the value of all of its neighbors
* rinse and repeat until you reach the destination node
* determine the path by following the parents backwards

## Implementation
```JS
const dijkstra = (graph) => {
  //track lowest code to reach every node
  const costs = Object.assign({finish: Infinity}, graph.start)
  //track the paths
  const parents = {finish: null}
  for(let child in graph.start){
    parents[child] = 'start'
  }
  //track visited nodes
  const visited = []

  let node = lowestCostNode(costs, visited)
  
  while(node){
    let cost = costs[node]
    let children = graph[node]
    for(let n in children){
      let newCost = cost + children[n]
      if(!costs[n]){
        costs[n] = newCost
        parents[n] = node
      }
      if(costs[n] > newCost){
        costs[n] = newCost
        parents[n] = node
      }
    }
    visited.push(node)
    node = lowestCostNode(costs, visited)
  }

  let optimalPath = ['finish']
  let parent = parents.finish
  while(parent){
    optimalPath.push(parent)
    parent = parents[parent]
  }
  optimalPath.reverse()

  const results = {
    distance: costs.finish
    path: optimalPath
  }
  return results
}

const lowestCostNode = (costs, visited) => {
  return Object.keys(costs).reduce((lowest, node) => {
    if(lowest === null || costs[node] < costs[lowest]){
      if(!visited.includes(node)){
        lowest = node
      }
    }
    return lowest
  }, null)
}
```
