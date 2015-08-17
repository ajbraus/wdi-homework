# Intro to Angular Challenges

| Objectives |
| :--- |
| Start an Angular 1.4 app with `ng-app` |
| Setup a two way data binding with `ng-model` |
| Display a list with `ng-repeat` |
| Manipulate the DOM with `$scope` |

## Background

Angular is an opinionated yet flexible front end framework made for building robust single page applications. It is written in JavaScript and created and maintained by Google.

## Data Bindings

Through data binding, Angular makes the UI of single page applications multiple times less complex. In order to understand data bindings its best to just set one up. Please follow along and make the most basic angular app you can:

1. Create the two root files of any AngularJS app in a new folder: `index.html` and `app.js`
2. For now, ignore `app.js`. In `index.html` add the below code that 1. adds angular to an html file, 2. puts an input field but add the "directive" `ng-model` which connects the input field's value to the AngularJS data model called `$scope`, and 3. binds this model to with the `{{}}` notation.
  ```html
  <!doctype html>
  <html ng-app>
  <head>
    <title>My Angular App</title>
    <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.3.14/angular.min.js"></script>
  </head>
  <body>

    <input type="text" ng-model="term" />
    <p>{{term}}</p>

  </body>
  </html>
  ```
2. `npm install http-server` and call `http-server` - now open `http://localhost:8080` in your browser
3. Type in the input. What do you see?

This is a two way data binding. As you type, you update `$scope` Angular's data model. Every time the model is updated, Angular updates the views to match the new state of the model. This is called Angular's **Digest Cycle**. In jQuery this would be like having a `change()` listener on every element and a function that updates the DOM, something like this but for every element:

```js
  $('input').change(function() {
    $('#term').text($(this).val());
  });
```

## View Controllers

Angular is very modular and lets you add controllers to your views. Tomorrow we'll learn Angular Routing where we will learn how to map controllers to views and urls.

1. In `app.js` initialize an angular app called `starter`

  ```js
  angular.module('starter', [])
  ```
2. Now connect this script to your `index.html` and set `starter` to be the value of your `ng-app` directive. Check that everything works the same.

  ```html
  <html ng-app="starter">
  <head>
    <title>My Angular App</title>
    <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.3.14/angular.min.js"></script>
    <script src="app.js"></script>
  </head>
  ...
  ```

3. Now add a controller to your `app.js` and connect it to your `<body>` tag with the directive `ng-controller`.  

  ```js
  angular.module('starter', [])
    .controller("MainCtrl", ['$scope', '$rootScope', function ($scope, $rootScope) {
      $scope.term = "cellar door"
    }])
  ```

  ```html
  <body ng-controller="MainCtrl">
  ```

## Adding a function to $scope

`$scope` reflects the state of data, but it also holds functions that can fire to query an API, change the DOM, or filter or change the model. Let's add a simple function.

1.  Add a button to your page and add the `ng-click` directive attribute to attach a click event activated function. Let's pass in the function as the value of the attribute: `showAlert()`.

  ```html
  <button ng-click="showAlert()">Alert</button>
  ```

2. Now in our `MainCtrl`, let's add this function to `$scope` and have it create an alert with the value of `$scope.term`

  ```js
  angular.module('starter', [])
  .controller("MainCtrl", ['$scope', '$rootScope', function ($scope, $rootScope) {
    $scope.term = "cellar door"
    $scope.showAlert = function() {
      alert($scope.term);
    }
  }])
  ```
3. Try it out.

## Base Challenges

1. Add bootstrap using the CDN. Using the bootstrap grid put your list of todos in the center third of the page.
1. Inside the <body> create a <div> element and attach an Angular controller called (you guessed it!) `TodoCtrl`.
2. Create this TodoCtrl in your `app.js` by dot-chaining it to the end of the `MainCtrl`.
3. Write a console log in the controller to make sure its working.
4. Assign an array of simple todo objects with the attribute "title" to `$scope.todos`.
5. Use `<li ng-repeat="todo in todos">{{todo.title}}</li>` to display the list of todos.
6. Above the list create an input field and use `ng-model` to bind the field to a variable in `$scope` called `todo.title`.
7. Make a button that has a click function that takes the `$scope.todo` and pushes it on to the `$scope.todos` array. After pushing the new todo, set `$scope.todo.title` to "".
9. Display a counter of how many todos you have.
10. Add an attribute "completed_at" to each todo.
11. Make a button that when you click it sets the "completed_at" time to now (use `new Date()`).
12. Use the directive `ng-class` to conditionally set a class that strikes through the todo title and turns the text grey if "completed_at" is present. Look up the ng-class docs to complete.
13. Make another button on each todo that deletes that todo from the array of todos. Add underscore and use the `_.findWhere()` function to find the todo where the title is equal to the title clicked. (Remember that to access the clicked element use the reserved word `this`)

## Stretch Challenges

1. Write a blog in AngularJS. It should have posts and the posts should have comments. (hint use `post.comments.push($scope.comment)` to push a comment into a comments attribute).
