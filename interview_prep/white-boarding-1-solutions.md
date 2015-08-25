# White Boarding 1 Solutions

## Problem 1 - Palindrome

```js
// Problem 1 - Palindrome

function isPalindrome(str) {
  // simple solution
  str = str.toLowerCase();

  // removing spaces and punctuation
  // str = str.toLowerCase().replace(/(\s+|\W+)/g, '');

  for (var i = 0; i < str.length; i ++) {
    if (str[i] !== str[str.length - i - 1]) {
      return false;
    }
  }
  return true;
}
```

```ruby
# Problem 1 - Palindrome

def is_palindrome(str)
  # simple solution
  str = str.downcase

  # removing spaces and punctuation
  # str = str.downcase.gsub(/(\s+|\W+)/, '');

  i = 0
  while i < str.length
    if str[i] != str[str.length - i - 1]
      return false
    end
    i += 1
  end

  return true
end
```

## Problem 2 - Greatest Difference

```js
// Problem 2 - Greatest Difference

// Solution 1 - nested for loops (O(n^2) time)
function greatestDiff(array) {
  var maxDiff = 0;
  for (var i = 0; i < array.length; i++) {
    for (var j = 0; j < array.length; j++) {
      if (array[i] - array[j] > maxDiff) {
        maxDiff = array[i] - array[j];
      }
    }
  }
  return maxDiff;
}

// Solution 2 - single for loop (O(n) time)
function greatestDiff(array) {
  var min = Infinity;
  var max = - Infinity;
  for (var i = 0; i < array.length; i++) {
    if (array[i] < min) {
      min = array[i];
    }
    else if (array[i] > max) {
      max = array[i];
    }
  }
  return max - min;
}
```

```ruby
# Problem 2 - Greatest Difference

# Solution 1 - nested for loops (O(n^2) time)
def greatest_diff(array)
  max_diff = 0

  i = 0
  while (i < array.length)
    j = 0
    while (j < array.length)
      if array[i] - array[j] > max_diff
        max_diff = array[i] - array[j]
      end
      j += 1
    end
    i += 1
  end

  max_diff
end

# Solution 2 - single for loop (O(n) time)
def greatest_diff(array)
  min = Float::INFINITY
  max = -Float::INFINITY

  array.each do |num|
    if num < min
      min = num
    elsif num > max
      max = num
    end
  end

  max - min
end
```

## Problem 3 - Calculate Change

```js
// Problem 3 - Calculate Change

function calcChange(cost, money) {
  cost *= 100;
  money *= 100;

  var changeNames = ['$20s', '$10s', '$5s', '$1s', 'quarters', 'dimes', 'nickels', 'pennies'];
  var changeTypes = [2000, 1000, 500, 100, 25, 10, 5, 1];
  var totalChange = money - cost;
  var changeCounts = {};

  // loop through changeTypes
  for(var i = 0; i < changeTypes.length; i++) {
    // calculate count of changeType needed
    var count = Math.floor(totalChange / changeTypes[i]);
    // save count in changeCounts object with changeName as key
    changeCounts[changeNames[i]] = count;
    // subtract amount of current changeType from totalChange
    totalChange -= count * changeTypes[i];
  }
  return changeCounts;
}
```

```ruby
# Problem 3 - Calculate Change

def calc_change(cost, money)
  cost *= 100
  money *= 100

  change_types = {
    '$20s' => 2000,
    '10s' => 1000,
    '$5s' => 500,
    '$1s' => 100,
    'quarters' => 25,
    'dimes' => 10,
    'nickels' => 5,
    'pennies' => 1,
  }
  total_change = money - cost
  change_counts = {}

  # iterate through change_types
  change_types.each do |name, value|
    # calculate count of change_type needed
    count = (total_change / value).floor
    # save count in change_counts hash with name as key
    change_counts[name] = count
    # subtract amount of current change_type from total_change
    total_change -= count * value
  end

  change_counts
end
```

## Problem 4 - Shuffle
```js
// Problem 4 - Shuffle

function shuffle(array) {
  var tempValue;
  var randomIndex;

  // loop through elements in array, starting with last element
  for (var i = array.length - 1; i > 0; i--) {
    // pick a random index in the elements that remain
    randomIndex = Math.floor(Math.random() * i);

    // swap element at i with element at randomIndex
    tempValue = array[i];
    array[i] = array[randomIndex];
    array[randomIndex] = tempValue;
  }

  return array;
}
```

```ruby
# Problem 4 - Shuffle

def shuffle(array)
  current_index = array.length - 1

  # while there are elements left to shuffle
  while (current_index > 0)
    # pick a random index in the elements that remain
    random_index = rand(current_index)

    # swap element at current_index with element at random_index
    temp_value = array[current_index];
    array[current_index] = array[random_index];
    array[random_index] = temp_value;

    # decrease current_index by 1
    current_index -= 1
  end

  array
end
```
