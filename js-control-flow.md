##Objectives  
| Objectives |
| :--- |
| Describe and use boolean logic |
| Trace the flow of a program based on its code |
| Predict the output from `if/else` and `switch` statements |
| Explain the differences between `for` loops and `while` loops, and when to use each |
| Implement `if/else` logic, `for` and `while` loops, and combinations |

### Motivation (Why?)

Conditionals and loops are fundamental to all programming in every language and paradigm.

### Analogy (What?)

Condtionals are like a **choose your own adventure book**.

Loops are like a **room of people introducing themselves**.

### Examples (How?)

#### Basic Boolean Operators

| English | "and" | "or" | "not" or "bang" | "double bang" |
| ------------- |:-------------|:-------------|:-------------| :------- |
| Javascript | `&&` | &#124;&#124; | `!` | `!!` | |  
| e.g. | `a && b` | a  &#124;&#124; b | `!b` | `!!b` |
| English | A and B | A or B | not B | not NOT B |

#### Boolean Comparison Operators

| strict equality | loose equality | not strictly equal | not loosely equal | greater than | less than | greater than or equal to | less than or equal to |
| ------------- |:-------------|:-------------|:-------------|:-------------|:-------------|:-------------|:-------------|
| `===` | `==` | `!==` | `!=` | `>` | `<` | `>=` | `<=` |

#### `if/else`

```
if (badWeather) {
  takeTheBus();
}

if (!badWeather) {
  walkToWork();
}
```

```
if (badWeather) {
  takeTheBus();
} else {
  walkToWork();
}
```

#### `else if`

```
if ( hasCar ) {
	// drive it!
} else if ( hasBike ) {
	// ride it!
} else if ( hasTransitPass ) {
	// take the bus!
} else {
	// better start walking!
}
```

#### `switch`

```
switch (row){
	case 1:
		price = 0.25;
	case 2:
		price = 0.50;
	case 3:
		price = 0.75;
	case 4:
		price = 1.00;
	default:  // the rest of the products (rows 5-7)
		price = 1.25
}
// ^ vending machine with prices organized by row!
```

#### `while/for` loops

```
var m = ["Bill", "Nicki", "Kelly"]
for (i = 0; i < m.length; i++) {
  console.log(m[i] + " is a nice person")
}

```

```
var movieData = {director: "Burton", year: 1993, title: "The Nightmare Before Christmas", price: 4.55}
for (key in movieData){
	if (movieData.hasOwnProperty(key)){
		console.log(key + ": ", movieData[key]);
	}
}
```

```
while (timeBeforeWork > 180000) { // Remember JS counts time in milliseconds
  hitSnooze()
}
```

##Challenges

### Docs & Resources

[Loops - JSforcats](http://jsforcats.com/#loops)
</br>
[Conditionals - Codeacademy](http://www.codecademy.com/glossary/javascript/if-statement)
</br>
[Loops - CodeAcademy](http://www.codecademy.com/glossary/javascript/loops)
</br>

### External Reading and Tutorials

[Javascripting](https://github.com/sethvincent/javascripting)
</br>
