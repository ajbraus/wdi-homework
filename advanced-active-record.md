# Advanced Active Record

Active Record is Rails data layer or ORM. It can do basic queries with `find`, `find_by`, `where`, `order`, and `uniq`, but it can also do more advanced queries: `average`, `sum`, `pluck`, `join`, `includes`, and [many more](http://guides.rubyonrails.org/active_record_querying.html)

## `sum` & `average`

* **sum** - If you want to find the sum of a field for all records in your table you can call the sum method on the class that relates to the table. This method call will look something like this:

```ruby
Client.sum("orders_count")
```

* **average** - If you want to see the average of a certain number in one of your tables you can call the average method on the class that relates to the table. This method call will look something like this:

```ruby
Client.average("orders_count")
```

## Joins - `joins`

Sometimes you want to query resources based on conditions of their association's attributes. For example:

> Give me all the articles that have had comments created in the last hour.

or

> What are all the animals whose owners live in 94115 zipcode?

You can accomplish this through using the rails Active Record method `joins`. Say you wanted to return all categories for whom new articles had been created in the past 24 hours.

```ruby
time_range = (Time.now.midnight - 1.day)..Time.now.midnight
Category.joins(:articles).where(articles: { created_at: time_rage })
```

or all animals whose owners live in 94115 zip-code

```ruby
Animal.joins(:owner).where(owner: { zip_code: 94115 })
```

The same can be done for join two associations. Say you want all articles with a particular category that have comments added the past 24 hours.

```ruby
Article.joins(:category, :comments).where(comments: { created_at: time_rage }).where(category: { name: "Top Stories" })
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

More of an FYI, rails lets you create "scopes" of different models for ease of access. Careful with scopes because they can be a bit inflexible.

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
