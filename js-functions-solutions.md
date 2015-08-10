# JS Functions Solutions

## Basic Challenge Solutions

1. multiply
  ```js
  var multiply = function(num1, num2) {
    return num1 * num2;
  };

  multiply(5, 7);
  ```

1. isEven
  ```js
  var isEven = function(num) {
    if (num % 2 === 0) {
      return true;
    } else {
      return false;
    }
  };

  isEven(4);
  ```

1. swap

  ```js
  var swap = function(arr, index1, index2) {
    var temp = arr[index1];
    arr[index1] = arr[index2];
    arr[index2] = temp;
    return arr;
  };

  swap(["moe", "larry", "curly"], 0, 2);
  ```

1. getRand

  ```js
  var getRand = function(min, max) {
    return Math.random() * (max - min) + min;
  };

  getRand(5, 10);
  ```

1. randArr

  ```js
  // use our `getRand` function as a helper (defined here again)
  var getRand = function(min, max) {
    return Math.random() * (max - min) + min;
  };

  var randArr = function(length) {
    var newArr = [];
    for (var i = 0; i < length; i += 1) {
      newArr.push(getRand(1, 100));
    }
    return newArr;
  };

  randArr(3);
  ```

## Stretch Challenge Solutions

1. getMax

  ```js
  var getMax = function(arr) {
    var max = 0;
    for (var i = 0; i < arr.length; i += 1) {
      if (arr[i] > max) {
        max = arr[i];
      }
    }
    return max;
  };

  getMax([65, 234, 99, 0, 12, 450]);
  ```

1. explainMather

  ```js
  // use our `multiply` function as a helper (defined here again)
  var multiply = function(num1, num2) {
    return num1 * num2;
  };

  // `mather` is a function we will pass in as an argument
  var explainMather = function(num1, num2, mather) {
    var output = mather(num1, num2);
    console.log(num1 + " and " + num2 + " are the inputs, and " + output + " is the output.");
  };

  explainMather(5, 8, multiply);
  ```

1. vowels

  ```js
  var vowels = function(str) {
    var vowelList = ["a", "e", "i", "o", "u"];
    var vowelCount = 0;
    for (var i = 0; i < str.length; i += 1) {
      if (vowelList.indexOf(str[i]) !== -1) {
        vowelCount += 1;
      }
    }
    return vowelCount;
  };

  vowels("pineapple");
  ```

1. merge

  ```js
  var list1 = [3, 6, 11];
  var list2 = [2, 4, 5, 8, 9];
  // output should be [2, 3, 4, 5, 6, 8, 9, 11]

  var merge = function(arr1, arr2) {
    var result = [];

    while (arr1.length > 0 && arr2.length > 0) {

      // compare first element in both arrays
      // remove the smaller number from its original array (using shift)
      // and push that value into result
      if (arr1[0] <= arr2[0]) {
        result.push(arr1.shift());
      } else {
        result.push(arr2.shift());
      }

    }
    // we need concat here b/c there will be a number left over
    // in one of the two arrays
    return result.concat(arr1).concat(arr2);
  };

  console.log(merge(list1, list2));
  ```

1. letterCount(word)

  ```js
  var letterCount = function(word) {
    // trim removes spaces
    var letters = word.toLowerCase().trim();
    var result = {};

    for (i = 0; i < letters.length; i += 1) {
      if (result[letters[i]]) {
        result[letters[i]] += 1;
      }
      else {
        result[letters[i]] = 1;
      }
    }
    return result;
  };

  var myWord = "BANANAS";
  console.log(letterCount(myWord));
  ```

1. sillySum(arr)

  ```js
  var sillySum = function(arr) {
    var total = 0;
    for (var i = 0; i < arr.length; i += 1) {
      total += arr[i] * i;
    }
    return total;
  };

  var myArray = [1, 2, 3, 4];
  console.log(sillySum(myArray));

  var anotherArray = [20, 36, 79, 13, 57];
  console.log(sillySum(anotherArray));
  ```

1. numSquare(max)

  ```js
  var numSquare = function(max) {
    var squaresArr = [];

    for (var i = 0; i <= max; i += 1) {
      if (Math.sqrt(i) % 1 === 0) {
        squaresArr.push(i);
      }
    }
    return squaresArr;
  };

  console.log(numSquare(100));


  // alternate solution

  var numSquare = function(max) {
    var squaresArr = [];

    for (i = 1; i * i <= max; i += 1) {
      squaresArr.push(i * i);
    }
    return squaresArr;
  };
  ```
