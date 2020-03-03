# Graphs
* Models a set of connections
* Made up of nodes and edges
  * node holds data
  * edge connects 2 nodes
* two nodes that are directly connected are called _neighbors_

## Implementation
```JS
class Graph {

  //noOfNodes stores the number of nodes in the graph
  //AdjList stores an adjacency list of a particular node
  constructor(noOfNodes){
    this.noOfNodes = noOfNodes
    this.AdjList = new Map;
  }

  addNode(data){
    //initialize the adjacency list with a null array
    //will eventually hold all of the nodes it is connect to via edges
    this.AdjList.set(data, [])
  }

  addEdge(node1, node2){
    //push the opposite node into each other's adjacency list 
    this.AdjList.get(node1).push(node2)
    this.AdjList.get(node2).push(node1)
  }

  printGraph(){
    //set a variable equal to a list of all of the nodes in the graph
    const keys = this.AdjList.keys()
    //loop through all of the nodes
    for(let node of keys){
      //get the adjacent nodes
      let values = this.AdjList.get(node)
      let conc = ""
      //for every adjacent node, loop over them and concatenate them into a string
      for(let adjacent of node){
        conc += adjacent + " "
        //print the node and the adjacency list
        console.log(node + "->" + conc)
      }
    }
  }

}

```
