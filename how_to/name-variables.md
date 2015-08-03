# How to Name Variables

As software developers we mostly have to follow the rules of logic and the syntax of the languages and frameworks we are using. However, there are a few pieces we do get to decide. We can decide on the names of variables, methods, functions, classes, and id's. Here are some considerations and conventions for how to name them all well.

## Domain Specific Language (DSL)



## Reserved Words

Although we have a lot of control over "taco" variables, there are a few words that are 'protected' because they are a fixe part of one or many languages.

| Javascript | Ruby |
|:--- |:--- |
| `return` | `return` |
| `true` | `true` |
| `false` | `false` |
| `begin` | `begin` |
| | `def` |
| | `end` |
| | `do`  |
| `default` |  |
| `this` |  |
| `try` |  | |

## The Dom

| | CSS Classes | ID's
|:--- |:--- |:--- |
| Convention | hyphenated | hyphenated |
| 1 Word | 'tag' | 'name' |
| 2 Words | 'tag-list' | 'name-input' |
| Selector | .tag-list | #name-input |

## JavaScript

| Variable | Constructor | function |
|:--- |:--- | :--- |
| camelCase | UpperCamelCase | camelCase() (parens) |
| `firstName` | `Person` | `showForm()` |

## Ruby/Ruby on Rails

| Variable | Model Class | Model Instance | Controller | Table |
|:--- |:--- |:--- |:--- |:--- |
| snake_case | UpperCamelCase | '@'+ snake_case' |  UpperCamelCases (plural) | snake_cases (plural) |
| `current_time` | `User` | `@user` | `UsersController` | `users` |
