Algorithm
* set of instructions to accomplish a task

## Binary Search

* Input is a sorted list of elements
* If the element is in the list, binary search returns the position where it's located, or otherwise  `null`

#### Simple Search
* Eliminate one number at a time by moving sequentially through a list
* The maximum number of guesses is the length of the list you're searching through
* Simple search runs in linear time and is denoted as O(n)

#### Binary Search
* **ONLY** works with a SORTED list
* Start with the middle number
  * if too low, guess the middle number of the upper half
  * if too high, guess the middle number of the lower half
    * each guess eliminates _HALF_ of the list
* A list of 100 elements would only take 7 maximum guesses to find the correct number
* A list of 240,000 would take 240,000 guesses with a simple search but ONLY 18 guesses with a binary search

```JS
function binarySearch(list, number){
  let low = 0, high = list.length - 1
  while(low <= high){
    let mid = low + high, guess = list[mid]
    if(guess === number){
      return mid
    } else if (guess > number){
      high = mid - 1
    } else {
      low = mid + 1
    }
  }
}
```
* Binary Search runs in logarithmic time (log time) and is denoted as O(logn)

#### Logarithms
* log<sub>10</sub> 100 = 2
  * How many 10s do we need to multiply to get 100
  * 10 x 10 = 100
* 10<sup>2</sup> = 100 <> log<sub>10</sub>100 = 2
* 10<sup>3</sup> = 1000 <> log<sub>10</sub>1000 = 3
* 2<sup>3</sup> = 8 <> log<sub>2</sub>8 = 3
* 2<sup>4</sup> = 16 <> log<sub>2</sub>16 = 4
