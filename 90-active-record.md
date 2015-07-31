# Know Your Relationships!
| Objective                                                                     |  
| :-------------------                                                          |  
| Understand how to create one-to-many and many-to-many relationships in rails. |  
| Understand how to modify migrations to add foreign keys to tables             |  
| Understand how to create a join table                                         |  
| Understand how to create model instances when they have associations.         |  

Today we'll be:

 - Reviewing what you already learned about associations from Mongoose
 - Translating what you've learned into Rails
 - Discussing migrations. _This is a new concept for us!_

---

## Vocab

**Relational Database**

A relational database is one designed to efficiently query and structure relationships between data. The data is typically structured into tables with columns and rows. *Think SQL when you think Relational Database.*

**Model**

A model is a class that maps to the data relation (table) and potentially bridges tables. You can think of a model as the blueprint (class) for what each row of data is going to contain. Unlike a migration, you perform CRUD on instances of your models.

**Object Relational Mapper (ORM)**

An ORM is a an abstraction layer between our Relational Database and our "Object Oriented" Application. The role of the ORM is to map objects (classes/instances) to entries (tables/rows) in our database. This means we can use a high-level language, like Javascript or Ruby, to create and manipulate our data, instead of writing queries in raw SQL (a "Domain Specific Langauge"). Read more [here](http://stackoverflow.com/questions/1279613/what-is-an-orm-and-where-can-i-learn-more-about-it).

**Schema**

You can think of your database schema as a "living document", reflecting the current configuration (e.g. tables, columns, and data constraints) of the tables in your database. You generally DO NOT EDIT your schema file directly -- instead you create a new "migration" to handle the changes for you.

**Migration** a.k.a ‘schema evolution’ or ‘mutation’

Migrations provide us with a mechanism for changing/evolving our database schema over time, as well as a controlled way to "undo" or "roll back" those changes. Each migration represents an historical/incrimental change to our database schema (you can think of it like a git commit). Examples of migrations are creating, deleting and altering tables (and their existing columns). Before you can start manipulating your models, you *MUST* create and run a migration. QUESTION: Why didn't we use migrations in Mongo?


---

##Would you rather...

| ActiveRecord | SQL |
| :-------------------- | :------- |
| User.all | `SELECT * from users` |
| User.find(123) | `SELECT * from users WHERE users.id = 123 LIMIT 1` |
| user.posts | `SELECT * from posts WHERE posts.user_id = 123` |
| student.courses | `SELECT * FROM courses INNER JOIN enrollments ON courses.id = enrollments.course_id 	WHERE enrollments.student_id = 456	` |

---

## AciveRecord CRUD (in the Console)

Open up your terminal and navigate to the root of a recent rails project that you know has items in the database. Open up the console by typing ```rails console``` or ```rails c```.

**IMPORTANT: Here we will use a ```User``` model. Just replace ```User``` with a model that you have in your project.**

#### Create
* `User.create(first_name: "Abraham", last_name: "Lincoln")`
* `User.create(first_name: "Abraham", last_name: "Maslow")`

NB: See all your users with `User.all`


#### Update

* Find - `user = User.find(1)` #the number '1' passed into the find method corresponds to the id of the user it will find
* Set - `user.first_name = "Taco"`
* Save - `user.save`

**or**

* Find — `user = User.find(1)`
* Update — `user.update_attributes(first_name: "Taco")`

#### Delete

* Find - `user = User.find(1)`
* Destroy - `user.destroy`

#### More Finding

* `User.all` -> returns an array of allusers
* `User.find_by_last_name('Lincoln')` -> replace last_name with any param in your model. This command returns only the first user that meets the criteria.
* `User.where(first_name: 'Abraham')` -> returns an array of users that meet the criteria
* `User.first` -> finds first user
* `User.last` -> finds last user

---
