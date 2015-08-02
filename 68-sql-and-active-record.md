# SQL & Active Record

Rails Active Record module that all models inherit from gives you magical syntax for making queries on any SQL database. Active Record is 'opinionated' like the rest of rails, but it also is flexible enough to allow raw SQL queries.

Let's look at some comparisons of what SQL is written by Active Record.

> Reference: [RailsGuides Active Record Query Interface](http://guides.rubyonrails.org/active_record_querying.html)

You've already been using Active Record query method with the `find`, `first` and `last` methods.

Active Record vs. SQL
```sql
Client.find(10)
SELECT * FROM clients WHERE (clients.id = 10) LIMIT 1

Client.first
SELECT * FROM clients ORDER BY clients.id ASC LIMIT 1

Client.last
SELECT * FROM clients ORDER BY clients.id DESC LIMIT 1
```

The most important Active Record query method is `where` and it takes hash parameters or a string of raw SQL.

```ruby
Client.where(first_name: 'Lifo')
Client.where(locked: true)
Client.where("orders_count = ?", params[:orders])
Client.where("created_at >= :start_date AND created_at <= :end_date", {start_date: params[:start_date], end_date: params[:end_date]})
```

More advanced queries
```ruby
Client.where(created_at: (Time.now.midnight - 1.day)..Time.now.midnight)
SELECT * FROM clients WHERE (clients.created_at BETWEEN '2008-12-21 00:00:00' AND '2008-12-22 00:00:00')
```

## Joins - `joins`

Let's look at a more complex example of `joins`. In SQL we create associations through join tables. Rails abstracts away from the literal join into a simple method.

Take this example of relationships. Draw a schema drawing for this set of models.

```ruby
class Category < ActiveRecord::Base
  has_many :articles
end

class Article < ActiveRecord::Base
  belongs_to :category
  has_many :comments
  has_many :tags
end

class Comment < ActiveRecord::Base
  belongs_to :article
  has_one :guest
end

class Guest < ActiveRecord::Base
  belongs_to :comment
end

class Tag < ActiveRecord::Base
  belongs_to :article
end
```

To get all or a subset of categories and their articles out of the database you would have to perform a join in SQL.

```sql
SELECT categories.* FROM categories
  INNER JOIN articles ON articles.category_id = categories.id
```

But in Rails you can simply call `joins`. Say you wanted to return all categories for whom new articles had been created in the past 24 hours.

```ruby
time_range = (Time.now.midnight - 1.day)..Time.now.midnight
Category.joins(:articles).where(articles: { created_at: time_rage })
```

The same can be done for join two associations. Say you want all articles with a particular category that have comments added the past 24 hours.

```ruby
Article.joins(:category, :comments).where(comments: { created_at: time_rage }).where(category: "Top Stories")
```

## Eager Loading - `includes`

By default Rails uses **lazy loading** meaning it only actually fetches the data from the database you actually use at the last possible minute, but sometimes its more efficient if rails `includes` associated records with an initial request. Say if you want clients' address information upfront in one db query, instead of doing 10 db queries as you iterate over the clients address info. (This can speed up your server a lot!)

```sql
SELECT * FROM clients LIMIT 10
SELECT addresses.* FROM addresses
  WHERE (addresses.client_id IN (1,2,3,4,5,6,7,8,9,10))
```

```ruby
Client.includes(:address).limit(10)
```

## Scopes

More of an FYI, rails lets you create "scopes" of different models for ease of access.

```
class Article < ActiveRecord::Base
  scope :published, -> { where(published: true) }
end

Article.published # => [published articles]
```

# Challenges

1. Make a `where` query using the hash parameter on a model in one of your projects.
2. Make a `where` query using the raw SQL string parameter.
3. Make a query that `joins` two models.
4. Make a request and include an association.
