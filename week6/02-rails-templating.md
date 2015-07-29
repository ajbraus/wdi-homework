# Rails Models, Resources & Templating

## Resources

[![Rails Resources](http://img.youtube.com/vi/QYHdAGRzmMA/0.jpg)](https://www.youtube.com/watch?v=QYHdAGRzmMA)

## Models
[![Rails Models](http://img.youtube.com/vi/rKtLU2LcGA8/0.jpg)](https://www.youtube.com/watch?v=rKtLU2LcGA8)]

## Templating

The rails framework is based on a server-side architecture. The client will be passive and the server is very active. The server sends primarily HTML (and not JSON) back to the client. The server (not the client) will keep track of "state". State will be reflected in the HTML with which the server responds. That HTML is built with server-side templating called "erb" - **Embedded Ruby**.

The Rails framework provides a large number of helpers for working with assets, dates, forms, numbers and model objects, to name a few. These helpers are available to all templates by default.

In addition to using the standard template helpers provided, creating custom helpers to extract complicated logic or reusable functionality is strongly encouraged.

Here are a list of some built-in erb template helpers with examples.

## Helpers

### Loops

erb
```html
<h1>Names of all the people</h1>
<% @people.each do |person| %>
  Name: <%= person.name %><br>
<% end %>
```

### Links
HTML
```html
<a href="/articles/3">Show</a>
```

erb
```html
<%= link_to "Show", article_path(@article) %>
```

### URL Links
HTML
```html
<a href="http://google.com">Google</a>
```

erb
```html
<%= link_to "Google", "http://google.com" %>
```

### Images

HTML
```html
<img src="/images/doggie.png" width="100px" class="img-responsive"/>
```

erb
```html
<%= image_tag 'doggie.png', width: "100px", class:"img-responsive" %>
```

### Forms, Labels, and Inputs

HTML
```html
<form action="/articles" class="form">
  <label for="title">Title</label>
  <input type="text" name="article[title]" placeholder="Title text here..."/>
  <button type="submit" class="btn btn-default">Publish</button>
</form>
```

erb
```html
<%= form_for @article, class:"form" do |f| %>
  <%= f.label :title %>
  <%= f.text_field :title %><br />
  <%= f.submit "Publish", class:"btn btn-default" %>
<% end %>
```

Also ```radio_button("article", "category", "rails")``` and ```check_box("article", "validated")```

### Distance of Time in Words (e.g. crazy sh*t)


```ruby
distance_of_time_in_words(Time.now, Time.now + 15.seconds)
# => less than a minute
```

Number Helpers
```ruby
number_to_human_size(1234)          # => 1.2 KB
number_to_human_size(1234567)       # => 1.2 MB
number_to_phone(1235551234) # => 123-555-1234
```

"Humanize" a variable name
```ruby
'employee_salary'.humanize              # => "Employee salary"
'author_id'.humanize                    # => "Author"
'author_id'.humanize(capitalize: false) # => "author"
```

### Other built-in Rails helpers worth mentioning
```yield```, ```content_for```
