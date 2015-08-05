#Partials!

 There are many occasions where a developer may be using the same snippet of html over and over again in their views.  While not always avoidable, it is important to keep your code D.R.Y (Don't Repeat Yourself) while building an application.  Rails provides developers with a nifty concept called 'Partials' to make sub-templates to dry up the views.

 Simply put, partials allow users to create sub-templates or sub-views in a separate file that you can load into different parts of the application.

 A common example of using a 'partials' is making a partial for the form section of the new and edit templates.  

 **new.html.erb**
 ```
 <h1>New Post</h1>

 <%= form_for :article do |f| %>
  <p>
    <%= f.label :title %><br>
    <%= f.text_field :title %>
  </p>

  <p>
    <%= f.label :text %><br>
    <%= f.text_area :text %>
  </p>

  <p>
    <%= f.submit %>
  </p>
<% end %>
```

 Let's also assume that you've given the user the ability to edit their blog posts:

  **edit.html.erb**
 ```
 <h1>Edit Post</h1>

 <%= form_for :article do |f| %>
  <p>
    <%= f.label :title %><br>
    <%= f.text_field :title %>
  </p>

  <p>
    <%= f.label :text %><br>
    <%= f.text_area :text %>
  </p>

  <p>
    <%= f.submit %>
  </p>
<% end %>
```

An instance like is is a prime opportunity to use a PARTIAL!!

 Our **new** and **edit** views are stored in **app/views/posts**.  We can place our partial file in the **posts** folder so our views can easily reference it.

  Partials are always named with an underscore ( _ ) at the beginning of the name.  So, in this case, our partial would be named **_form.html.erb**.  And it could be found at **app/views/posts/_form.html.erb**

Once we have the partial stored in the folder you can reference it like so:
**app/views/posts/new.html.erb**
```
<h1>New Post</h1>

<%= render 'form' %>
```

and...

**app/views/posts/edit.html.erb**
```
<h1>Edit Post</h1>

<%= render 'form' %>
```

This is but one example of how you can use partials to keep your code D.R.Y, speed up your development, and reduce mistakes while building applications.

Partials can also be used in places like headers, footers, the head of your views, and the concept even exists in your controllers (in the form of private methods) to help keep them skinny.


##Readings and Resources:

Here are some in depth articles that can help show the different ways partials help in development:

[Rich on Rails](https://richonrails.com/articles/partials-in-ruby-on-rails)

[Getting Started with Rails](http://guides.rubyonrails.org/getting_started.html#using-partials-to-clean-up-duplication-in-views)
The end of section 5.

[Layouts in Rails](http://guides.rubyonrails.org/layouts_and_rendering.html#using-partials)

[Quick Video Intro into Partials](https://www.youtube.com/watch?v=F1QHYQwzVK4)
