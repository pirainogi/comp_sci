### Computer Memory
* every slot in memory can hold one element
* every slot in memory has an address
* if you want to store multiple items, arrays and lists are the most basic options

### Arrays
* RANDOM ACCESS
  * read the elements in any order
* An array stores elements in contiguous slots in memory
  * Because of this, every time your array grows beyond the number of available contiguous slots, the entire array has to move to the next point in memory that has enough contiguous slots
* Possible to hold extra slots than necessary
  * Con: wastes slots on that aren't being used
* Because every element is contiguous in memory, you can read any element in the array by asking for the index number of that element  
* Arrays index at 0

### Linked Lists
* SEQUENTIAL ACCESS
  * reading the elements one by one
* Each element in the list stores the address of the next item
* Elements can fit into any slot; not contiguous slots
* Because LLs aren't contiguous, you must traverse the linked list to find a specific element

### Run Times
* Arrays
  * Reading: O(1) > Constant Time  
  * Writing/Insertion: O(n) > Linear Time
  * Deletions: O(n) > Linear Time
* Linked Lists
  * Reading: O(n) > Linear Time  
  * Writing/Insertion: O(1) > Constant Time
    * Better for inserting elements into the middle (only have to change the pointer)
  * Deletions:  O(1) > Constant Time
