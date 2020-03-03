# Hash Functions
* Data is stored (or "mapped") as key-value pairs
  * value always needs to be consistent
  * every key should map to a distinct value  
  * values are stored in an array and the function points to the index of the value that is associated with that key
* Collisions
  * if the hash function assigns the same index position in the array to multiple keys, it creates a linked list in that slot
  * required to search through the linked list in that slot in order to find the correct key and associated value

# Hash Table
* combination of a hash function and an array
* also known as hash map, maps, dictionaries, and assoc. arrays
* constant time lookup
  * worst case: slow at search, insertion, and deletion
  * based on collisions 
  * prevented with low load factor and good hash function
    * load factor: number of items in hash table/number of slots
    * if load factor is over 1, you have more items than slots in your array
    * when load factor increases, more slots are needed (resizing)
      * create a new array that is twice the size
      * reinsert all of the original items into the new hash table
      * load factor is lowered and will perform better
      * ideal time to resize is when load factor is greater than 0.7

* filters out dups
* also used as a cache storage system
  * only do the work if the requested value isn't in the cache already
