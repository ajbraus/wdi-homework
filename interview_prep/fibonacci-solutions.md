1. Iterative
  ```js
  var fib = function(n) {

    // base case (doesn't change for n <= 2)
    var currentNum = 1;
    var prevNum = 1;
    var prevPrevNum = 0;

    // iterate through all numbers from 1-n
    for (var i = 1; i <= n; i += 1) {
      if (i > 2) {
        prevPrevNum = prevNum;
        prevNum = currentNum;
        currentNum = prevNum + prevPrevNum;
      }
    }

    return currentNum;

  };
  ```

2. Recursive

  ```js
  var fib = function(n) {

    // base case
    if (n <= 2) {
      return 1;
    }

    // recursive case
    else {
      return fib(n - 1) + fib(n - 2);
    }
  };
  ```
