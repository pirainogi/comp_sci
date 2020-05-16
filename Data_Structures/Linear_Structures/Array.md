# Arrays 
- what is an array 
  - fixed-length container containing n elements indexable from the range 
    - indexable: slot/index can be referenced by number 
  - contiguous chunks of memory 
- when/where is an array used 
  - storing and accessing sequential data 
  - temporarily storing objects 
  - IO routines as buffers 
  - lookup tables/inverse lookup tables
  - return multiple values from a function 
  - dynamic programming to cache answers to subproblems 
- complexity 
  - access: O(1)
  - search: O(n)
  - insertion/appending/deletion (static): n/a
  - insertion/deletion (dynamic): O(n)
    - shift and recopy 
  - appending (dynamic): O(1)
- static array usage 
  - array indexing is 0-based 
  - iterated over with `for-each` loop 
- dynamic array implementation 
  - grow or shrink in size 
  - use a static array 
    - create a static array with an initial capacity 
    - add elements to the udnerlying static array 
    - if adding an element exceeds the current capacity, double the capacity of the array and copy everything over 

```JS
class Array{ 
  constructor(){ 
    this.length=0; 
    this.data={}; 
  } 

  size(){
    return this.length
  }

  getElementAtIndex(index){ 
    return this.data[index]; 
  } 

  push(element){ 
    this.data[this.length]=element; 
    this.length++; 
    return this.length; 
  } 

  pop(){ 
    const item= this.data[this.length-1]; 
    delete this.data[this.length-1]; 
    this.length--; 
    return this.data; 
  } 

  deleteAt(index){ 
    for(let i=index; i<this.length-1;i++){ 
      this.data[i]=this.data[i+1]; 
    } 
    delete this.data[this.length-1]; 
    this.length--; 
    return this.data; 
  } 

  insertAt(item, index){ 
    for(let i=this.length;i>=index;i--){ 
      this.data[i]=this.data[i-1]; 
    } 
    this.data[index]=item; 
    this.length++; 
    return this.data; 
  } 

} 
```