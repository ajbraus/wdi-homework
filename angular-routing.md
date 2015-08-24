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

## Vanilla ui-router (we won't be using this router)

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

Please **Follow Along** with these steps to add `ngRoute` to your project that you started yesterday.

## Add `ngRoute` to A Project

1. Include `angular-route.js` in your index.html file after `angular.js`
  ```html
    <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.4.4/angular-route.min.js"></script>
  ```
1. Now you need to load the `ngRoute` module into your application.
  ```js
    angular.module('starter', ['ngRoute'])
  ```
1. Now we're ready to set up our routes!

** a quick note on naming conventions -- modules like `ng-route` will sometimes be written as `ngRoute`. They are referring to the same module, just in different contexts. **


## Setting up our Templates
As you can probably imagine, as our app grows, our single `html` file is going to get very big and messy. To combat this, we're going to turn our `index.html` into a "layout template." Like in Rails, this template will be the common template for all the views in our application. Other "partial templates" are then included into this layout template depending on the current "route" -- the view that is currently displayed to the user.

To create application routes, we are going to use `ng-route`. `ng-route` helps us wire together controllers, view templates, and the current URL location.

1. Create a folder in the top level of your app called `templates`.
1. Create a new file called `todos.html` and put it in the `templates` folder.
1. In `index.html`, move the code between the `<body></body>` tags to your new `todos.html` file.
1. In `index.html` add an `ng-view` directive in the `body`.
  ```html
  <body ng-controller="MainCtrl">
        <div ng-view></div>
  </body>
  ```

## Configure our Routes

1. Using the `.config()` method, we request the $routeProvider to be injected into our config function and use the `$routeProvider.when()` method to define our routes. Open up your `app.js` file. We're going to dot-chain our route information off our app. Put this code at the top of the file right below where you define the app.
  ```js
  angular.module('starter', ['ngRoute'])
  .config(['$routeProvider',
      function($routeProvider) {
        $routeProvider.
          when('/', {
            templateUrl: 'templates/todos.html',
            controller: 'TodoCtrl'
          }).
          otherwise({
            redirectTo: '/'
          });
      }]);
  ```

## Setting up our Controllers

1. Create a new file in your top level called `controllers.js`.
1. Move your `MainCtrl` from `app.js` to this new file.
  ```js
  angular.modules('starter', [])
  .controller('MainCtrl', ['$scope', '$rootScope',
      function($scope, $rootScope) {
        ...
      }
  ])
  ```
1. Move your `TodoCtrl` from `app.js` to this new file.
  ```js
  .controller('TodoCtrl', ['$scope',
      function($scope) {
        ...
      }
  ])
  ```

1. Make sure everything gets loaded correctly. YAY!!
