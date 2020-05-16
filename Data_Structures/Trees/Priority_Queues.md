# Priority Queues 
- what is a priority queue 
  - abstract data type 
  - operates similar to a normal queue but elements have a priority 
  - elements with higher priority are dequeued first 
  - only supports comparable data 
    - data inserted into the PQ must be able to be ordered in some way (either least to greatest or greatest to least)
    - need to be able to assign relative priorities to each element 
  - only guaranteed that next number in sequence is smallest of the current queue 
- what is a heap 
  - tree based data structure that satisfies the heap invariant (heap property): if a is a parent node of b, then a is ordered with respect to be for all nodes a, b in the heap 
  - binary heaps 
    - binary tree that supports the heap invariant 
    - two children for all parents 
    - complete binary tree is a tree in which at every level, except possibly the last, is completely filled and all possible nodes as far left as possible 
      - gives us an insertion point 
    - binary heap representation (array)
    ![binary heap representation with array](https://github.com/pirainogi/comp_sci/blob/master/0_img-resources/binary_heap_rep.png)
      - insertion position is the last position in the array 
      - let i be the parent node index 
        - left child: 2i+1 
        - right child: 2i+2 
  - binomial heaps 
    - any number of child branches 
  - max heap 
    - parent is greater than all children 
  - min heap 
    - parent is less than all children 
- when/where to use a priority queue 
  - use in certain implementations of Dijkstra's shortest path algorithm 
  - anytime you need to dynamically fetch the 'next best' or 'next worse' element 
  - used in huffman coding (lossless data compression)
  - best first search algos 
    - use PQs to continuously grab the next most promising node 
    - minimum spanning tree algorithms 
- how to turn a min priority queue into a max priority queue 
  - problem: most programming languages only provide min PQ but we might need a max PQ 
  - since elements in a PQ are comparable, they implement some sort of comparable interface which we can negate to achieve a max heap 
    - with numbers 
      - let x and y be numbers in the PQ 
      - for a min PQ, if x <= y, x comes out of the PQ before y 
      - negation is x >= y, then y comes out before x 
      - alternative: negate the number as you insert them into the PQ 
        - negate them again when they are taken out 
    - with strings 
      - lex is a comparator for strings which sorts them into lexicographic order 
      - let nlex be the negation of lex 
        - if s1 < s2 => -1 
          - nlex -(-1) => 1 
        - if s1 = s2 => 0 
          - nlex -(0) => 0 
        - if s1 > s2 => 1 
          - nlex -(1) => -1 
- complexity analysis 
  - binary heap construction O(n)
    - heap sort 
  - polling O(log(n))
  - peeking O(1)
  - adding O(log(n))
  - removing (naive) O(n)
    - linear scan and then remove 
  - advanced removing with hash table O(log(n))
  - naive contains O(n)
  - contains check with hash table O(1)
- binary heap priority queue implementation details 
  - heap sinking/swimming (sift down/up or bubble up/down)
    - heaps give us the best possible time complexity 
    - we could also use an unordered list for the same behavior but worse time complexity 
  - adding elements to a priority queue 
    - add element to the next available node 
      - if in violation of the min-heap 
        - swap node with parent 
        - rinse and repeat until no longer in violation 
  - removing elements from a priority queue 
    - remove the root value (highest priority)
      - called polling 
      - swap with the last element 
        - delete the original root 
        - bubble down 
          - select smallest child to swap (left for a tie)
          - rinse and repeat until no longer in violation 
    - remove any node 
      - scan through the tree until you fine the right node (left to right)
      - swap with the last node 
      - remove the node 
      - if in violation of the heap invariant 
        - bubble up until tree is balanced 
  - polling O(log(n))
  - removing O(n)
    - to improve the time complexity in O(log(n))
      - inefficiency comes from having to perform a linear search to find out where an element is indexed at 
      - use a hashtable for constant time lookup
      - what if multiple nodes with the same value 
        - instead of mapping one value to one position, one value to multiple position (set or tree set)
      - which element do we remove if a node is repeated in the heap, does it matter 
        - doesn't matter as long as the heap invariant is satisfied    
- implementation 

```JS
class MinHeap {
  constructor () {
    /* Initialing the array heap and adding a dummy element at index 0 */
    this.heap = [null]
  }

  getMin () {
    /* Accessing the min element at index 1 in the heap array */
    return this.heap[1]
  }

  insert (node) {
  /* Inserting the new node at the end of the heap array */
  this.heap.push(node)
  /* Finding the correct position for the new node */
  if (this.heap.length > 1) {
    let current = this.heap.length - 1
    /* Traversing up the parent node until the current node (current) is greater than the parent (current/2)*/
    while (current > 1 && this.heap[Math.floor(current/2)] > this.heap[current]) {
      /* Swapping the two nodes by using the ES6 destructuring syntax*/
      [this.heap[Math.floor(current/2)], this.heap[current]] = [this.heap[current], this.heap[Math.floor(current/2)]]
      current = Math.floor(current/2)
      }
    }
  }

  remove() {
    /* Smallest element is at the index 1 in the heap array */
    let smallest = this.heap[1]
    /* When there are more than two elements in the array, we put the right most element at the first position
        and start comparing nodes with the child nodes
    */
    if (this.heap.length > 2) {
      this.heap[1] = this.heap[this.heap.length-1]
      this.heap.splice(this.heap.length - 1)
      if (this.heap.length === 3) {
        if (this.heap[1] > this.heap[2]) {
            [this.heap[1], this.heap[2]] = [this.heap[2], this.heap[1]]
        }
        return smallest
      }
      let current = 1
      let leftChildIndex = current * 2
      let rightChildIndex = current * 2 + 1

      while (this.heap[leftChildIndex] &&
      this.heap[rightChildIndex] &&
      (this.heap[current] > this.heap[leftChildIndex] ||
      this.heap[current] > this.heap[rightChildIndex])) {
        if (this.heap[leftChildIndex] < this.heap[rightChildIndex]) {
          [this.heap[current], this.heap[leftChildIndex]] = [this.heap[leftChildIndex], this.heap[current]]
          current = leftChildIndex
        } else {
          [this.heap[current], this.heap[rightChildIndex]] = [this.heap[rightChildIndex], this.heap[current]]
          current = rightChildIndex
        }
        leftChildIndex = current * 2
        rightChildIndex = current * 2 + 1
      }
    }
    if (this.heap[rightChildIndex] === undefined && this.heap[leftChildIndex] < this.heap[current]) {
      [this.heap[current], this.heap[leftChildIndex]] = [this.heap[leftChildIndex], this.heap[current]]
    }
    /* If there are only two elements in the array, we directly splice out the first element */
    else if (this.heap.length === 2) {
      this.heap.splice(1, 1)
    } else {
      return null
    }
    return smallest
  }

}
```
[source code](https://blog.bitsrc.io/implementing-heaps-in-javascript-c3fbf1cb2e65)