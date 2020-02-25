### Selection Sort  
* You want to sort a list of artists with their play count to determine your favorite artists
  * Go through the original list and find the most-played artist
    * Add it to a new list
    * Remove from the first list
  * Rinse and repeat until new list is sorted and complete
* O(n<sup>2</sup>) run time
  * Takes O(n) to check the first list for the most played artist through n artists
  * You have to complete this n times for the length of the list

```JS
function findSmallest(array){
  let smallest = array[0], smallest_index = 0
  for(let i = 0; i < array.length; i++){
    if(array[i] < smallest){
      smallest = array[i]
      smallest_index = i
    }
  }
  return smallest_index
}

function selectionSort(array){
  let newArr = [], length = array.length
  for(let i = 0; i < length; i++){
    let smallest_index = findSmallest(array)
    newArr.push(array[smallest_index])
    array.splice(smallest_index, 1)
  }
  return newArr
}
```
