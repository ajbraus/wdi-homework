# Week 5

# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Project One

## Objectives

**Your app should have all of the following:**

* **Express API** Implement a server-side JSON API with Express.
* **RESTful Routes** Design the routes in a [RESTful](http://restfulrouting.com/mappings/resources) manner.
* **MongoDB** Persist at least two models in a Mongo Database.
* **jQuery** Use jQuery to manipulate the DOM.
* **AJAX** Use jQuery to ask your server for JSON asynchronously with AJAX.
* **Underscore Templating** Render the JSON data on the client-side using underscore templates.
* **Testing** Write request tests for 50% of your app's API routes.
* **Model Relationship** Create a `has_many` relationship between the User and another model using either embedded or referenced data.
* **Visual Design** Use Bootstrap to kick-start your UI and UX.
* **Heroku** Deploy your app to Heroku.

## BONUS CHALLENGES

If you want to push yourself and learn something new, optionally consider doing some of the following with your app, but *please talk to an instructor* beforehand:

* **Data Validation** Validate data by handling incorrect inputs during sign up, such as unique email addresses and minimum password lengths. Use jQuery Validate.
* **Search** Build a form that allows users to search for data based on keywords.
* **A Map** Use gmaps.js or mapbox to add a map to your site.
* **Authentication** Enable users to sign up, log in, and log out.
* **Authorization** Disallow users from deleting content in other user's profiles. This means a user should not be able to delete a post (or other resource) if it is not theirs.
* **Many-to-Many** Set up a many-to-many relationship like "tags" on posts.
* **Email** Send emails with express-mailer
* **SMS** Send SMSs with the Twillio API
* **Payments** Add payments with stripe.com
* **External API** Use an external API to integrate rich data into your app.
* **Web-Scraping** Write a web-scraper to collect data from a website that doesn't have an API. Example technologies include [Casper](http://casperjs.org) or [Kimono](https://www.kimonolabs.com).
* **Web Sockets** Create an open, real-time connection between your server and client (e.g. live chatting). Check out [Socket.io](http://socket.io/) if you're interested in web sockets.
* **Whatever else you can think of!**

## TIMELINE

* **Friday, July 17th by 9:00am** - **REQUIRED**:  Submit your project proposal
  * Wireframes (simple/hand drawn are great)
  * User narratives / user stories ("Users can create a meal with various foods." or "As a SpaceBook user looking for new friends, I want to be able to update my location to my current planet.")
  * Models and DB design (ERD)

* **Weekend**
  - Build initial index file
    - add bootstrap
    - make a template to display the core resource (e.g. "Post", or "Article", or "Todo")
  - Use the template to show dummy data from an array in the client side javascript code (add jQuery)
  - Move array of static data to server (build server with 1 route to get all data)
  - Move array of static data to DB (add mongoose and seed local DB)

> It is NOT RECOMMENDED to do styling beyond using bootstrap css and components

* **Monday, July 20th** - **REQUIRED**:  Deploy your code to Heroku by end of day (EOD).
  - Build any forms or form templates
  - Add POST route(s)
  - Add route tests

* **Tuesday, July 21st**
	- Finish CRUD of your primary Resource
  - Push to Heroku

* **Wednesday, July 22nd** - Suggestion:
  - Add another resource or a "reach" feature
  - Push to Heroku

* **Thursday, July 23rd** - Suggestion:
  - Improve and customize styling
  - Final Push to Heroku

* **Friday, July 24th, 9:17am** - Project due and presentations!

## WHAT WE ARE LOOKING FOR
#### Code should be...

* Properly indented
* Frequently committed, with descriptive commit messages
* Commented
* DRY

## ACCESS TO INSTRUCTORS
We will schedule 1:1s throughout the week. We will also do mini lessons on certain topics if we notice that several people are running into the same issues.

## FINAL DELIVERABLES

* **REMEMBER to build from the "outside-in" - Templates->Scripts->Server->DB**
* **REMEMBER to work together, pair, and share code!**

* Completion of the **core requirements**
* A link to your website **hosted on Heroku**
* A link to your **source code on GitHub**
* A `README.md` file that serves as your **project documentation**
* A **presentation** of 7 minutes or less illustrating:
	* What is your project and what does it do?
	* What was your motivation to build it?
	* What are you proud of?
	* What would you do with more time?
	* What aspect presented the most challenges?

## GROUPS

### HAPPY CODING :)
