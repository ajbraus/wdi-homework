# MEAN Authentication with JWT (JSON Web Tokens)

| Objectives |
| :--- |
| Compare and contrast a cookie-session and webtoken authentication |
| Boostrap JWT authentication in a MEAN application |

## Background

With Express and Ruby we learned the Cookie-Session method of authentication. There is a way to use the same method in a **Single Page Application** with AngularJS, however there are some problems:

To avoid these problems the client and the server can exchange an encrypted chunk of JSON called a **JSON Web Token** or JWT (pronounced ''*jot*'')

![cookie-token-auth](/images/cookie-token-auth.png)
> Reference [auth0.com](https://auth0.com/blog/2014/01/07/angularjs-authentication-with-cookies-vs-token/)

## Why Use JWT?

Aren't you tired of worrying about keeping track of all these things:

1. Sessions
1. Cookies
1. CSRF
1. CORS

## JWT Flow
> Reference: [blog.matoski.com](http://blog.matoski.com/articles/jwt-express-node-mongoose/)

1. Client Login
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

### For example:

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

#### Encryption

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

https://scotch.io/tutorials/the-anatomy-of-a-json-web-token
http://jwt.io/
https://developer.atlassian.com/static/connect/docs/latest/concepts/understanding-jwt.html
http://blog.matoski.com/articles/jwt-express-node-mongoose/


# Challenges

Follow this tutorial

## Tutorial

1. Clone the seed-mean-html repo and run it
  ```bash
  $ git clone https://github.com/ajbraus/seed-mean-html.git mean-auth
  $ cd mean-auth
  $ nodemon
  ```
1. Add npm modules `express-jwt` and `jsonwebtoken` to your server.
  ```
  $ npm install express-jwt jsonwebtoken -s
  ```
1. Protect the `/api` route with JWT
  ```js
  // server.js
  // JWT
  jwt = require('express-jwt');

  // ...

  app.use('/api', jwt({ secret: 'secret'})

  ```
  Now you should expect your api routes to return `401 (Unauthorized)` error. Have your app go to `/login` when unauthorized.

1. Add '/login' template, route and controller

  ```html
  <div class="col-sm-4 col-sm-offset-4">
    <legend>Login</legend>
    <form ng-submit="login">
      <div class="form-group">
        <label for="exampleInputEmail1" ng-model="user.email">Email address</label>
        <input type="email" class="form-control" id="exampleInputEmail1" placeholder="Email">
      </div>
      <div class="form-group">
        <label for="exampleInputPassword1" ng-model="user.password">Password</label>
        <input type="password" class="form-control" id="exampleInputPassword1" placeholder="Password">
      </div>
      <div class="form-group">
        <label for="exampleInputPassword1" ng-model="password_confirm">Confirm Password </label>
        <input type="password" class="form-control" id="exampleInputPassword1" placeholder="Confirm Password">
      </div>
      <button type="submit" class="btn btn-default">Submit</button>
    </form>
  </div>
  ```

1. Add a `User` factory and inject it into your `LoginCtrl`

  ```js
  // services.js

  .factory('User', ['$resource', 'HOST', function ($resource, HOST) {
    return $resource(HOST + '/users/:id', { id: '@id' }, {
      update: { method: 'PUT' },
      sign_up: { url: HOST + '/users', method: 'POST', isArray: false },
      login: { url: HOST + '/users/login', method: 'POST', isArray: false },
      logout: { url: HOST + '/users/logout', method: 'GET', isArray: false }
    })
  }]);
  ```
  


1.  

1. Add '/sign-up' template, route & controller
  ```js
  // app.js

  .when('/sign-up', {
    templateUrl: 'templates/sign-up'
  , controller: 'SignUpCtrl'
  })
  ```
1. Add an auth service
  ```js

  ```
1. Add
