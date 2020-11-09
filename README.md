# Comparing and contrasting using Elixir/Phoenix vs. Ruby on Rails for a MongoDB app

One of the advantages of 'NoSQL' database systems is that you can add columns to arbitrary rows in a table
whenever you feel like it, whereas with SQL, you have to change the whole table

Suppose you have table "People", with columns "First Name", "Middle Name" and "Last Name"

Middle Name is optional, so you already have a strange hack where some of the people have a Middle
Name, and some of them have a Middle Name of NULL, which means "it's not there"

In NoSQL systems like MongoDB, you can have rows in which Middle Name isn't there at all, and others,
in which it is

And suppose you have a huge table, where only a small number of rows need an additional column, eg. "Favorite Sport Team"

Most of your people don't care about sport, but if you add this column, you give them all a Favorite Sport Team,
with most of them set to NULL

In MongoDB, you can just add that new column to the rows which need it

To demonstrate this, I wrote an app in Ruby on Rails and React, https://github.com/pdxrod/mongo-db-react-rails-app,
and another in Elixir and Phoenix, https://github.com/pdxrod/simple_mongo_app

The Ruby on Rails solution was by far the easiest

Recreating the app in Phoenix, I found

- a lack of accurate online documentation

- the Phoenix app generator creates and app which is tightly-coupled to SQL, so you have to decouple it in numerous places
(hat-tip to https://medium.com/swlh/setup-phoenix-on-docker-with-mongodb-d411e24dd78c)

- by default, the Elixir MongoDB app creates a row with an id consisting of BSON.ObjectId("HEX-NUMBER"); I couldn't
find any way of searching using these ids, so I replaced them with just hex strings, eg. "5f9d79c5a9f74f0bfb2cb5cc"  

---

# Caveat

These apps are absolutely minimal, with no security, no NoSQL injection rejection, no HTML injection rejection,
no asking if you really want to delete this row, no cute CSS, etc.. They are just experiments to see "which is the most
productive application framework for a simple NoSQL app which enables the addition of arbitrary columns to a table?".

Neither of them are the basis of a production application! I take no responsibility for what this code does,
but welcome feedback

Oh, and the answer to the above question is - RUBY ON RAILS
