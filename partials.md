# Partials!

 There are many occasions where a developer may be using the same snippet of html over and over again in their views.  While not always avoidable, it is important to keep your code D.R.Y (Don't Repeat Yourself) while building an application.  Rails provides developers with a nifty concept called 'Partials' to make sub-templates to dry up the views.

 Simply put, partials allow users to create sub-templates or sub-views in a separate file that you can load into different parts of the application.

 ##Form Templates

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

## Passing Local Variables

Partials are very powerful when it comes to using local variables.  You can insert a local variable in your partial to help minify your code and keep things very neat.

**new.html.erb**
```
<h1>New zone</h1>
<%= render partial: "form", locals: {zone: @zone} %>
```

**edit.html.erb**
```
<h1>Editing zone</h1>
<%= render partial: "form", locals: {zone: @zone} %>
```

**_form.html.erb**
```
<%= form_for(zone) do |f| %>
  <p>
    <b>Zone name</b><br>
    <%= f.text_field :name %>
  </p>
  <p>
    <%= f.submit %>
  </p>
<% end %>
```

In the previous example Action View's submit helper will return "Create Zone" for the new action and "Update Zone" for the edit action.

If you have an instance of a model to render into a partial, you can use a shorthand syntax:

```
<%= render @customer %>

```
Assuming that the @customer instance variable contains an instance of the Customer model, this will use **_customer.html.erb** to render it and will pass the local variable customer into the partial which will refer to the @customer instance variable in the parent view.

## Rendering Collections

Partials are very useful in rendering collections. When you pass a collection to a partial via the :collection option, the partial will be inserted once for each member in the collection:

**index.html.erb**
```
<h1>Products</h1>
<%= render partial: "product", collection: @products %>
```
**_product.html.erb**
```
<p>Product Name: <%= product.name %></p>
```

When a partial is called with a pluralized collection, then the individual instances of the partial have access to the member of the collection being rendered via a variable named after the partial. In this case, the partial is **_product**, and within the **_product** partial, you can refer to product to get the instance that is being rendered.

There is also a shorthand for this. Assuming @products is a collection of product instances, you can simply write this in the index.html.erb to produce the same result:

```
<h1>Products</h1>
<%= render @products %>
```

Rails determines the name of the partial to use by looking at the model name in the collection. In fact, you can even create a heterogeneous collection and render it this way, and Rails will choose the proper partial for each member of the collection:

**index.html.erb**

```
<h1>Contacts</h1>
<%= render [customer1, employee1, customer2, employee2] %>
```

**customers/_customer.html.erb**

```
<p>Customer: <%= customer.name %></p>
```

**employees/_employee.html.erb**
```
<p>Employee: <%= employee.name %></p>
```

In this case, Rails will use the customer or employee partials as appropriate for each member of the collection.

In the event that the collection is empty, render will return nil, so it should be fairly simple to provide alternative content.

```
<h1>Products</h1>

<%= render(@products) || "There are no products available." %>
```


These are a few examples of how you can use partials to keep your code D.R.Y, speed up your development, and reduce mistakes while building applications.

Partials can also be used in places like headers, footers, the head of your views, and the concept even exists in your controllers (in the form of private methods) to help keep them skinny.


## Readings and Resources:

Here are some in depth articles that can help show the different ways partials help in development:

[Rich on Rails](https://richonrails.com/articles/partials-in-ruby-on-rails)

[Getting Started with Rails](http://guides.rubyonrails.org/getting_started.html#using-partials-to-clean-up-duplication-in-views)
The end of section 5.

[Layouts in Rails](http://guides.rubyonrails.org/layouts_and_rendering.html#using-partials)

[Quick Video Intro into Partials](https://www.youtube.com/watch?v=F1QHYQwzVK4)
