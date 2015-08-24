# Angular Routing Challenges

> The Angular Routing tutorial lives [here](http://ajbraus.gitbooks.io/wdi-homework/content/angular-routing.html)

| Objectives |
| :--- |
| Add multiple views to the todo app you created this morning using `ng-route` |
| Create route-specific view templates |
| Create separate controllers for separate routes |


## Base Challenges

1. Add a navbar to your layout template (`index.html`) that will navigate between your home page and your new programming page. Use `ng-href` to make links to your other pages.
1. Add another route to the URL `/about-us` with a template `about-us.html` and just put your name in it.
1. Add a route to `/lists/:list_name` and link it to a `ListShowCtrl`. Put a console log in the controller and navigate to '/cleaning'.
1. Now `console.log` the `$routeParams.list_name` and see it console log "cleaning".
1. Return all the todos with a list of "cleaning" from your array of todos.
1. Add a "new list" button that goes to a `/lists/new` route with a form that creates a new list. After it creates the list, use `$location.path('/lists/' + $scope.list.name)` redirect to the newly created list.
1. Add a botton that marks a todo as completed.
1. Add a way to show only completed (checked) todos and only active (unchecked) todos.
1. Inside the list add a button that markes all todos as done.
1. Add a button to delete all completed todos.

## Stretch Challenges

1. Use the bootstrap modal to create sign up and login modals (make sure these are narrow modals! not wide ones). Have the login and signup buttons and modals live in the MainCtrl. Put the `login` and `signup` functions in the `$scope` of the `MainCtrl`. That will give you the access to these modals and functions in all views. Have the signup and login functions just console log a `$scope.user` with email and password object you would send to the server.
1. Make a "ListIndex" route, controller, and template to `/lists`. In list index you can navigate to All todos, each list, and always back.
