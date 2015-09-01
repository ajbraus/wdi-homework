# MEAN Authentication with JWT (JSON Web Tokens)

| Objectives |
| :--- |
| Compare and contrast a cookie-session and webtoken authentication |
| Boostrap JWT authentication in a MEAN application |

## Background

With Express and Ruby we learned the Cookie-Session method of authentication; however, there is a better way to do communicate authentication with **Single Page Application** and **Service-Based Architecture**. We're going to use an encrypted chunk of JSON called a **JSON Web Token** or JWT (pronounced ''*jot*'') to communicate authentication between client and server.

![cookie-token-auth](/images/cookie-token-auth.png)
> Reference [auth0.com](https://auth0.com/blog/2014/01/07/angularjs-authentication-with-cookies-vs-token/)

## Why Use JWT?

Aren't you tired of worrying about keeping track of all these things?

1. Sessions - JWT doesn't require sessions
1. Cookies - JWT you just save the token to the client
1. CSRF - Send the JWT instead of a CSRF token
1. CORS - Forget about it, if your JWT is valid, the data is on its way

Also these benefits:

1. Speed - you don't have to look up the session
1. Storage - you don't have to store the session
1. Mobile Ready - Apps don't let you set cookies!
1. Testing - you don't have to make loging in a special case in your tests

## JWT Flow
> Reference: [blog.matoski.com](http://blog.matoski.com/articles/jwt-express-node-mongoose/)

1. Client logs in
1. Client receives a token and stores it in localStorage or sessionStorage.
1. Client does requests with the token using an **AngularJS Interceptor**
1. Token gets decoded on the server
1. Use token data to decide if user has access to the resource, otherwise return a 401 message

## JWT FTW

A JWT is pretty easy to identify. It is three strings separated by .

```
  aaaaaaaaaa.bbbbbbbbbbb.cccccccccccc
```

Each part has a different significance:

![jwt](/images/jwt.png)

### Here is a JWT Example:

#### Header

```js
var header = {
  "typ": "JWT",
  "alg": "HS256"
}
```

#### Payload

```js
var payload = {
  "iss": "scotch.io",
  "exp": 1300819380,
  "name": "Chris Sevilleja",
  "admin": true
}
```

#### Signature

```js
var encodedString = base64UrlEncode(header) + "." + base64UrlEncode(payload);

HMACSHA256(encodedString, 'secret');
```

> **REMEMBER** The 'secret' acts as an encryption string known only by the two parties communicating via JWT. Protect your secrets!

#### JSON Web Token
```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzY290Y2guaW8iLCJleHAiOjEzMDA4MTkzODAsIm5hbWUiOiJDaHJpcyBTZXZpbGxlamEiLCJhZG1pbiI6dHJ1ZX0.03f329983b86f7d9a9f5fef85305880101d5e302afafa20154d094b229f75773
```

## Further Reading

- [jwt.io](http://jwt.io/)
- [Atlassian JWT docs](https://developer.atlassian.com/static/connect/docs/latest/concepts/understanding-jwt.html)
- [scotch.io tutorial](https://scotch.io/tutorials/the-anatomy-of-a-json-web-token)
- [JWT Express Node Mongoose](http://blog.matoski.com/articles/jwt-express-node-mongoose/)

# Features of mean-auth

## User Service

The User service needs some custom routes:

```js
app.factory('User', ['$resource', 'HOST', function ($resource, HOST) {
  return $resource(HOST + '/api/users/:id', { id: '@id' }, {
    update: { method: 'PUT' },
    sign_up: { url: HOST + '/api/users', method: 'POST', isArray: false },
    login: { url: HOST + '/api/users/login', method: 'POST', isArray: false },
    logout: { url: HOST + '/api/users/logout', method: 'GET', isArray: false }
  })
}])
```

## Auth Service

So far we've used services like "client-side models" that connect to our RESTful API with `$resource`, but you can also tuck away functions into services and an **Authentication Service** is a very nice group of functions.

```js
app.factory('Auth', [function() {
  return {
    isLoggedIn: function () {
      return !!localStorage.getItem('jwtToken')
    }
  }
}])
```

## Angular Interceptors

An Angular interceptors allow you to "intercept" http requests and responses and change them. We use an interceptor to attach the JWT to every outgoing http request, and handle what to do with 401 (Unauthorized) statuses in any http response.

```js
// SERVICES.JS

app.factory('authInterceptor', function ($rootScope, $q, $window) {
  return {
    request: function (config) {
      config.headers = config.headers || {};
      if ($window.localStorage.jwtToken) {
        config.headers.Authorization = 'Bearer ' + $window.localStorage.jwtToken;
      }
      return config;
    },
    response: function (response) {
      if (response.status === 401) {
        // handle the case where the user is not authenticated
      }
      return response || $q.when(response);
    }
  };
})

app.config(function ($httpProvider) {
  $httpProvider.interceptors.push('authInterceptor');
});
```

## $rootScope.$broadcast('taco') & $rootScope.$on('taco', callback)

Use AngularJS's `$broadcast` and `$on` to notify other controllers that you logged in:

```js
  $rootScope.$broadcast('loggedIn'); // TELL THE OTHER CONTROLLERS WE'RE LOGGED IN
```

```js
  $rootScope.$on('loggedIn', function () {
    $scope.isLoggedIn = true
  })
```

# Challenges

Fork this mean-auth sample project and add a `sign-up` method.

**Goal** Get the mean-auth app running locally
1. Clone the mean-auth
  ```bash
  $ git fork https://github.com/ajbraus/mean-auth
  $ cd mean-auth
  $ nodemon
  ```

**Goal** Add a sign-up feature
1. Add '/sign-up' template, route & controller
  ```js
  // app.js

  .when('/sign-up', {
    templateUrl: 'templates/sign-up'
  , controller: 'SignUpCtrl'
  })
  ```
1. Add the email to the JWT
1. Sign the JWT and send it back to the client and save it
1. After signup go to '/'
1. Notify the rest of the app that you are logged in with `$rootScope.$broadcast('loggedIn')`

**Goal**: Hash passwords

1. Install and `bcrypt`
  ```
  $ npm install --save bcrypt
  ```
1. Add bcrypt and salt to your `user.js`
  ```js
    // user.js

    bcrypt = require('bcrypt'),
    salt = bcrypt.genSaltSync(10);
  ```
1. Add the `createSecure`, `authenticate` and `checkPassword` functions to the `User` model.
  ```js
  //
  // user.js
  //

  // ...

  UserSchema.statics.createSecure = function (email, password, callback) {
    // `this` references our schema
    // store it in variable `that` because `this` changes context in nested callbacks
    var that = this;

    // hash password user enters at sign up
    bcrypt.genSalt(function (err, salt) {
      bcrypt.hash(password, salt, function (err, hash) {
        console.log(hash);

        // create the new user (save to db) with hashed password
        that.create({
          email: email,
          passwordDigest: hash
        }, callback);
      });
    });
  };

  UserSchema.statics.authenticate = function (email, password, callback) {
    this.findOne({email: email}, function (err, user) {
      console.log(user);
      if (user === null) {
        callback('Can\'t find user with email ' + email, user);
      } else if (user.checkPassword(password)) {
        callback(null, user);
      }
    });
  };

  UserSchema.methods.checkPassword = function (password) {
    return password == this.password;
  };
  ```
1. Use the `User.createSecure` method to create a user at signup.
1. Add the authenticate function to the `/api/users/login` route
  ```js
    User.authenticate(req.body.email, req.body.password, function(error, user) {
      if (error) {
        res.send(error)
      } else if (user) {
        // CREATE, SIGN, AND SEND TOKEN HERE
      }
    });
  ```

**Extra Credit**: Validate that confirm password and password match in client
**Extra Credit**: Submit a pull request back to mean-auth


## Or if you want everything easy:

[Satellizer](https://github.com/sahat/satellizer)
