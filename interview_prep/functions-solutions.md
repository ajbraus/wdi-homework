1. Reverse

  ```js

  var reverse = function(str) {
    var newStr = "";
    for (var i = str.length - 1; i >= 0; i -= 1) {
      newStr += str[i];
    }
    return newStr;
  };

  reverse("Hello");

  ```

2. swap

  ```js

  var x = "a";
  var y = "b";

  // check values of x and y
  console.log("x: " + x + ", y: " + y);

  // swap x and y
  var temp = x;
  x = y;
  y = temp;

  // check values of x and y again
  console.log("x: " + x + ", y: " + y);
  
  ```
