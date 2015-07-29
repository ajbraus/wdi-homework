#What I Wish I Had Known About Rails

## 1) Skinny Controllers, Fat Models

> [Sitepoint](http://www.sitepoint.com/10-ruby-on-rails-best-practices/)

Arguably one of the most important ways to write clear and concise code in Ruby on Rails, the motto “Fat Model, Skinny Controller” refers to how the M and C parts of MVC ideally work together. Namely, any non-response-related logic should go in the model, ideally in a nice, testable method. Meanwhile, the “skinny” controller is simply a nice interface between the view and model.

In practice, this can require a range of different types of refactoring, but it all comes down to one idea: by moving any logic that isn’t about the response (for example, setting a flash message, or choosing whether to redirect or render a view) to the model (instead of the controller), not only have you promoted reuse where possible but you’ve also made it possible to test your code outside of the context of a request.

Let’s look at a simple example. Say you have code like this:

```ruby
def index
  @published_posts = Post.all :conditions => {['published_at <= ?', Time.now]}
  @unpublished_posts = Post.all :conditions => {['published_at IS NULL OR published_at > ?', Time.now]}
end
```

You can change it to this:

```ruby
def index
  @published_posts = Post.all_published
  @unpublished_posts = Post.all_unpublished
end
```

Then, you can move the logic to your post model, where it might look like this:

```ruby
def self.all_published
  all :conditions => {['published_at <= ?', Time.now]}
end

def self.all_unpublished
  all :conditions => {['published_at IS NULL OR published_at > ?', Time.now]}
end
```

With the methods ```Post.all_published``` and ```Post.all_unpublished```, we’ve not only made it simpler to test our code, we’ve also made it possible to reuse that same set of conditions in another location.

## 2) byebug


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

## 5) Make Friends with The Asset Pipeline
## 2) Rails Magic to Ignore
  * has_and_belongs_to_many
  * devise
  * acts_as_taggable

## 6) Paperclip

[Paperclip](https://github.com/thoughtbot/paperclip) is a gem for saving images. The way it works is it exposes hooks in your model through the ```has_image``` method. This method behind the scenes sends and grabs images to a Amazon S3 bucket that you setup and then point to when configuring your resource that will have image attributes.

Once you ```brew install imagemagick``` and create an AWS S3 account and bucket you can get started with their [Quick Start Guide](https://github.com/thoughtbot/paperclip#quick-start)

This gem is brought to the world by Thoughtbot - one of the leading Ruby on Rails consulting companies.

## 7) Migrate data inside of data migrations (not just update tables)

"Migration" files in rails are made to create and update SQL tables and columns in our database. And they are great at it. They make it so our database is both versioned and easily reproducible on other machines. They act as a sort of story of how our database started and grew and changed.

One thing that is sometimes overlooked with migrations is that you can use them to update data in your database as well. They are "Data Migrations".

## 8) Rails API is a thing
## 9) ... Just brainstorming here
