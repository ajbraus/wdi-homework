# Outside-In Development and Anti-Patterns

So you are a developer now, and you want to start a project. Where should you start?

There are a couple options of where to start and how to run a project.

## Outside-In Development

In a client-side architecture app, an outside in development pattern works well to build your app.

For a client-side application, generally it is good to work from the **Outside-In**, meaning to work on static views first, then adding dynamic data from an api or server, and finally connecting to a persistent database. At many steps the code will throw a predictable error. Which is good! Generally these errors will tell you exactly what your next step should be.

1. Create a static view - `index.html`

  ```html
    <h1>Posts</h1>
    <div id="posts">
      <div class="post">
        <h2>I like Candy Bars</h2>
        <p>There once was a man from nantucket</p>
      </div>
    </div>
  ```

2. Add dynamic data
  ```js
    // scripts.js

    var post = { title:"I like Candy Bars", body: "There once was a man from nantucket"}
    var $postTemplate = _.template($('#postTemplate').html());
    $('#posts').append($postTemplate(post))
  ```
3. Fetch dynamic data from the server or API

  ```js
    // scripts.js

    $.get('/posts', function(data) {
      _.each(data, function(post) {
        $('#posts').append($postTemplate(post))
      })
    })
  ```
4. Add a server route
  ```js
    // server.js

    app.get('/posts', function(req, res) {
      res.json(Post.query);
    })
  ```

5. Finally create a model.

Notice that at each step the code errors out. This is OK!


## Route-Side In Development

In a server-side architecture app, for example, a **rails app** is best to build **Route-Side-In** meaning you first make a route and controller method and then define the template before adding controller logic and dynamic data from the database.

here's an example in rails

1. Define the route and controller

  ```ruby
    # config/routes.rb

    Rails.application.routes.draw do
      root: 'posts#index'
      resource :posts, only: [:index]
    end
  ```
  ```ruby
    # controllers/posts_controller.rb

    class PostsController << ApplicationController
      def index
      end
    end
  ```
2. Define the `posts/index.html.erb` template

  ```html
    <h1>Hello World</h1>
  ```

3. Once your template is visible at '/posts', then add controller logic.
  ```ruby
    # posts_controller.rb
    # ...
    def index
      @posts = Post.all
    end
    # ...
  ```

4. Then create the model and database.
  ```bash
  $ rails g model Post title:string body:text
  $ rake db:create db:migrate
  ```

5. Then update the template to show the data.

  ```html
    <% @posts.each do |post| %>
      <h1><%= post.title %></h1>
      <p><%= post.body %></p>
    <% end %>
  ```
6. Now "rinse and repeat" one route/controller/view at a time.

By following a **Route-Side-In** approach you will be moving slowly and consistently through your dev project.

## Common Project Anti-Patterns

An **Anti-Pattern** is a development or project planning strategy or pattern that looks like it will work well or even save you some time, but that in hindsight only slowed you down or frustrated you.

There are dangerously seductive patterns that seem like good ideas but then actually are the cause of 90% of your head-ache and heart-ache with projects. Try to avoid these anti-patterns and instead try to move carefully and conservatively stepwise through your plan.

### Nerd Rage & A Random Walk

A software project can seem like an intimidatingly large number of things to do and if you're like me, your first reaction is to just clench your firsts, swing your arms, and hurl yourself at the project with maniacal tears of nerd rage coursing down your cheeks. :). Don't do this. **Always make a plan** and for each step of your plan **make another smaller plan**.

### "Inside Out"

Sometimes one can fall into the **Anti-Pattern** of trying to work from the **Inside-Out**, meaning trying to build all your models and database tables/collections and then your server, and finally the views. This is generally harder because we build software so humans can use it, so starting from the "human end of things" -- the views -- is just common sense.

### "Working ahead"

One of the most common project anti-patterns you will inevitably encounter is feeling like you can effectively "work ahead" or "prepare for when I get there" or "setup something before hand". Working ahead in software is as impossible as jumping over your own shadow.

Instead always strive to do one thing at a time in the order that it makes sense to do them. Make a link to a page, then make the template, then add data to it, then get the data from the server, then, if necessary, add a new model that models the data in the database. Rinse and repeat.

### Scope-Creep

In is important to have ambitious and even grandious dreams for your software. Indeed, what were simple sites and apps are now billion dollar companies that have changed the world, so you aught to think big! However, even the biggest, baddest piece of software moves stepwise from a very simple low level of abstraction and functionality gradually to higher levels of abstraction and more sophisticated functionality.

Over any period of time you can only do so much. As developers we all need to develop a sixth sense of how much we can accomplish in a given timeframe. For projects in WDI, you usually have 7 days. You will get frustrated if you **bite off more than you can chew**.

Ways to avoid scope creep is to divide all tasks into wants and needs. That way you can allow any new big idea but you can put it in a "want" category that you can do if there is time. If you do this very aggressively, you probably will have time on Wednesday and Thursday to do some of these "stretch" features.

### There's a Library for That...

There is a library for everything, but for every library you add to your project, generally the project's complexity doubles, so you want to use as few libraries as possible, but not fewer.

It can seem easy to "just add a module for that" instead of making and understanding your own implementation. Be wary of plugging in a lot of libraries you are not familiar with in hopes that it will save you time. Likely these libraries are what are going to cause you the most problems up front or down the road.
