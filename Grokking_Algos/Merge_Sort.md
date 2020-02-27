# Merge Sort
* Divide the array into 2 halves recursively
* Merge and sort the smaller arrays

```JS
function mergeSort(array){
  //base case
  if(array.length < 2){
    return array
  }
  // define the variables as arrays depending on the current midpoint
  const midpoint = Math.floor(array.length / 2)
  const left = array.slice(0, midpoint)
  const right = array.slice(midpoint)
  // defined elsewhere
  return merge(
    //recurisvely call mergeSort until all elements are halved into individual arrays
    mergeSort(left), mergeSort(right)
  )
}

function merge(left, right){
  let result = [], leftIndex = 0, rightIndex = 0

  // push the values into the results array in the right order
  while(leftIndex < left.length && rightIndex < right.length){
    if(left[leftIndex] < right[rightIndex]){
      result.push(left[leftIndex])
      leftIndex ++
    } else {
      result.push(right[rightIndex])
      rightIndex++
    }
  }
  //there will be one element remaining to the left or right so we need to add them to the result array
  return [...result, ...left.slice(leftIndex), ...right.slice(rightIndex)]
}
```
