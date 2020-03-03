## Shortest Path Problem
* What is the smallest/shortest way to get from point a to point b
* breadth-first-search solution

# Breadth-First Search
* search through all adjacent nodes
* if none of the nodes are what you're looking for, search through all of that node's adjacent nodes
* check _ALL_ first-degree connections before expanding into second-degree connections
  * only check nodes in the order in which they are added to the list
* don't check nodes that have already been checked 

### Big O
* Running time is at least O(number of edges)
* Adding a node to the queue takes constant time _O(1)_
* Commonly written as O(n+e) (or O(v+e) for vertices)

### Pseudocode
* keep a queue containing the nodes to check
* pop a node off the queue
* check if this node fulfills what we're looking for f
  * yes: done
  * no: add all of their neighbors to the END of the queue
* loop
* if the queue is empty, no nodes fulfill what we're looking for

## Implementation

```JS
bfs(graph, startingNode){
  let queue = []
  //when the value of the node is an array
  queue = queue.concat(graph[startingNode])
  let visited = []
  while(queue.length){
    let node = queue.shift()
    // if not in the visited array, it will return -1
    if(visited.indexOf(node) === -1){
      if(fnThatChecksSomething(node)){
        console.log('found it')
        return true
      } else {
        queue = queue.concat(graph[node])
        visited.push(node)
      }
    }
  }
  return false
}
```
