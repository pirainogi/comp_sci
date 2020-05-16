# Stack 
- what is a stack 
  - one-ended linear data structure that models a real-world stack 
  - push and pop operations 
  - last in, first out (LIFO)
- where is it used 
  - undo mechanisms in text editors 
  - compiler syntax checking for matching brackets/braces 
  - model piles of books/plates 
  - behind the scenes to support recursion by keeping track of previous function calls 
  - Depth-First-Search on a graph 
- complexity (with a linked list)
  - pushing O(1)
  - popping O(1)
  - peeking O(1)
  - searching O(n)
  - size O(1)
- example 
  - brackets 
    - use a stack 
    - push on for { or [ or ( 
    - pop off reverse of } or ] or ) in top of stack 
    - if not, invalid 
  - tower of hanoi 
    - move all disks to the right most peg without putting a larger disk onto a smaller disk 
- usage 
- implementation 

```JS
class Stack { 
  constructor(){ 
    this.items = []; 
  } 

  push(element){ 
    this.items.push(element); 
  } 

  pop(){ 
    if (this.items.length == 0) 
      return "Underflow"; 
    return this.items.pop(); 
  } 

  peek(){ 
    return this.items[this.items.length - 1]; 
  }

  isEmpty(){ 
    return this.items.length == 0; 
  } 

  printStack(){ 
    let str = ""; 
    for (var i = 0; i < this.items.length; i++) 
      str += this.items[i] + " "; 
    return str; 
  } 

} 
```

```JS
//with a singly linked list 
//pushing new elements on mean that the head is going to change every time 
//popping elements off mean the head adjusts to the next node and prev node is deleted 
```