# Queue
* **FIRST IN, FIRST OUT**
* cannot access random elements in the Queue
* only two operations:
  * enqueue
  * dequeue

```JS
class Queue {
  constructor(){
    this.items = []
  }

  isEmpty(){
    return this.items.length === 0
  }

  enqueue(data){
    this.items.push(data)
  }

  dequeue(){
    if(this.isEmpty()){
      return "nothing to dequeue"
    } else {
      return this.items.shift()
    }
  }

  front(){
    if(this.isEmpty()){
      return "nothing in the queue"
    } else {
      return this.items[0]
    }
  }

  printQueue(){
    return this.items.join(", ")
  }
  
}
```
