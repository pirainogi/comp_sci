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
* filters out dups
* also used as a cache storage system
  * only do the work if the requested value isn't in the cache already
