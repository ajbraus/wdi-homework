# Angular Directives Challenges

| Objectives |
| :--- |
| Use `ng-submit` to do validation |
| Filter data in an `ng-repeat` with a custom filter |
| Pluralize words with `ng-pluralize` |
| Show and hide data with `ng-hide` |

# Challenges

## Base Challenges

For these challenges use your todo app from yesterday

1. Pluralize the lable of the count of your todos. e.g. "4 Todos"
1. Add an attribute `created_at` to your todos and use the `date` filter to display this time as "posted on Monday April 24, 2015"
1. Update your todo form to use an actual `<form>` and `ng-submit`.
1. Require the `todo.title` and disable the button if `todo.title.$invalid`
1. Add an attribute "completed" to each todo.
1. Make a button that when you click it sets the "completed" to true.
1. Use the directive `ng-class` to conditionally set a class that strikes through the todo title and turns the text grey if "completed" is true. Look up the ng-class docs to complete.

## Try Challenges

1. Add a new resource to your todos called "Lists". Lists have a title and many todos. (Hint: Think mongo nested resource).
2. Wireframe how you would navigate between lists of todos and add new todos to them. Use `ng-repeat` and `filter` to filter to see only one list's todos.
