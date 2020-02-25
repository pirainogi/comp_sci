## Big O

###Grow Rate of Algorithms
* Regardless of computational power, we base an algorithm's run time based on the number of units (or operations) of work
  * For a simple search with 100 elements, it would take 100ms to run
  * With a binary search with 100 elements, it would only take 7ms to run
  * When we increase the number of elements to a billion, the run time changes dramatically
    * Binary Search takes 32ms
      * log<sub>2</sub> 1,000,000,000,000 = 32
    * Simple Search takes 1,000,000,000,000ms (11 days) because it needs to do 1 unit of work for every element
  * You CANNOT assume run time will grow at the same rate
    * Binary Search was 15x faster than Simple Search at 100 elements
    * Binary Search was 33 million x faster with 1 billion elements
* Algorithms' run time increases as the size of the input increases
* Run time is expressed in Big O notation
* Algorithms that are faster become more and more faster with a larger input 

###Worst-Case Run Time
* No matter what the discrete result of the algorithm is for a certain input, Big O assumes the worst-case scenario for every algorithm

###Fastest to Slowest
* O(log n)
  * logarithmic time
  * binary search
* O(n)
  * linear time
  * simple search
* O(n * log n)
  * fast sorting algorithm
* O(n<sup>2</sup>)
  * slow sorting algorithm
* O(n!)
  * really slow algorithm
