# Routing in Angular

In a client-side framework like AngularJS routing is managed not by the server, but by the front end itself. Angular detects the path of your URL and conventionally maps that URL to a controller and template.

## Background

Angular first shipped with a simple routing module that let you connect one URL with one controller and one template. Very quickly developers in the Angular community wanted to go beyond this simple coupling and leverage Angular's ability to nest controllers, views, and scopes together to make more complex and modular front-end applications. The Angular community decided to extract the standard angular routing module into its own separate module calle `ngRoute`. This commenced a virtual food fight for who could build the best routing module for Angular. The unproclaimed winner was a module called `ui-router` which is part of a larger library called  [Angular-UI](https://angular-ui.github.io/) that provides a whole family of useful custom Angular directives.

For the purposes of learning Angular, we will be using the standard `ngRoute` routing module. But as you google routing problems you will find many examples of apps using `ui-router` so we will look at `ui-router`'s basic setup.

The core difference between `ng-route` and `ui-router` is that `ng-route` is based on URL and `ui-router` is based on the `state` of an application and treats the URL as merely an attribute of a state.

## Vanilla ng-route

> Reference: [ngRoute](https://docs.angularjs.org/api/ngRoute)

```js
sampleApp.config(['$routeProvider',
  function($routeProvider) {
    $routeProvider.
      when('/phones', {
        templateUrl: 'partials/phone-list.html',
        controller: 'PhoneListCtrl'
      }).
      when('/phones/:phoneId', {
        templateUrl: 'partials/phone-detail.html',
        controller: 'PhoneDetailCtrl'
      }).
      otherwise({
        redirectTo: '/phones'
      });
  }]);
```

## Vanilla ui-router

> Reference: [ui-router](https://github.com/angular-ui/ui-router)

```js
$stateProvider
  .state('home', {
    url: '/',
    templateUrl: 'welcome/home.html',
    controller: 'HomeCtrl'
  });
```

## Accessing URL Params

Using `ngRoute` we will want to access URL parameters in a controller, like when you want to use an `:id` to GET a single resource or when you want to. We'll inject `$routeParams`

```js
app.controller("GuitarDetailsController", ['$scope','$http','$routeParams',
 function($scope, $http, $routeParams)
  {
    $http.get('js/data.json').success (function(data){
      $scope.guitarVariable = data;
      $scope.whichGuitar = $routeParams.guitarID;
    });
  }]
);
```

# Tutorial

Please **Follow Along** with these steps to add `ngRoute` to your project.

## Add `ngRoute` to A Project

1. Include `angular-route.js` in your index.html file after `angular.js`
  ```html
    <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.4.4/angular-route.min.js"></script>
  ```
1. Now you need to load the `ngRoute` module into your application.
  ```js
    angular.module('starterApp', ['ngRoute']);
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

  todoControllers.controller('TodoCtrl', ['$scope',
      function($scope) {
        console.log("The TodoCtrl lives to serve.")
      }
  ])
  ```
1. Move the page specific code from `app.js` to the space where the `...` is in `controllers.js`.
