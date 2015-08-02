# Regular Expressions

>[Ruby Regexp](http://ruby-doc.org/core-2.2.0/Regexp.html)

Regular expressions (**regex** or **regexps**) are patterns which describe the contents of a string. They’re used for testing whether a string contains a given pattern or extracting the portions that match. Common examples of regexps are "find-and-replace" operations and string format validation (i.e. phone numbers or email addresses).

Many programming languages have regexp capabilities built-in, and Ruby is one of them. Today we'll use regexps to match string patterns in Ruby.

## Defining and Matching

Regexps are bounded by forward-slashes (`/`). **For example:**

```ruby
/hello/
```

To test if a string matches the pattern of a regexp, we use `.match`. **For example:**

```ruby
# returns match data if any
/san/.match("san francisco") #=> #<MatchData "san">

# returns nil if no match data
/san/.match("San Francisco") #=> nil
```

## Basic Regexp Patterns

For a more complete list of basic regex patterns, see [Rubular's Regex quick reference](http://rubular.com).

```ruby
/[abc]/ #=> a single character of: a, b, or c

/\A/ #=> start of string

/\s/ #=> any whitespace character

/\d/ #=> any digit (number)

/(a|b)/ # => a or b
```
