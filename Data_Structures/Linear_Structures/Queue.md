# Queue 
- what is a queue 
  - linear data structure which models real world queues by having 2 primary operations 
    - enqueue or dequeue 
  - front and back end 
  - first in, first out (**FIFO**)
- terminology 
  - enqueue = adding = offering 
  - dequeue = polling (and removing)
- when/where to use them 
  - waiting line models a queue 
  - efficiently keep track of x most recently added elements 
  - web server request management (first come, first served)
  - breadth first search 
- complexity 
  - enqueue O(1)
  - dequeue O(1)
  - peeking O(1)
  - contains O(n)
  - removal O(n)
  - is empty O(1)
- breadth first search example 
  - add starting node to queue 
  - mark starting node as visited 
  - for every neighbor of the visited, if not visited, add to queue 
  - rinse and repeat 
- implementation details 
  - popular methods: arrays, singly linked list, doubly linked list 

```JS
class Queue { 
  constructor(){ 
    this.items = []; 
  } 

  enqueue(element){     
    this.items.push(element); 
  }

  dequeue(){ 
    if(this.isEmpty()) 
      return "Underflow"; 
    return this.items.shift(); 
  } 

  front(){ 
    if(this.isEmpty()) 
      return "No elements in Queue"; 
    return this.items[0]; 
  } 

  isEmpty(){ 
    return this.items.length === 0; 
  } 

  printQueue(){ 
    let str = ""; 
    for(var i = 0; i < this.items.length; i++) 
      str += this.items[i] +" "; 
    return str; 
  } 

} 
``` 