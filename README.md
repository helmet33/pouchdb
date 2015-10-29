###### Semantic Web and Linked Data - Exercise 6
# Introduction to PouchDB
In this exercise we will have a look at PouchDB, which is a CouchDB clone written in JavaScript.
It is a document-oriented database system.
We'll mainly follow the [PouchDB Getting Started Guide](http://pouchdb.com/getting-started.html) in this exercise.

## Exercises
1. Download this repository and install pouchdb in the package folder.

    ```sh
    > npm install --save pouchdb
    ```
	
1. In index.js, use require to include pouchdb in your code.

	```js
	var PouchDB = require('pouchdb');
	```

1. Create a new PouchDB database to store to-dos.

	```js
	var db = new PouchDB('todos');
	```

1. Add a function to create a to-do to the database.

	```js
	function addTodo(text) {
	  
	  var todo = {
		_id: new Date().toISOString(),
		title: text,
		completed: false
	  };
	  
	  db.put(todo, function callback(err, result) {
		if (!err) {
		  console.log('Successfully posted a todo!');
		}
	  });
	
	}
	```

1. Add a function to retreive all the to-dos in the database and print them on the console.

	```js
	function showTodos() {
	  db.allDocs({include_docs: true, descending: true}, function(err, doc) {
		console.log(doc.rows);
	  });
	}
	```

1. Add a function to update a to-do. For now the only update we'll allow is to have the to-do marked as completed.

	```js
	function completeTodo(todo) {
	  todo.completed = true;
	  db.put(todo);
	}
	```

1. Add a function to delete a to-do
	
	```js
	function deleteButtonPressed(todo) {
	  db.remove(todo);
	}
	```
	
1. Tell PouchDB to show us the to-dos on the console every time we change the database.

	```js
	db.changes({
	  since: 'now',
	  live: true
	}).on('change', showTodos);
	```

1. Create three to-dos: "Clean dog", "Wash car", "Drink coffee".
	
	```js
	addTodo("Clean dog");
	...
	```

1. List all the todos.
	
	```js
	showTodos();
	```
	
## Advanced exercises
1. Have showTodos store all of the to-dos in an array.

1. Update a to-do.

1. Delete a to-do.

## Notes

- [PouchDB Getting Started Guide](http://pouchdb.com/getting-started.html)

- [PouchDB homepage](http://pouchdb.com/)

- [CouchDB homepage](http://couchdb.apache.org/)

