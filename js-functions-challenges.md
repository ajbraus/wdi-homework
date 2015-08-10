
## Challenges

1. Write a `multiply` function that finds the product of two numbers.

  ```js
  multiply(5, 7) => 35
  ```

2. Write a function that takes in a number and returns `true` if the number is even and `false` if the number is odd (**Hint:** Look up the `%` operator).

  ```js
  isEven(4) => true
  ```

3. Write a function that swaps two values at two different indexes in an array.

  ```js
  swap(["moe", "larry", "curly"], 0, 2) => ["curly", "larry", "moe"]
  ```

4. Write a function that generates a random number in a specified range (**Hint:** Look up Math.random()).

  ```js
  getRand(5, 10) => 8 (any number between 5 and 10)
  ```

5. Write a function that generates an array of specified length that contains random numbers from 1 to 100.

  ```js
  randArr(3) => [23, 11, 82]
  ```

## Stretch Challenges

1. Write a `getMax` function that finds the maximum number in an array.

1. Write a function called `explainMather` that takes in three arguments: two numbers and a function called `mather`. The `explainMather` function should pass the two numbers into `mather` and write out a message in the console to show the two number inputs and the output from `mather`. Test `explainMather` by passing in your `multiply` function from challenge #1.

1. Write a `vowels` function that counts the number of vowels in a given string.

1. merge(arr1, arr2)

  Write a function that takes two sorted arrays of numbers and returns a merged array of the sorted numbers. For example, if the input arrays were `var arr1 = [3,6,11]` and `var arr2 = [2,4,5,8,9]`, the returned array would be: `[2,3,4,5,6,8,9,11]`.

1. letterCount(word)

  Write a function that counts the number of times each letter occurs in a given string. It should return an object containing the count for each letter. For example, the string "apple" would return the following:

  ```js
  {
    a: 1,
    p: 2,
    l: 1,
    e: 1
  }
  ```

  **Bonus**: Make sure that lower case letters and upper case letters count for the same character. Also, ignore spaces and punctuation.

1. sillySum(arr)

  Write a function that takes an array of numbers and returns the sum of each number multiplied by its index.

  ```js
  count += (number * index)
  ```

1. numSquare(max)

  Create a function called `numSquare` that will return an array of all perfect square numbers up to, but not exceeding a max number.
