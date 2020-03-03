# Graphs
* Models a set of connections
* Made up of nodes and edges
  * node holds data
  * edge connects 2 nodes
* two nodes that are directly connected are called _neighbors_
* directed graph
  * the relationships are either one way or two way (but they have directions)
  * in a one-way relationship, node1 can be neighbors with node2 but not the opposite
  * represented with arrows
* undirected graph
  * relationships are always two way and both nodes are each other's neighbor
  * represented with lines 
* topographical sort
  * make an ordered list out of a graph
  * based on one-way relationships (directed)
* **TREES ARE A TYPE OF GRAPH**

## Implementation
* you could also use a hash instead of a map (map prevents duplicates)
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
