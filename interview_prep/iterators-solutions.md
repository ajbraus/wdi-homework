1. Write a function called `each` that takes in an array and a callback function. `each` should iterate through all items in the array and call the callback function with each item and its index as parameters. `each` should return the original array that was passed in.
  ```
  // `each` takes in an array and a callback function
  var each = function(list, callback) {
    // iterates through each item in array
    for (var i = 0; i < list.length; i += 1) {
      // calls callback function with item and index
      callback(list[i], i);
    }
    // returns original array
    return list;
  };
  ```
2. Write a function called `map` that takes in an array and a callback function. `map` should iterate through all items in the array, call the callback function with each item and its index as parameters, and return a new array of the results.

  ```
    // `map` takes in an array and a callback function
    var map = function(list, callback) {
      var mappedList = [];
      // iterates through each item in array
      for (var i = 0; i < list.length; i += 1) {
        // calls callback function with item and index (adds result to `mappedList`)
        mappedList.push(callback(list[i], i));
      }
      // returns mapped array of results
      return mappedList;
    };
  ```

3. Write a function called reduce that takes in an array of numbers. `reduce` should return the sum of all the numbers in the array.

```
  // `reduce` takes in an array of numbers
  var reduce = function(numList) {
    var sum = 0;
    for (var i = 0; i < numList.length; i += 1) {
      sum += numList[i];
    }
    return sum;
  };
```
