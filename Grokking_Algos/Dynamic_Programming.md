# Dynamic Programming

* solve subproblems and builds up to solving the larger problem
* start with a grid
  * values of the subproblems are what you're trying to optimize 
* final row represents our current best guess for the max
  * cell[i][j] = max of { 1. previous max (value at cell[i-1][j-1]) vs. 2. value of current item + value of remaining space (cell[i-1][j-weight])}
* only works when each subproblem is discrete and doesn't depend on other subproblems
