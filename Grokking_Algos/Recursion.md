## Recursion
* When a function/method calls itself
* In order to prevent an infinite loop, you need to set the parameters for when the function should stop calling itself
* saves the state of the partially complete function calls 

#### Base Case
* When the function doesn't call itself again

#### Recursive Case
* When a function calls itself

```JS
function countdown(i){
  console.log(i)
  if(i< 0){
    return
  } else {
    countdown(i-1)
  }
}
```

## Divide and Conquer
1. Figure out the base case (simplest possible case)
2. Divide/decrease your problem until it becomes the base case

#### First Example
* 1680 x 640 farm
  * want to divide evenly into _square_ plots
  * plots as big as possible

* base case: one side is a mutiple of another side
  * 50m x 25m can be evenly divided into 2 plots
* recursive case: apply the algorithm to every plot that cannot be evenly split up
  * total land can be divided into 2 square plots of 640x640 but 400x640 left
* solution: largest square plot is 80 x 80 with no left overs

#### Second Example
* Sum up an array of numbers and return the total
* base case: an array with 0 or 1 number
  * return 0 or the value of the element
* recursive: decrease the size of the array each pass (sum of the first number and the sum of the rest of the list)
