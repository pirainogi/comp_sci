## Recursion
* When a function/method calls itself
* In order to prevent an infinite loop, you need to set the parameters for when the function should stop calling itself

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
