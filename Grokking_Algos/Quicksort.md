# Quicksort
* sorting algorithm
* much faster than selection sort and frequently used
* base case
  * arrays that don't need to be sorted (0 or 1 element )
* recursive case
  * pick an element from the array (**pivot**)
    * first item in the array
  * partition the array
    * find the elements that are smaller than the pivot
      * create a sub-array of these numbers
    * find elements that are larger than the pivot
      * create a sub-array of these numbers
  * call quicksort on the sub-arrays and then combine the results

### Example
`[33, 15, 10]`
* `33` is the pivot
* numbers smaller: `[15, 10]`
* numbers greater: `[]`
* left array + pivot + right array
* call the recursive case again for the sub-arrays
  * `quicksort([15, 10]) + [33] + quicksort([])`
  * `[10, 15, 33]`

## Algorithm
```JS
function quicksort(array){
  if(array.length < 2){
    return array
  }
  else {
    let pivot = array[0]
    let less = [], greater = []
    for(let i = 1; i < array.length; i++){
      if(array[i] <= pivot){
        less.push(array[i])
      } else if(array[i] > pivot){
        greater.push(array[i])
      }
    }
  return [...quicksort(less), pivot, ...quicksort(greater)]
  //return quicksort(less).concat(pivot).concat(quicksort(greater))
  }
}
```

## Big O
* Worst case: O(n<sup>2</sup>)
* Average case: O(n log n)
