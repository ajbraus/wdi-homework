# SQL & Active Record

Rails Active Record module that all models inherit from gives you magical syntax for making queries on any SQL database. Active Record is 'opinionated' like the rest of rails, but it also is flexible enough to allow raw SQL queries.

Let's look at some comparisons of what SQL is written by Active Record.

> Reference: [RailsGuides Active Record Query Interface](http://guides.rubyonrails.org/active_record_querying.html)

You've already been using Active Record query method with the `find` method.

Active Record vs. SQL
```
Client.find(10)
SELECT * FROM clients WHERE (clients.id = 10) LIMIT 1

Client.first
SELECT * FROM clients ORDER BY clients.id ASC LIMIT 1

Client.last
SELECT * FROM clients ORDER BY clients.id DESC LIMIT 1
```

The most important Active Record query method is very simple:

```
  Client.where(first_name: 'Lifo')
  Client.where(locked: true)
  Client.where("orders_count = ?", params[:orders])
  Client.where("created_at >= :start_date AND created_at <= :end_date", {start_date: params[:start_date], end_date: params[:end_date]})
```

More advanced queries
```
Client.where(created_at: (Time.now.midnight - 1.day)..Time.now.midnight)
SELECT * FROM clients WHERE (clients.created_at BETWEEN '2008-12-21 00:00:00' AND '2008-12-22 00:00:00')
```

## Joins - `joins`

```
Client.joins('LEFT OUTER JOIN addresses ON addresses.client_id = clients.id')
SELECT clients.* FROM clients LEFT OUTER JOIN addresses ON addresses.client_id = clients.id
```

```
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

```
Category.joins(:articles)
```

```
SELECT categories.* FROM categories
  INNER JOIN articles ON articles.category_id = categories.id
```

```
Article.joins(:category, :comments)
```

```
SELECT articles.* FROM articles
  INNER JOIN categories ON articles.category_id = categories.id
  INNER JOIN comments ON comments.article_id = articles.id
```

## Eager Loading - `includes`

```
Client.includes(:address).limit(10)
```

```
SELECT * FROM clients LIMIT 10
SELECT addresses.* FROM addresses
  WHERE (addresses.client_id IN (1,2,3,4,5,6,7,8,9,10))
```

## Scopes

```
class Article < ActiveRecord::Base
  scope :published, -> { where(published: true) }
end

Article.published # => [published articles]
```
