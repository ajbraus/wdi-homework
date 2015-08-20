# Angular Routing Challenges

| Objectives |
| :--- |
| Add multiple views to the todo app you created this morning using `ng-route` |
| Create route-specific view templates |
| Create separate controllers for separate routes |

## Setting up Routing

1. Include `angular-route.js` in your index.html file after `angular.js`
```html
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.3.14/angular-route.min.js"></script>
```
1. Now you need to load the `ngRoute` module into your application.
```js
angular.module('app', ['ngRoute']);
```
1. Now we're ready to set up our routes!

*** a quick note on naming conventions -- modules like `ng-route` will sometimes be written as `ngRoute`. They are referring to the same module, just in different contexts. ***

## Setting up our Templates
As you can probably imagine, as our app grows, our single `html` file is going to get very big and messy. To combat this, we're going to turn our `index.html` into a "layout template." Like in Rails, this template will be the common template for all the views in our application. Other "partial templates" are then included into this layout template depending on the current "route" -- the view that is currently displayed to the user.

To create application routes, we are going to use `ng-route`. `ng-route` helps us wire together controllers, view templates, and the current URL location.

1. Create a folder in the top level of your app called `templates`.

1. Create a new file called `programming.html` and put it in the `templates` folder.

1. In `index.html`, move the code between the `<body></body>` tags to your new `programming.html` file.

1. In `index.html` add an `ng-view` directive in the `body`.
```html
<body ng-controller="MainCtrl">
      <div ng-view></div>
</body>
```

## Configure our Routes
1. Using the `.config()` method, we request the $routeProvider to be injected into our config function and use the `$routeProvider.when()` method to define our routes. Open up your `app.js` file. We're going to dot-chain our route information off our app.
```js
.config(['$routeProvider',
    function($routeProvider) {
      $routeProvider.
        when('/programming', {
          templateUrl: 'templates/programming.html',
          controller: 'ProgrammingCtrl'
        }).
        otherwise({
          redirectTo: '/'
        });
    }]);
```

## Setting up our Controllers

1. Create a new file in your top level called `controllers.js`.

1. Include this

  ```js
  var todoControllers = angular.modules('starter', []);

  todoControllers.controller('TodoCtrl', [$scope,
      function($scope) {
        ...
      }
  ])
  ```

1. Move the page specific code from `app.js` to the space where the `...` is in `controllers.js`.

## Base Challenges
1. Add a navbar to your layout template (`index.html`) that will navigate between your home page and your new programming page (use `ng-href`).
1. Add another route called `cleaning`.
1. Add some items to your `cleaning` page with an input field.
1. Add checkboxes next to each of the todos (use `ng-model`).
1. Add a button that marks all the todos as complete.
1. Add a way to show only completed (checked) todos and only active (unchecked) todos.
1. Add functionality that deletes all completed todos.

## Evening Challenges
