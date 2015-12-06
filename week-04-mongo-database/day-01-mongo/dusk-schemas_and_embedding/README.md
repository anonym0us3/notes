# Relationships and Embedding in Mongo


## Learning Objectives

| Objectives |
| :---- |
| Describe one-to-one, one-to-many, and many-to-many data relationships |
| Build the appropriate queries for nested data relationships |
| Use an "Embedded" pattern to associate resources with Mongoose |
| Create, update, and delete data for the nested resource |

## Motivation

Real-world data usually consists of different types of things that are related to each other in some way. A banking app might need to track employees, customers, and accounts. A food ordering app needs to know about restaurants, menus, and its users!  We've seen that when data is very simple, we can combine it all into one model.  When data is more complex or less closely tied together, we often create two or more related models.

Today we'll look at one way to think about relationships between two data records. The first is *cardinality* - how many of each type of thing participate in the relationship? The second deals with where data is stored.

## Cardinality

### One-to-One

Each person has one brain, and each (living human) brain belongs to one person.

<img src="https://raw.githubusercontent.com/sf-wdi-22-23/modules-23/master/w03-intro-backend-with-express/d4-weekend-lab/img/one_to_one.png" alt="one to one erd"  width="250">

One-to-one relationships can sometimes just be modeled with simple attributes. A person and a brain are both complex enough that we might want to have their data in different models, with lots of different attributes on each.


### One-to-Many

Each youtube creator has many videos, and each video was posted by one youtube creator.

<img src="https://raw.githubusercontent.com/sf-wdi-22-23/modules-23/master/w03-intro-backend-with-express/d4-weekend-lab/img/one_to_many.png" alt="one to many erd" width="250">

### Many-to-Many

Each student can go to many classes, and each class has many students.

<img src="https://raw.githubusercontent.com/sf-wdi-22-23/modules-23/master/w03-intro-backend-with-express/d4-weekend-lab/img/many_to_many.png" alt="many to many erd"  width="250">

### Entity Relationship Diagrams

Entity relationship diagrams (ERDs) represent the relationships between data or entities.

![Entity Relationship Diagram example](https://www.edrawsoft.com/images/examples/entity-relationship-diagram.png)

Note: Attributes can be represented as line items under a heading (like all of the Item1, Item2, Item3 under each heading above) or as ovals stemming from the heading's rectangle.  

<a href="http://docs.oracle.com/cd/A87860_01/doc/java.817/a81358/05_dev1.htm" target="_blank">More guidelines for ERDs</a>



## Embedding Data within a Database

**Embedded Data** is directly nested *inside* of other data. Each record has a copy of the data.

<img src="http://docs.mongodb.org/manual/_images/data-model-denormalized.png">

It is *efficient* to embed data because you don't have to make a separate request or a separate database query -- the first request or query gets you all the information you need.  

###Scenario  


How would you design the following?

* A `User` that has many `Tweets`?
* A `Food` that has many `Ingredients`?


### Setting Up Relationships with Mongoose

**Embedding Data**

```javascript
var tweetSchema = new Schema({
  body: {
    type: String,
    default: ""
  }
});

var userSchema = new Schema({
  username: {
    type: String,
    default: ""
  },
  tweets: [tweetSchema]   // EMBEDDING :D
});
```


## Route Design

Remember to always make "RESTful" routes. RESTful routes are the most popular modern convention for designing resource paths for nested data. Here is an example of an application that has routes for `Store` and `Item` models:

### RESTful Routing

| **HTTP Verb** | **Path** | **Description** |
|---|---|---|
| GET | /store | Get all stores |
| POST | /store | Create a store |
| GET | /store/:id | Get a store |
| DELETE | /store/:id | Delete a store |
| GET | /store/:store_id/items | Get all items from a store |
| POST | /store/:store_id/items | Create an item for a store |
| GET | /store/:store_id/items/:item_id | Get an item from a store |
| DELETE | /store/:store_id/items/:item_id | Delete an item from a store |

*In routes, avoid nesting resources deeper than shown above.*


## Embedded Data Example: To-Do Lists

Imagine you have a database of todo `Lists`, each with many `Todos`. Since todos only belong to one list, you could use embedded data to store todos inside the list they belong to. If you needed to update or delete a todo, you would first need to find the associated list, then the todo to update or delete.

```js
// List model

var mongoose = require('mongoose'),
    Schema = mongoose.Schema,
    // require Todo model
    Todo = require('./todo');

var ListSchema = new Schema({
  name: String,
  // embed todos in list
  todos: [TodoSchema]
});

var List = mongoose.model('List', ListSchema);
module.exports = List;
```

```js
// Todo model

var mongoose = require('mongoose'),
    Schema = mongoose.Schema;

var TodoSchema = new Schema({
  text: String,
  completed: Boolean
});

var Todo = mongoose.model('Todo', TodoSchema);
module.exports = Todo;
```

### Route to Create Embedded Data

```js
// create todo embedded in list
app.post('/api/lists/:listId/todos', function (req, res) {
  // set the value of the list id
  var listId = req.params.listId;

  // store new todo in memory with data from request body
  var newTodo = new Todo(req.body.todo);

  // find list in db by id and add new todo
  List.findOne({_id: listId}, function (err, foundList) {
    foundList.todos.push(newTodo);
    foundList.save(function (err, savedList) {
      res.json(newTodo);
    });
  });
});
```

### Route to Update Embedded Data

```js
// update todo embedded in list
app.put('/api/lists/:listId/todos/:id', function (req, res) {
  // set the value of the list and todo ids
  var listId = req.params.listId;
  var todoId = req.params.id;

  // find list in db by id
  List.findOne({_id: listId}, function (err, foundList) {
    // find todo embedded in list
    var foundTodo = foundList.todos.id(todoId);
    // update todo text and completed with data from request body
    foundTodo.text = req.body.todo.text;
    foundTodo.completed = req.body.todo.completed;
    foundList.save(function (err, savedList) {
      res.json(foundTodo);
    });
  });
});
```

### Route to Delete Embedded Data

```js
// delete todo embedded in list
app.delete('/api/lists/:listId/todos/:id', function (req, res) {
  // set the value of the list and todo ids
  var listId = req.params.listId;
  var todoId = req.params.id;

  // find list in db by id
  List.findOne({_id: listId}, function (err, foundList) {
    // find todo embedded in list
    var foundTodo = foundList.todos.id(todoId);
    // remove todo
    foundTodo.remove();
    foundList.save(function (err, savedList) {
      res.json(foundTodo);
    });
  });
});
```
