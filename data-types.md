# JavaScript Data Types

## Key Questions

### Primitives

* Boolean
* Null (nonexistent object)
* Undefined (empty variable)
* Number (integer and floating point)
* String (words in quotes)
* Symbol (only in ES6)

### Objects

Objects are a *reference data type* that allow us to group primitives together as an array or hash. There isn't enough room in a variable to store an entire object; instead, we store a reference to another location in memory.

Use the object literal to create objects:
```
var car = { make: "Tesla", model: "S", year: 2015 };
```
```
var cars = [car, { make: "Toyota", model: "Prius", year: 2010 }];
```

## Further Reading

1. [JavaScript data types and data structures [MDN]](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures)
2. [Different ways to define an object [SO]](http://stackoverflow.com/questions/1143498/difference-between-an-object-and-a-hash)
3. [Working with strings](http://learnjsdata.com/strings.html)

## Challenges
