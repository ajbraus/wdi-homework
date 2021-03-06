# 7 Things I Wish I Had Known About Rails

## 1) Skinny Controllers, Fat Models

> [Sitepoint](http://www.sitepoint.com/10-ruby-on-rails-best-practices/)

Arguably one of the most important ways to write clear and concise code in Ruby on Rails, the motto “Fat Model, Skinny Controller” refers to how the M and C parts of MVC ideally work together. Namely, any non-response-related logic should go in the model, ideally in a nice, testable method. Meanwhile, the “skinny” controller is simply a nice interface between the view and model.

In practice, this can require a range of different types of refactoring, but it all comes down to one idea: by moving any logic that isn’t about the response (for example, setting a flash message, or choosing whether to redirect or render a view) to the model (instead of the controller), not only have you promoted reuse where possible but you’ve also made it possible to test your code outside of the context of a request.

Let’s look at a simple example. Say you have code like this in your controller:


```ruby
@user = User.new(params[:user])
@user.first_name, @user.last_name = params[:user][:full_name].split(" ", 2)
```

You can move the second line to your User model like this:

```ruby
def full_name=(value)
  self.first_name, self.last_name = value.to_s.split(" ", 2)
end
```

Whenever you set the ```full_name``` attribute, your model will now automatically set the ```first_name``` and ```last_name``` attributes for you as well, even though ```full_name``` doesn’t exist in the database. Likewise, you’ll typically want to define a getter method, ```full_name```, that returns ```"#{first_name} #{last_name}"```.


## 2) byebug

[Byebug](https://github.com/deivid-rodriguez/byebug) is a wonderful gem for debugging code that ships in new rails projects. To use it just add ```byebug``` anywhere you have a question about, and then run that code. In your terminal, your server will stop at the word ```byebug``` and open up a REPL console at that moment in the code. You can debug models, controllers, even views. Try it out.

## 3) thin

Thin is another ruby server that is a bit of a tighter ship than plain old ```$ rails s```. Its less noisy, and it has stricter requirements more like the heroku environment. Try it out.

Gemfile

```gem 'thin'```

```$ bundle install```

```$ thin start```


## 4) rails console

The Rails Console is an awesome tool to debug or do a quick smoke test on your associations, methods, or just plain old ruby. Whatever runs in your console is the way it will run in your app. Just type this into your terminal in the root of a rails project and see what happens.

```$ rails c```

Let's imagine you just made a ```has_many``` ```belongs_to``` associations between a ```User``` model and a ```Post``` model. We know that ```@user.posts``` should give us an array of post objects. Great let's check that in the console quick.

```
u = User.first
u.posts
#=> []
```
Yay it worked! If the association were not setup correctly we would have gotten an error that ```.posts``` was not a valid method to call on a user instance.

## 5) Rails Magic to Ignore

Rails has a lot of magic and magical gems you can use. Here are some seductive pieces of magic that IMO you can ignore.

  ### has_and_belongs_to_many
Rails is so fancy with its awesome `has_many` and `belongs_to` methods. Wouldn't it be great if there were a model method for many-to-many relationships? Here it is: `has_and_belongs_to_many`. Oh man awesome, thanks rails. But wait, I'd like there to be data stored on the join table. And I'd like the join table to be named something reasonable like `reservations` or `follows` or `subscriptions` but I can't do any of that if I use this fancy method. Instead I should have used `has_many :through`.
  ### devise
Here is a fancy-pants gem for authentication. OMG it just works! Until you want to customize it. Oh that's not too hard. But wait now I want the controller logic to be a tinsy bit different. This is HORRRIBLE - AHHHHH I wish I had rolled my own authentication!
  ### acts_as_taggable
Rails has a fancy "tags" gem that creates a many-to-many relationship to a tags resource.
  ### remote: true
Rails allows you to make forms submit though AJAX simply by adding `remote: true` to a `form_for` method. But do not be seduced by this. It is better to just use jQuery.

## 6) Paperclip

[Paperclip](https://github.com/thoughtbot/paperclip) is a gem for saving images. The way it works is it exposes hooks in your model through the ```has_image``` method. This method behind the scenes sends and grabs images to a Amazon S3 bucket that you setup and then point to when configuring your resource that will have image attributes.

Once you ```brew install imagemagick``` and create an AWS S3 account and bucket you can get started with their [Quick Start Guide](https://github.com/thoughtbot/paperclip#quick-start)

This gem is brought to the world by Thoughtbot - one of the leading Ruby on Rails consulting companies.

## 7) Migrate data inside of data migrations (not just update tables)

"Migration" files in rails are made to create and update SQL tables and columns in our database. And they are great at it. They make it so our database is both versioned and easily reproducible on other machines. They act as a sort of story of how our database started and grew and changed.

One thing that is sometimes overlooked with migrations is that you can use them to update data in your database as well. They are "Data Migrations".

Example:

1. Say you started with a `name` column, but now you want to go back and make a `first` and a `last` column and make a `full_name` virtual attribute. In a new migration you should write something like this.

```

```
