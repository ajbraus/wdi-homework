# Intro To Ruby

<img src="https://www.appsurfer.com/assets/main_landing/rubyLogo2-56b1015daf5f9c22d0225c6abe822307.gif" alt="Drawing" style="width: 100px;"/>

| Objectives |
|:--- |
| ... identify control flow patterns and functions in JS and utilize them in Ruby |
| ... apply control flow to create command line applications |
| ... apply methods in ruby to solve problems |

## What is Ruby?
> [Techotopia](http://www.techotopia.com/index.php/What_is_Ruby%3F)

Ruby is an object-oriented interpreted scripting language. When we say it is interpreted we mean to say that the Ruby source code is compiled by an interpreter at the point of execution (similar in this regard to JavaScript and PHP). This contrasts with compiled languages such as Java, Objective C, C, or C++ where the code is pre-compiled into a binary format targeted to run on a specific brand of microprocessor.

## History of Ruby
> [Techotopia](http://www.techotopia.com/index.php/What_is_Ruby%3F)

Ruby was created by Yukihiro Matsumoto (more affectionately known as Matz) in Japan starting in 1993. Matz essentially kept Ruby to himself until 1995 when he released it to the public. Ruby quickly gained a following in Matz's home country of Japan in the following years, and finally gained recognition in the rest of the programming world beginning in the year 2000. From that point on Ruby has grown in popularity, particularly because of the popularity of the Ruby on Rails web application development framework.

## How to Try Ruby Out

**Every Mac comes with Ruby inside!**

```bash
$ irb

irb(main):001:0> 2 + 2
=> 4
irb(main):002:0>
```


## Comparing to JavaScript

#### Basic Differences

| JavaScript | Ruby |
|:--- |:--- |
| ```null```, ```undefined``` | ```nil``` |
| var word = "string"  | @word = "string"  |
| a function takes arguments | a method takes parameters |
| ```console.log("hello")```  | ```puts "hello"``` |
| ```else if``` | ```elsif``` |
| Console in Browser | Console in Terminal (```$ irb```) |

#### Define a Method/Function with a Parameter/Argument

JavaScript
```js
var say = function(something) {
  console.log(something);
};

say("hello");
```

Ruby
```ruby
def say(something)
  puts something
end

say('hello')
say 'gello'
```

#### Define For Loop

JavaScript
```js
var names = ["Sonja", "Alex", "Jared"]

for (i = 0; i < names.length; i++) {
  console.log(names[i]);
}
```

Ruby
```ruby
@names = ["Sonja", "Alex", "Jared"]

names.each do |n|
  p n
end
```

#### Define a Map Function

JavaScript
```js
var names = ["Sonja", "Alex", "Jared"]

var nameLengths = _.map(names, function(el) {
  el.length
})
```

Ruby
```ruby
names = ["Sonja", "Alex", "Jared"]

name_lengths = names.map do |n|
  n.count
end

# OR

name_lengths = names.map { |n| n.count }

```

#### Ruby has awesome stuff that JS doesn't

For example: ```any?``` and ```present?``` and ```blank?``` that return true or false.

```ruby

def greet(friends)
  friends.each do |f|
    p "Hello #{f}"
  end
end

my_friends = ["Andrew", "Bill", "Sally"]

if my_friends.any? # checks if there are any values in an array
  have_a_party(my_friends)
end

```

#### Ruby also has awesome iterators built right in (a la UnderscoreJS)

For example: ```each``` and ```map``` and ```inject``` and those even have some fancy syntax you can use.

```ruby

people = [{ name: "Mary", age: 34 },
          { name: "Sonja", age: 54 },
          { name: "John", age: 64 }]

people.each do |person|
  puts "person[:name] is #{person[:age]} years old."
end
#=> "Mary is 34 years old"
#=> "Sonja is 54 years old"
#=> "John is 64 years old"

people.map(&:age) #=> [34, 54, 64]
people.inject(0) { |sum, n| sum + n[:age] } #=> 152

```



## Challenges

[Ruby Tutorial: Try Ruby](http://tryruby.org/)
