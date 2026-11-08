# The Complete Developers Guide to MongoDB #
## Section 1: Let's Start ##
### MongoDB Setup on macOS ###
1. [Homebrew](https://brew.sh/)
2. Add MongoDB repository to Homebrew: `brew tap mongodb/brew`
3. Run update: `brew update`
4. Install community edition of MongoDB: `brew install mongodb-community@6.0`
5. Starting: `brew services start mongodb-community@6.0`
6. Stopping: `brew services stop mongodb-community@6.0`
7. Connecting to Mongo shell: `mongosh` **(M)**
8. [Official documentation](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-os-x/)

### MongoDB Setup on Windows ###
1. [MSI installer](https://www.mongodb.com/try/download/community)
	1. Include MongoDB compass
		1. GUI
2. [Official documentation](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-windows/)
3. [Mongosh](https://www.mongodb.com/try/download/shell)
	1. Windows 64-bit (8.1+) MSI
	2. `PATH` will be set automatically
4. Usage:
	1. Windows Services Console > Start MongoDB service
	2. Windows Services Console > Stop MongoDB service
5. Running command shell: `mongosh` **(M)**

### Using MongoDB Compass on macOS ###
1. [MongoDB compass](https://www.mongodb.com/try/download/compass)
	1. Pre-requisite: MongoDB server must be running
	2. Save & Connect

### Using MongoDB Compass on Windows ###
1. Already installed
2. MongoDB server must be running
3. Launch Compass
	1. Save & Connect

## Section 2: A Quick ES6 Refresher ##
### A Refresher on Promises ###
1. Promises:
	1. `/promises`
		1. `code .`
			1. `index.html`
			
			```
			<head>
			</head>
			<body>
			  <button>Click!</button>
			  
			  <script>
			    console.log('game is starting');
			  </script>
			</body>
			```
			
				1. `open index.html`

### Let's Play A Game ###
1. How does the game work?
	1. Refresh of the document: start the game
	2. User needs to click at least 6 times
		1. Within 2 seconds
			1. If >= 6, they won
			2. If < 6, they lost
2. index.html

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>

<body>
  <button>Click!</button>

  <script>
    let counter = 0;

    document.querySelector('button').addEventListener('click', () => {
      counter++;
    });

    setTimeout(() => {
      if (counter > 5) {
        alert('You won!');
      } else {
        alert('You lost!');
      }
    }, 2000);
  </script>
</body>

</html>
```

### Winning the Game ###
1. Standalone package. User decides what to do if user wins or loses.
2. index.html

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>

<body>
  <button>Click!</button>

  <script>
    function startGame() {
      let counter = 0;

      document.querySelector('button').addEventListener('click', () => {
        counter++;
      });

      return new Promise((resolve, reject) => {
        setTimeout(() => {
          if (counter > 5) {
            resolve(counter);
          } else {
            reject(counter);
          }
        }, 2000);
      });
    }
    startGame()
      .then((counter) => alert('You win! Your clicks: ' + counter))
      .catch((counter) => alert('You lost! Your clicks: ' + counter));
  </script>
</body>

</html>
```

### Behind the Scenes with Promises ###
1. Promise: A tool for managing async code flow in our application
	1. Any code that is going to execute at some time in the future
2. `resolve`, `reject` - Used to manipulate the state of a promise
	1. States:
		1. 'unresolved' - waiting for something to finish
		2. 'resolved' - something finished and it all wenk ok
			1. We decide to transition to this state
			2. If we call `resolved` function, Promise transitions to `resolved` state
				1. calls the function passed to `.then`
		3. 'rejected' - something finished and something went bad
			1. If we call `rejected` function, Promise transitions to `rejected` state
				1. calls the function passed to `.catch`
3. Libraries use Promises
	1. We need to use the consuming side of the `Promise`

## Section 3: Core Fundamentals of MongoDB ##
### Where Do We Use Mongo? ###
1. It is a database (stores data)
2. Uses a webserver
	1. Node, Python, Ruby, ...
	2. Outside traffic is filtered here
		1. It has security rules
3. Mongoose: ORM or ODM (Object Data Mapping)
	1. Helps working with MongoDB easier

### Fundamentals of MongoDB ###
1. How to connect browser and Mobile App to MongoDB?
	1. We don't
2. Data storage
	1. We can have multiple databases inside a single Mongo instance
		1. Each database has multiple collections
			1. Traditionally, one collection for each type of resource (like a table)
				1. Collection of states
				2. Collection of books
3. Core Mongoose/Mongo - next

### A Last Touch of Setup ###
1. Core Mongoose/Mongo
	1. Create data
	2. Read data
	3. Update data
	4. Destroy data
2. Workspace: `prod` directory
	1. `prod/users`

## Section 4: A Test Driven Experience ##
### Project Overview ###
1. `prod/users`
	1. `npm init`
		1. All defaults
	2. `npm install --save mocha nodemon mongoose`
2. Application:
	1. Mongo database
		1. Collection of Users
	2. Mongoose (library)
	3. Mocha (testing framework)
		1. To ensure we are inserting data into MongoDB
	4. Project structure:
		1. `src/user.js` (for mongoose)
		2. `test/`
			1. `/create_test.js`
			2. `/read_test.js`
			3. `/update_test.js`
			4. `/destroy_test.js`

### The Test Helper File ###
1. Test setup
	1. `test/test_helper.js`
		1. Logic:
			1. Mocha starts
			2. Tell mongoose to connect to Mongo (mongoose is a js package)
			3. ...wait...
			4. Mongoose connects to Mongo
			5. Connection Successful? Run tests
			6. Connection Failed? Show Error
	2. Code:
	
	```
	const mongoose = require('mongoose');

	mongoose.connect('mongodb://localhost:27017/users_test');
	mongoose.connection
	  .once('open', () => console.log('Good to go!'))
	  .on('error', (error) => console.warn('Warning', error));
	```
	
		1. Fix: `mongodb://127.0.0.1:27017/users_test`

### Mongoose Connection Helper ###
1. `require('mongoose')`
	1. Includes the library
2. `mongoose.connect(...)` - connects to MongoDB
	1. `users_test` - database
		1. It is automatically created if it does not exist
3. `.once(...)`
	1. Event handler
		1. Watch for mongoose to emit an event called 'open' only once and then run the passed function
4. `.on(...)`
	1. Event handler
		1. Watch for mongoose to emit an event called 'error' and then run the passed function
5. `node test/test_helper.js`

### Mongoose Models ###
1. How does Mongoose work?
	1. User Model (represents a record in a collection) - It has functions to work with the collection: Used to construct a single record in a database
		1. Schema: Tells what properties each record will have and what their data types are
			1. `name`: `string`
2. `src/user.js`

```
const mongoose = require('mongoose');
const Schema = mongoose.Schema;
```

### More on Models ###
1. `src/user.js`

```javascript
const mongoose = require('mongoose'); // Import the Mongoose library, which is an Object Data Modeling (ODM) library for MongoDB and Node.js. It provides a schema-based solution to model application data.
const Schema = mongoose.Schema; // `Schema` is a constructor function that allows us to define the structure of documents in a MongoDB collection. It is used to create a new schema for the 'user' collection.

const UserSchema = new Schema({
  name: String, // The name of the user. It is a string data type.
});

const User = mongoose.model('user', UserSchema); // 'user' is a collection. It is automatically created in the database if it doesn't exist. `UserSchema` is the schema for the collection. It defines the structure of the documents in the collection. `User` is a class that we can use to create new users and interact with the 'user' collection in the database.

module.exports = User; // Export the User model so that it can be used in other files.

```

### The Basics of Mocha ###
1. `test/create_test.js` - `_test.js` should be used
2. Mocha test structure:

```
Describe # function/block
  it # block/function
  it
  it
  it
```

```
describe('Creation of records', () => {
  it('saves a user', () => {
    
  });
}); // Mocha runs one `it` at a time. Each `it` is a test case. The first argument is a string that describes what the test case does. The second argument is a function that contains the code for the test case. In this case, we are testing the creation of records in the database. The `it` block is currently empty, meaning no actual test logic has been implemented yet.
```

### Running Mocha Tests ###
1. `test/create_test.js`

```
const assert = require('assert');

describe('Creation of records', () => {
  it('saves a user', () => {
    assert(1 + 1 == 2);
  });
}); // Mocha runs one `it` at a time. Each `it` is a test case. The first argument is a string that describes what the test case does. The second argument is a function that contains the code for the test case. In this case, we are testing the creation of records in the database. The `it` block is currently empty, meaning no actual test logic has been implemented yet.
```

2. package.json

```
"test": "mocha"
```

3. Running: `npm run test`

### Constructing Model Instances ###
1. `create_test.js`

```
const assert = require('assert'); // Import the assert module, which provides a set of assertion functions for verifying invariants. It is used in testing to check if certain conditions are met.
const User = require('../src/user'); // Import the User model from the user.js file. This model is used to interact with the 'user' collection in the MongoDB database.

describe('Creation of records', () => {
  it('saves a user', () => {
    const joe = new User({ name: 'Joe' }); // Create a new instance of the User model with the name 'Joe'. This instance represents a document that will be saved to the 'user' collection in the database.
  });
}); // Mocha runs one `it` at a time. Each `it` is a test case. The first argument is a string that describes what the test case does. The second argument is a function that contains the code for the test case. In this case, we are testing the creation of records in the database. The `it` block is currently empty, meaning no actual test logic has been implemented yet.
```

### Saving Users to Mongo ###
1. `ObjectId("....")` - Helper. An object that helps Mongo keep track of ids
	1. Later
2. `create_test.js`

```javascript
const assert = require('assert'); // Import the assert module, which provides a set of assertion functions for verifying invariants. It is used in testing to check if certain conditions are met.
const User = require('../src/user'); // Import the User model from the user.js file. This model is used to interact with the 'user' collection in the MongoDB database.

describe('Creation of records', () => {
  it('saves a user', () => {
    const joe = new User({ name: 'Joe' }); // Create a new instance of the User model with the name 'Joe'. This instance represents a document that will be saved to the 'user' collection in the database.
    joe.save();
  });
}); // Mocha runs one `it` at a time. Each `it` is a test case. The first argument is a string that describes what the test case does. The second argument is a function that contains the code for the test case. In this case, we are testing the creation of records in the database. The `it` block is currently empty, meaning no actual test logic has been implemented yet.
```

### Dropping Collections ###
1. Plan:

```
Mocha starts
Empty Database
Test #1
Empty Database
Test #2
Empty Database
...
```

2. `test_helper.js`

```
const mongoose = require('mongoose');

mongoose.connect('mongodb://127.0.0.1:27017/users_test');
mongoose.connection
  .once('open', () => console.log('Good to go!'))
  .on('error', (error) => console.warn('Warning', error));

beforeEach(() => {
  mongoose.connection.collections.users.drop();
});
```

### Mocha's Done Callback ###
1. `done` - callback
	1. Provided by `mocha`
		1. Once it is called, the tests will continue running
2. `test_helper.js`

```javascript
const mongoose = require('mongoose');

mongoose.connect('mongodb://127.0.0.1:27017/users_test');
mongoose.connection
  .once('open', () => console.log('Good to go!'))
  .on('error', (error) => console.warn('Warning', error));

beforeEach((done) => {
  mongoose.connection.collections.users.drop(() => {
    // Ready to run the next test!
    done(); // The `done` function is a callback provided by Mocha that signals the completion of an asynchronous operation. In this case, it is called after the 'users' collection is dropped, indicating that the database is ready for the next test case to run.
  }); // Callback function is executed after the 'users' collection is dropped. This ensures that the database is cleared before each test case runs, preventing interference between tests and ensuring that each test starts with a clean state.
});
```

### Mongoose's isNew Property ###
1. `joe.isNew === true`
	1. If record is not saved in db yet, `isNew` is set to `true`
	2. If record is saved in db, `isNew` is set to `false`
2. `test_helper.js` (fix)

```javascript
const mongoose = require('mongoose');

before(async function () {
  this.timeout(10000); // Increase the timeout for the before hook to 10 seconds. This is useful if the database connection takes longer than the default timeout period.

  await mongoose.connect('mongodb://127.0.0.1:27017/users_test');
});

beforeEach(async function () {
  this.timeout(10000); // Increase the timeout for the beforeEach hook to 10 seconds. This is useful if the database connection takes longer than the default timeout period.

  await mongoose.connection.collections.users.drop(); // Drop the 'users' collection before each test to ensure a clean state. This prevents tests from interfering with each other by ensuring that the database is empty before each test runs.
});

after(async function () {
  await mongoose.connection.dropDatabase(); // Drop the entire test database after all tests have completed. This is important to clean up any data that was created during testing and to ensure that the database is in a clean state for future tests.
  await mongoose.connection.close(); // Close the database connection after all tests have completed. This is important to free up resources and prevent memory leaks.
});
```

3. `create_test.js`

```javascript
const assert = require('assert'); // Import the assert module, which provides a set of assertion functions for verifying invariants. It is used in testing to check if certain conditions are met.
const User = require('../src/user'); // Import the User model from the user.js file. This model is used to interact with the 'user' collection in the MongoDB database.

describe('Creation of records', () => {
  it('saves a user', async () => {
    const joe = new User({ name: 'Joe' }); // Create a new instance of the User model with the name 'Joe'. This instance represents a document that will be saved to the 'user' collection in the database.
    await joe.save();
    // Has joe been saved successfully?
    assert(!joe.isNew); // The `isNew` property is a boolean that indicates whether the document has been saved to the database. If `isNew` is false, it means the document has been successfully saved. The `assert` function checks if `!joe.isNew` is true, and if not, it will throw an error, indicating that the test has failed.
  });
}); // Mocha runs one `it` at a time. Each `it` is a test case. The first argument is a string that describes what the test case does. The second argument is a function that contains the code for the test case. In this case, we are testing the creation of records in the database. The `it` block is currently empty, meaning no actual test logic has been implemented yet.
```

### Default Promise Implementation ###
1. Mongoose has default Promise library
	1. We can plugin our own promise library
		1. bluebird
		2. q
		3. ES6 Promise
2. `test_helper.js`

```javascript
mongoose.Promise = global.Promise; // Use the global Promise implementation for Mongoose. This ensures that Mongoose uses native Promises instead of its own implementation, which can help avoid issues with compatibility and performance.
```

3. Hook to execute once before all tests

```javascript
before(async function () {
  this.timeout(10000); // Increase the timeout for the before hook to 10 seconds. This is useful if the database connection takes longer than the default timeout period.

  await mongoose.connect('mongodb://127.0.0.1:27017/users_test');
  await mongoose.connection
    .once('open', () => {
      console.log('Connection has been made, now make fireworks...');
    })
    .on('error', (error) => {
      console.log('Connection error:', error);
    }); // Connect to the MongoDB database at the specified URL. The `once` method listens for the 'open' event, which indicates that the connection has been successfully established. The `on` method listens for the 'error' event, which indicates that there was an error connecting to the database. If an error occurs, it will be logged to the console.
});
```

### Test Setup for Finding Users ###
1. Finding records:
	1. Two ways
		1. Find a user with a name of 'Joe'
			1. Search Query (all possible users)
		2. Find a particular user with this given Id
			1. Lookup (specific)
2. `test/reading_test.js`

```javascript
const assert = require('assert'); // Import the assert module from Node.js. This module provides a set of assertion functions for verifying invariants in your code. In this case, it is used to check if the user has been saved successfully to the database.
const User = require('../src/user'); // Import the User model from the user.js file. This model is used to interact with the 'user' collection in the MongoDB database.

describe('Reading users out of the database', () => {
  let joe; // Declare a variable 'joe' to hold the user instance. This variable will be used in the tests to reference the user that is created and saved to the database.

  beforeEach(async () => {
    joe = new User({ name: 'Joe' }); // Create a new instance of the User model with the name 'Joe'. This instance represents a document that will be saved to the 'user' collection in the database.
    await joe.save(); // Save the 'Joe' user to the database. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. This ensures that the user is saved before any tests are run.
  });

  it('finds all users with a name of Joe', async () => {});
});
```

### Making Mongo Queries ###
1. Two query methods:
	1. `User.find(criteria)`
		1. Find all the users that match the given criteria. Returns an array.
	2. `User.findOne(criteria)`
		1. Find the first user that matches the criteria. Returns a single record.
			1. It stops the query after finding one record
2. `reading_test.js`

```javascript
const assert = require('assert'); // Import the assert module from Node.js. This module provides a set of assertion functions for verifying invariants in your code. In this case, it is used to check if the user has been saved successfully to the database.
const User = require('../src/user'); // Import the User model from the user.js file. This model is used to interact with the 'user' collection in the MongoDB database.

describe('Reading users out of the database', () => {
  let joe; // Declare a variable 'joe' to hold the user instance. This variable will be used in the tests to reference the user that is created and saved to the database.

  beforeEach(async () => {
    joe = new User({ name: 'Joe' }); // Create a new instance of the User model with the name 'Joe'. This instance represents a document that will be saved to the 'user' collection in the database.
    await joe.save(); // Save the 'Joe' user to the database. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. This ensures that the user is saved before any tests are run.
  });

  it('finds all users with a name of Joe', async () => {
    const users = await User.find({ name: 'Joe' }); // Use the Mongoose 'find' method to retrieve all users from the database with the name 'Joe'. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. The result is an array of user documents that match the query.
  });
});
```

### The ID Property - A Big Gotcha ###
1. `_id` property is assigned to a new record even if it is not saved to the database
	1. Mongoose generates a unique id
2. `reading_test.js`

```javascript
const assert = require('assert'); // Import the assert module from Node.js. This module provides a set of assertion functions for verifying invariants in your code. In this case, it is used to check if the user has been saved successfully to the database.
const User = require('../src/user'); // Import the User model from the user.js file. This model is used to interact with the 'user' collection in the MongoDB database.

describe('Reading users out of the database', () => {
  let joe; // Declare a variable 'joe' to hold the user instance. This variable will be used in the tests to reference the user that is created and saved to the database.

  beforeEach(async () => {
    joe = new User({ name: 'Joe' }); // Create a new instance of the User model with the name 'Joe'. This instance represents a document that will be saved to the 'user' collection in the database.
    await joe.save(); // Save the 'Joe' user to the database. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. This ensures that the user is saved before any tests are run.
  });

  it('finds all users with a name of Joe', async () => {
    const users = await User.find({ name: 'Joe' }); // Use the Mongoose 'find' method to retrieve all users from the database with the name 'Joe'. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. The result is an array of user documents that match the query.
    assert(users[0]._id.toString() === joe._id.toString()); // Use the 'assert' function to check if the '_id' of the first user in the 'users' array matches the '_id' of the 'joe' instance. This verifies that the user we created and saved earlier can be successfully retrieved from the database. If the assertion fails, an error will be thrown, indicating that the test has failed.
  });
});
```

### Automating Tests with Nodemon ###
1. `nodemon` - automatically run tests when we change any file
2. `package.json`

```json
"test": "nodemon --exec 'mocha -R min'"
```

	1. `-R min` - for formatting text output
		1. Condensed test output
		2. Clear out previous test results
	2. Windows:
	
	```
	"test": "nodemon --exec \"mocha -R min\""
	```
	
3. `mocha --watch` - some compatibility with mongoose

### Finding Particular Records ###
1. `User.findOne(...)`

```javascript
  it('find a user with a particular id', async () => {
    const user = await User.findOne({ _id: joe._id }); // Use the Mongoose 'findOne' method to retrieve a single user from the database with the specific '_id' of the 'joe' instance. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. The result is a single user document that matches the query.
    assert(user.name === 'Joe'); // Use the 'assert' function to check if the 'name' of the retrieved user matches 'Joe'. This verifies that the user we created and saved earlier can be successfully retrieved from the database using its unique '_id'. If the assertion fails, an error will be thrown, indicating that the test has failed.
  });
```

### Many Ways to Remove Records ###
1. `test/delete_test.js`

```javascript

```

2. Model Class: `User`
	1. `remove`
		1. Takes in a criteria and delete matching records
	2. `findOneAndRemove`
	3. `findByIdAndRemove`
3. Model Instance: `joe`
	1. `remove`
		1. Remove itself

### Class Based Removes ###
1. `delete_test.js`

```javascript
const assert = require('assert');
const User = require('../src/user');

describe('Deleting a user', () => {
  let joe;

  beforeEach(async () => {
    joe = new User({ name: 'Joe' });
    await joe.save();
  });

  it('model instance remove', async () => {
    await joe.deleteOne(); // Use the `deleteOne` method on the `joe` instance to delete it from the database. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. The `deleteOne` method is an instance method that removes the specific document from the collection.
    const user = await User.findOne({ name: 'Joe' }); // Use the Mongoose `findOne` method to search for a user with the name 'Joe' in the database. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. The result is either the user document that matches the query or `null` if no matching document is found.
    assert(user === null); // Use the `assert` function to check if the result of the `findOne` query is `null`. If it is `null`, it means that the user has been successfully deleted from the database. If the assertion fails, an error will be thrown, indicating that the test has failed.
  });

  it('class method remove', async () => {
    await User.deleteMany({ name: 'Joe' }); // Use the Mongoose `deleteMany` method to delete all users with the name 'Joe' from the database. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. The `deleteMany` method is a class method that removes all documents that match the specified query from the collection.
    const user = await User.findOne({ name: 'Joe' }); // Use the Mongoose `findOne` method to search for a user with the name 'Joe' in the database. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. The result is either the user document that matches the query or `null` if no matching document is found.
    assert(user === null); // Use the `assert` function to check if the result of the `findOne` query is `null`. If it is `null`, it means that all users with the name 'Joe' have been successfully deleted from the database. If the assertion fails, an error will be thrown, indicating that the test has failed.
  });

  it('class method findOneAndRemove', async () => {});

  it('class method findByIdAndRemove', async () => {});
});
```

### More Class Based Removals ###
1. `delete_test.js`

```javascript
const assert = require('assert');
const User = require('../src/user');

describe('Deleting a user', () => {
  let joe;

  beforeEach(async () => {
    joe = new User({ name: 'Joe' });
    await joe.save();
  });

  it('model instance remove', async () => {
    await joe.deleteOne(); // Use the `deleteOne` method on the `joe` instance to delete it from the database. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. The `deleteOne` method is an instance method that removes the specific document from the collection.
    const user = await User.findOne({ name: 'Joe' }); // Use the Mongoose `findOne` method to search for a user with the name 'Joe' in the database. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. The result is either the user document that matches the query or `null` if no matching document is found.
    assert(user === null); // Use the `assert` function to check if the result of the `findOne` query is `null`. If it is `null`, it means that the user has been successfully deleted from the database. If the assertion fails, an error will be thrown, indicating that the test has failed.
  });

  it('class method remove', async () => {
    await User.deleteMany({ name: 'Joe' }); // Use the Mongoose `deleteMany` method to delete all users with the name 'Joe' from the database. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. The `deleteMany` method is a class method that removes all documents that match the specified query from the collection.
    const user = await User.findOne({ name: 'Joe' }); // Use the Mongoose `findOne` method to search for a user with the name 'Joe' in the database. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. The result is either the user document that matches the query or `null` if no matching document is found.
    assert(user === null); // Use the `assert` function to check if the result of the `findOne` query is `null`. If it is `null`, it means that all users with the name 'Joe' have been successfully deleted from the database. If the assertion fails, an error will be thrown, indicating that the test has failed.
  });

  it('class method findOneAndRemove', async () => {
    await User.findOneAndDelete({ name: 'Joe' }); // Use the Mongoose `findOneAndDelete` method to find and delete a single user with the name 'Joe' from the database. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. The `findOneAndDelete` method is a class method that finds a single document that matches the specified query and removes it from the collection.
    const user = await User.findOne({ name: 'Jone' }); // Use the Mongoose `findOne` method to search for a user with the name 'Joe' in the database. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. The result is either the user document that matches the query or `null` if no matching document is found.
    assert(user === null); // Use the `assert` function to check if the result of the `findOne` query is `null`. If it is `null`, it means that the user with the name 'Joe' has been successfully deleted from the database. If the assertion fails, an error will be thrown, indicating that the test has failed.
  });

  it('class method findByIdAndRemove', async () => {
    await User.findByIdAndDelete(joe._id); // Use the Mongoose `findByIdAndDelete` method to find and delete a user by its unique `_id`. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. The `findByIdAndDelete` method is a class method that finds a single document by its `_id` and removes it from the collection.
    const user = await User.findOne({ _id: joe._id }); // Use the Mongoose `findOne` method to search for a user with the specific `_id` of the `joe` instance in the database. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. The result is either the user document that matches the query or `null` if no matching document is found.
    assert(user === null); // Use the `assert` function to check if the result of the `findOne` query is `null`. If it is `null`, it means that the user with the specific `_id` has been successfully deleted from the database. If the assertion fails, an error will be thrown, indicating that the test has failed.
  });
});
```

### The Many Ways to Update Records ###
1. Updating
	1. Model Class
		1. `update`
		2. `findOneAndUpdate`
		3. `findByIdAndUpdate`
	2. Model Instance
		1. `update`
		2. '`set`' and '`save`'
2. `test/update_test.js`

```javascript
const assert = require('assert');
const User = require('../src/user');

describe('Updating records', () => {
  let joe;

  beforeEach(async () => {
    joe = new User({ name: 'Joe' });
    await joe.save();
  });

  it('instance set and save', async () => {});
});
```

### Set and Save for Updating Records ###
1. `test/udpate_test.js`

```javascript
const assert = require('assert');
const User = require('../src/user');

describe('Updating records', () => {
  let joe;

  beforeEach(async () => {
    joe = new User({ name: 'Joe' });
    await joe.save();
  });

  it('instance set and save', async () => {
    joe.set('name', 'Alex'); // Use the `set` method on the `joe` instance to change the value of the 'name' field to 'Alex'. This method allows us to update the properties of the document before saving it to the database. The `set` method takes two arguments: the name of the field to update and the new value for that field.
    await joe.save(); // Use the `save` method on the `joe` instance to save the updated document to the database. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. The `save` method persists the changes made to the document in the database.
    const users = await User.find({}); // Use the Mongoose `find` method to retrieve all users from the database. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. The result is an array of user documents that match the query.
    assert(users.length === 1);
    assert(users[0].name === 'Alex');
  });
});
```

### Model Instance Updates ###
1. `update_test.js`

```javascript
const assert = require('assert');
const User = require('../src/user');

describe('Updating records', () => {
  let joe;

  beforeEach(async () => {
    joe = new User({ name: 'Joe' });
    await joe.save();
  });

  async function assertName(operation, name) {
    await operation(); // Execute the provided operation, which is expected to update the user's name in the database. This function takes an asynchronous function as an argument and awaits its completion before proceeding to the next steps.
    const users = await User.find({}); // Use the Mongoose `find` method to retrieve all users from the database. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. The result is an array of user documents that match the query.
    assert(users.length === 1); // Use the `assert` function to check if the length of the `users` array is equal to 1. This verifies that there is exactly one user in the database after the update operation. If the assertion fails, an error will be thrown, indicating that the test has failed.
    assert(users[0].name === name); // Use the `assert` function to check if the 'name' of the first user in the `users` array is equal to the provided `name`. This verifies that the user's name has been successfully updated in the database. If the assertion fails, an error will be thrown, indicating that the test has failed.
  }

  it('instance set and save', async () => {
    joe.set('name', 'Alex'); // Use the `set` method on the `joe` instance to change the value of the 'name' field to 'Alex'. This method allows us to update the properties of the document before saving it to the database. The `set` method takes two arguments: the name of the field to update and the new value for that field.
    await assertName(() => joe.save(), 'Alex'); // Call the `assertName` function, passing in an asynchronous function that saves the `joe` instance to the database and the expected name 'Alex'. This will execute the save operation and then verify that the user's name has been updated correctly in the database.
  });

  it('A model instance can update', async () => {
    await assertName(() => joe.updateOne({ name: 'Alex' }), 'Alex'); // Call the `assertName` function, passing in an asynchronous function that updates the `joe` instance in the database using the `updateOne` method and the expected name 'Alex'. This will execute the update operation and then verify that the user's name has been updated correctly in the database.
  });
});
```

### Class Based Updates ###
1. `update_test.js`

```javascript
const assert = require('assert');
const User = require('../src/user');

describe('Updating records', () => {
  let joe;

  beforeEach(async () => {
    joe = new User({ name: 'Joe' });
    await joe.save();
  });

  async function assertName(operation, name) {
    await operation(); // Execute the provided operation, which is expected to update the user's name in the database. This function takes an asynchronous function as an argument and awaits its completion before proceeding to the next steps.
    const users = await User.find({}); // Use the Mongoose `find` method to retrieve all users from the database. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. The result is an array of user documents that match the query.
    assert(users.length === 1); // Use the `assert` function to check if the length of the `users` array is equal to 1. This verifies that there is exactly one user in the database after the update operation. If the assertion fails, an error will be thrown, indicating that the test has failed.
    assert(users[0].name === name); // Use the `assert` function to check if the 'name' of the first user in the `users` array is equal to the provided `name`. This verifies that the user's name has been successfully updated in the database. If the assertion fails, an error will be thrown, indicating that the test has failed.
  }

  it('instance set and save', async () => {
    joe.set('name', 'Alex'); // Use the `set` method on the `joe` instance to change the value of the 'name' field to 'Alex'. This method allows us to update the properties of the document before saving it to the database. The `set` method takes two arguments: the name of the field to update and the new value for that field.
    await assertName(() => joe.save(), 'Alex'); // Call the `assertName` function, passing in an asynchronous function that saves the `joe` instance to the database and the expected name 'Alex'. This will execute the save operation and then verify that the user's name has been updated correctly in the database.
  });

  it('A model instance can update', async () => {
    await assertName(() => joe.updateOne({ name: 'Alex' }), 'Alex'); // Call the `assertName` function, passing in an asynchronous function that updates the `joe` instance in the database using the `updateOne` method and the expected name 'Alex'. This will execute the update operation and then verify that the user's name has been updated correctly in the database.
  });

  it('A model class can update', async () => {
    await assertName(
      () => User.updateMany({ name: 'Joe' }, { name: 'Alex' }),
      'Alex',
    ); // Use the Mongoose `updateMany` method on the User model to update all users with the name 'Joe' to have the name 'Alex'. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. The `updateMany` method takes two arguments: a filter object that specifies which documents to update and an update object that specifies the new values for the fields being updated.
  });

  it('A model class can update one record', async () => {
    await assertName(
      () => User.findOneAndUpdate({ name: 'Joe' }, { name: 'Alex' }),
      'Alex',
    ); // Use the Mongoose `findOneAndUpdate` method on the User model to find a single user with the name 'Joe' and update its name to 'Alex'. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. The `findOneAndUpdate` method takes two arguments: a filter object that specifies which document to update and an update object that specifies the new values for the fields being updated.
  });

  it('A model class can find a record with an Id and update', async () => {
    await assertName(
      () => User.findByIdAndUpdate(joe._id, { name: 'Alex' }),
      'Alex',
    ); // Use the Mongoose `findByIdAndUpdate` method on the User model to find a user by its unique `_id` and update its name to 'Alex'. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. The `findByIdAndUpdate` method takes two arguments: the `_id` of the document to update and an update object that specifies the new values for the fields being updated.
  });
});
```

## Section 5: Mongo Operators ##
### Update Operators ###
1. Performance inside MongoDB
2. `UserModel`

```
schema
	name
	postCount
```

	1. `postCount` - number of blog posts a user has as a count
		1. Adding new property does not fail existing tests
			1. It doesn't enforce any requirement
3. One option to update all the records:
	1. Fetch all users
	2. Iterate through them and update their post count
	3. Save all users
		1. Problem: We need to load all the data in server
			1. big performance issue
				1. Solution: Avoid loading data to server as much as possible
4. Another option:
	1. Send the following command: Find users and increment their postCount by 1
		1. Better performance
			1. **Mongo update operators** - very efficient (done by Mongo)
				1. `$inc`
				2. `$mul`
				3. `$rename`
				4. `$setOnInsert`
				5. `$set`
				6. `$unset`
				7. `$min` (update if less than this value)
				8. `$max`
				9. ... (check the documentation)
					1. Good for updating multiple records

### The Increment Update Operator ###
1. `$inc` - Increments the value of the field by the specified amount
	1. Useful to send off logic to Mongo
2. `update_test.js`

```javascript
  it('A user can have their postCount incremented by 1', async () => {
    await User.updateMany({ name: 'Joe' }, { $inc: { postCount: 1 } }); // Use the Mongoose `updateMany` method on the User model to increment the `postCount` field of all users with the name 'Joe' by 1. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. The `$inc` operator is a MongoDB update operator that increments the value of a field by a specified amount. In this case, we are incrementing the `postCount` field by 1.
    const user = await User.findOne({ name: 'Joe' }); // Use the Mongoose `findOne` method to retrieve a single user from the database with the name 'Joe'. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. The result is a user document that matches the query.
    assert(user.postCount === 1); // Use the `assert` function to check if the `postCount` of the retrieved user is equal to 1. This verifies that the `postCount` field has been successfully incremented by 1 in the database. If the assertion fails, an error will be thrown, indicating that the test has failed.
  });
```

### Validation of Records ###
1. Mongoose - interface to Mongo (has API)
	1. Mongo directly provides similar CRUD API
	2. Other features are offered by Mongoose that are not offered by Mongo
		1. Validation
			1. Check if properties are safe to save to a database
				1. Example: Name > 2 characters
					1. If the condition is not met, it is not saved in the database
2. `test/validation_test.js`

```javascript
const assert = require('assert');
const User = require('../src/user');

describe('Validating records', () => {
  it('requires a user name', async () => {});
});
```

### Requiring Attributes on a Model ###
1. `test/validation_test.js`

```javascript
const assert = require('assert');
const User = require('../src/user');

describe('Validating records', () => {
  it('requires a user name', async () => {
    const user = new User({ name: undefined }); // Create a new instance of the User model with the name set to undefined. This simulates a scenario where a user is created without a name, which is expected to fail validation.})
    const err = user.validateSync(); // Call the `validateSync` method on the `user` instance to perform synchronous validation. This method checks if the user document adheres to the schema's validation rules. Since the 'name' field is required, this validation is expected to fail, and an error object will be returned.
    const { message } = err.errors.name; // Destructure the `message` property from the `err.errors.name` object. This message contains the validation error message for the 'name' field, which is expected to indicate that the name is required.
    assert(message === 'Name is required'); // Use the `assert` function to check if the validation error message for the 'name' field matches the expected message 'Name is required'. If the assertion fails, an error will be thrown, indicating that the test has failed.
  });
});
```

### Validation With a Validator Function ###
1. `src/user.js`

```javascript
const UserSchema = new Schema({
  name: {
    type: String, // The name of the user. It is a string data type.
    validate: {
      validator: (name) => name.length > 2, // The `validator` function is a custom validation function that checks if the length of the 'name' field is greater than 2. It takes the value of the 'name' field as an argument and returns a boolean indicating whether the validation passed or failed.
      message: 'Name must be longer than 2 characters', // The `message` property is a custom error message that will be displayed if the validation fails. In this case, if the length of the 'name' field is not greater than 2, this message will be shown to indicate that the name must be longer than 2 characters.
    },
    required: [true, 'Name is required'], // The `required` property is a validation rule that ensures the 'name' field must be provided when creating or updating a user document. If the 'name' field is missing, Mongoose will throw a validation error with the message 'Name is required'.
  }, // The name of the user. It is a string data type.
  postCount: Number, // The number of posts made by the user. It is a number data type.
});
```

2. `test/validation_test.js`

```javascript
  it('requires a user name longer than 2 characters', async () => {
    const user = new User({ name: 'Al' }); // Create a new instance of the User model with the name set to 'Al'. This simulates a scenario where a user is created with a name that is shorter than the required length of 3 characters, which is expected to fail validation.
    const err = user.validateSync();
    const { message } = err.errors.name;
    assert(message === 'Name must be longer than 2 characters');
  });
```

### Handling Failed Inserts ###
1. `test/validation_test.js`

```javascript
  it('disallows invalid records from being saved', async () => {
    const user = new User({ name: 'Al' });
    try {
      await user.save();
      assert(false); // If we reach this point, it means the save was successful when it should have failed.
    } catch (err) {
      const { message } = err.errors.name; // Destructure the `message` property from the `err.errors.name` object. This message contains the validation error message for the 'name' field, which is expected to indicate that the name must be longer than 2 characters.
      assert(message === 'Name must be longer than 2 characters'); // Use the `assert` function to check if the validation error message for the 'name' field matches the expected message 'Name must be longer than 2 characters'. If the assertion fails, an error will be thrown, indicating that the test has failed.
    }
  });
```

## Section 6: Handling Relational Data ##
### Embedding Resources in Models ###
1. Nested resources
	1. Example: List of posts (blog post, etc.)
2. Another model for Post:
	1. Two models:
		1. User model
			1. name: 'Joe'
		2. Post model
			1. title: 'JS and Me'
	2. It is good for relational database
		1. For MongoDB, we need to handle such relationships
			1. Solution: User has a list of posts (not a separate resource)
				1. User
					1. name: 'Joe'
					2. posts:
						1. title: 'Python And Me'
						2. title: 'JS Land'
						3. ...
		2. `user schema`
			1. `name` 
			2. `postCount`
			2. `post`, `post`, `post`
		3. `post schema` (we don't make a model but only a schema)
			1. `title`
				1. Model is used only for distinct collections (we will not have a separate collection of posts)

### Nesting Posts on Users ###
1. Embedded resource is called a sub-document in MongoDB
2. `post.js`

```javascript
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

const PostSchema = new Schema({
  title: String,
});

module.exports = PostSchema;
```

3. `user.js`

```
const PostSchema = require('./post');

const UserSchema = new Schema({
  ...
  posts: [PostSchema], // The `posts` field is an array of subdocuments that follow the structure defined in the `PostSchema`. Each element in the `posts` array represents a post made by the user, and it will have the properties defined in the `PostSchema`, such as 'title'.
});
```

### Testing Subdocuments ###
1. `test/subdocument_test.js`

```javascript
const assert = require('assert');
const User = require('../src/user');

describe('Subdocuments', () => {
  it('can instantiate a subdocument', async () => {
    const joe = new User({
      name: 'Joe',
      posts: [{ title: 'PostTitle' }],
    });
    await joe.save();
    const user = await User.findOne({ name: 'Joe' });
    assert(user.posts[0].title === 'PostTitle');
  });
});
```

### Adding Subdocuments to Existing Records ###
1. Adding new subdocuments to existing list of documents
2. Operations:
	1. Construct Joe
	2. Save Joe
	3. Fetch Joe
	4. Add a post to Joe
	5. Save Joe
	6. Fetch Joe
	7. Make assertion
3. The only way to add a subdocument is to add it to the parent document and save the parent document
4. `subdocument_test.js`

```javascript
  it('can add subdocuments to an existing record', async () => {
    const joe = new User({
      name: 'Joe',
      posts: [],
    });
    await joe.save();
    const user = await User.findOne({ name: 'Joe' });
    user.posts.push({ title: 'New Post' });
    await user.save();
    const updatedUser = await User.findOne({ name: 'Joe' });
    assert(updatedUser.posts[0].title === 'New Post');
  });
```

### Removing Subdocuments ###
1. `test/subdocuments_test.js`

```javascript
  it('can remove an existing subdocument', async () => {
    const joe = new User({
      name: 'Joe',
      posts: [{ title: 'New Title' }],
    });
    await joe.save();
    const user = await User.findOne({ name: 'Joe' });
    user.posts.pull(user.posts[0]); // Use the `pull` method on the `posts` array of the `user` instance to remove the first subdocument from the array. The `pull` method takes a subdocument as an argument and removes it from the array if it exists. In this case, we are removing the first post in the `posts` array, which has the title 'New Title'.
    await user.save();
    const updatedUser = await User.findOne({ name: 'Joe' });
    assert(updatedUser.posts.length === 0);
  });
```

### Virtual Types ###
1. `postCount` must reflect the number of `posts`
	1. It is separate and not tied to `posts`
		1. Solution: Virtual Types in Mongoose
			1. It is any field in the model that does not get persisted onto MongoDB
2. `test/virtual_type_test.js`

```javascript
const assert = require('assert');
const User = require('../src/user');

describe('Virtual types', () => {
  it('postCount returns number of posts', async () => {
    const joe = new User({
      name: 'Joe',
      posts: [{ title: 'PostTitle' }],
    });
    await joe.save(); // Save the 'Joe' user to the database. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. This ensures that the user is saved before we attempt to retrieve it and check the virtual property.
    const user = await User.findOne({ name: 'Joe' });
    assert(user.postCount === 1); // Use the `assert` function to check if the `postCount` virtual property of the retrieved user is equal to 1. This verifies that the virtual property correctly calculates the number of posts for the user. If the assertion fails, an error will be thrown, indicating that the test has failed.
  });
});
```

### Defining a Virtual Type ###
1. Procedure:
	1. "joe.postCount"
		1. `get`ter and `set`ter of es6 is used
			1. We need to define a getter for `postCount`
				1. Mongoose and JS will run the function `get` when we access `joe.postCount`
	2. Quick, run this function
	3. Return the value
	4. Your result is 1
2. `test/update_test.js`

```javascript
  xit('A user can have their postCount incremented by 1', async () => {
    await User.updateMany({ name: 'Joe' }, { $inc: { postCount: 1 } }); // Use the Mongoose `updateMany` method on the User model to increment the `postCount` field of all users with the name 'Joe' by 1. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. The `$inc` operator is a MongoDB update operator that increments the value of a field by a specified amount. In this case, we are incrementing the `postCount` field by 1.
    const user = await User.findOne({ name: 'Joe' }); // Use the Mongoose `findOne` method to retrieve a single user from the database with the name 'Joe'. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. The result is a user document that matches the query.
    assert(user.postCount === 1); // Use the `assert` function to check if the `postCount` of the retrieved user is equal to 1. This verifies that the `postCount` field has been successfully incremented by 1 in the database. If the assertion fails, an error will be thrown, indicating that the test has failed.
  });
```

3. `test/virtual_type_test.js`

```javascript
const assert = require('assert');
const User = require('../src/user');

describe('Virtual types', () => {
  it('postCount returns number of posts', async () => {
    const joe = new User({
      name: 'Joe',
      posts: [{ title: 'PostTitle' }],
    });
    await joe.save(); // Save the 'Joe' user to the database. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. This ensures that the user is saved before we attempt to retrieve it and check the virtual property.
    const user = await User.findOne({ name: 'Joe' });
    assert(user.postCount === 1); // Use the `assert` function to check if the `postCount` virtual property of the retrieved user is equal to 1. This verifies that the virtual property correctly calculates the number of posts for the user. If the assertion fails, an error will be thrown, indicating that the test has failed.
  });
});
```

4. `test/user.js`

```javascript
const mongoose = require('mongoose'); // Import the Mongoose library, which is an Object Data Modeling (ODM) library for MongoDB and Node.js. It provides a schema-based solution to model application data.
const Schema = mongoose.Schema; // `Schema` is a constructor function that allows us to define the structure of documents in a MongoDB collection. It is used to create a new schema for the 'user' collection.
const PostSchema = require('./post');

const UserSchema = new Schema({
  name: {
    type: String, // The name of the user. It is a string data type.
    validate: {
      validator: (name) => name.length > 2, // The `validator` function is a custom validation function that checks if the length of the 'name' field is greater than 2. It takes the value of the 'name' field as an argument and returns a boolean indicating whether the validation passed or failed.
      message: 'Name must be longer than 2 characters', // The `message` property is a custom error message that will be displayed if the validation fails. In this case, if the length of the 'name' field is not greater than 2, this message will be shown to indicate that the name must be longer than 2 characters.
    },
    required: [true, 'Name is required'], // The `required` property is a validation rule that ensures the 'name' field must be provided when creating or updating a user document. If the 'name' field is missing, Mongoose will throw a validation error with the message 'Name is required'.
  }, // The name of the user. It is a string data type.
  posts: [PostSchema], // The `posts` field is an array of subdocuments that follow the structure defined in the `PostSchema`. Each element in the `posts` array represents a post made by the user, and it will have the properties defined in the `PostSchema`, such as 'title'.
});

UserSchema.virtual('postCount').get(function () {
  return this.posts.length; // The `postCount` virtual property calculates the number of posts associated with the user. It uses the `length` property of the `posts` array to determine how many posts the user has. This virtual property does not get persisted to the database; it is computed on-the-fly whenever it is accessed.
});

const User = mongoose.model('user', UserSchema); // 'user' is a collection. It is automatically created in the database if it doesn't exist. `UserSchema` is the schema for the collection. It defines the structure of the documents in the collection. `User` is a class that we can use to create new users and interact with the 'user' collection in the database.

module.exports = User; // Export the User model so that it can be used in other files.
```

### ES6 Getters ###
1. `node`

```javascript
const User = require('./src/user');

console.log(joe.postCount); // `get` gets called
```

### Fixing Update Tests ###
1. `src/user.js`

```javascript
const UserSchema = new Schema({
  name: {
    type: String, // The name of the user. It is a string data type.
    validate: {
      validator: (name) => name.length > 2, // The `validator` function is a custom validation function that checks if the length of the 'name' field is greater than 2. It takes the value of the 'name' field as an argument and returns a boolean indicating whether the validation passed or failed.
      message: 'Name must be longer than 2 characters', // The `message` property is a custom error message that will be displayed if the validation fails. In this case, if the length of the 'name' field is not greater than 2, this message will be shown to indicate that the name must be longer than 2 characters.
    },
    required: [true, 'Name is required'], // The `required` property is a validation rule that ensures the 'name' field must be provided when creating or updating a user document. If the 'name' field is missing, Mongoose will throw a validation error with the message 'Name is required'.
  }, // The name of the user. It is a string data type.
  posts: [PostSchema], // The `posts` field is an array of subdocuments that follow the structure defined in the `PostSchema`. Each element in the `posts` array represents a post made by the user, and it will have the properties defined in the `PostSchema`, such as 'title'.
  likes: Number, // The `likes` field is a number that represents the total number of likes the user has received. It is a numeric data type and can be used to store the count of likes associated with the user.
});
```

2. `test/update_test.js`

```javascript
const assert = require('assert');
const User = require('../src/user');

describe('Updating records', () => {
  let joe;

  beforeEach(async () => {
    joe = new User({ name: 'Joe', likes: 0 });
    await joe.save();
  });

  async function assertName(operation, name) {
    await operation(); // Execute the provided operation, which is expected to update the user's name in the database. This function takes an asynchronous function as an argument and awaits its completion before proceeding to the next steps.
    const users = await User.find({}); // Use the Mongoose `find` method to retrieve all users from the database. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. The result is an array of user documents that match the query.
    assert(users.length === 1); // Use the `assert` function to check if the length of the `users` array is equal to 1. This verifies that there is exactly one user in the database after the update operation. If the assertion fails, an error will be thrown, indicating that the test has failed.
    assert(users[0].name === name); // Use the `assert` function to check if the 'name' of the first user in the `users` array is equal to the provided `name`. This verifies that the user's name has been successfully updated in the database. If the assertion fails, an error will be thrown, indicating that the test has failed.
  }

  it('instance set and save', async () => {
    joe.set('name', 'Alex'); // Use the `set` method on the `joe` instance to change the value of the 'name' field to 'Alex'. This method allows us to update the properties of the document before saving it to the database. The `set` method takes two arguments: the name of the field to update and the new value for that field.
    await assertName(() => joe.save(), 'Alex'); // Call the `assertName` function, passing in an asynchronous function that saves the `joe` instance to the database and the expected name 'Alex'. This will execute the save operation and then verify that the user's name has been updated correctly in the database.
  });

  it('A model instance can update', async () => {
    await assertName(() => joe.updateOne({ name: 'Alex' }), 'Alex'); // Call the `assertName` function, passing in an asynchronous function that updates the `joe` instance in the database using the `updateOne` method and the expected name 'Alex'. This will execute the update operation and then verify that the user's name has been updated correctly in the database.
  });

  it('A model class can update', async () => {
    await assertName(
      () => User.updateMany({ name: 'Joe' }, { name: 'Alex' }),
      'Alex',
    ); // Use the Mongoose `updateMany` method on the User model to update all users with the name 'Joe' to have the name 'Alex'. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. The `updateMany` method takes two arguments: a filter object that specifies which documents to update and an update object that specifies the new values for the fields being updated.
  });

  it('A model class can update one record', async () => {
    await assertName(
      () => User.findOneAndUpdate({ name: 'Joe' }, { name: 'Alex' }),
      'Alex',
    ); // Use the Mongoose `findOneAndUpdate` method on the User model to find a single user with the name 'Joe' and update its name to 'Alex'. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. The `findOneAndUpdate` method takes two arguments: a filter object that specifies which document to update and an update object that specifies the new values for the fields being updated.
  });

  it('A model class can find a record with an Id and update', async () => {
    await assertName(
      () => User.findByIdAndUpdate(joe._id, { name: 'Alex' }),
      'Alex',
    ); // Use the Mongoose `findByIdAndUpdate` method on the User model to find a user by its unique `_id` and update its name to 'Alex'. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. The `findByIdAndUpdate` method takes two arguments: the `_id` of the document to update and an update object that specifies the new values for the fields being updated.
  });

  it('A user can have their postCount incremented by 1', async () => {
    await User.updateMany({ name: 'Joe' }, { $inc: { likes: 10 } }); // Use the Mongoose `updateMany` method on the User model to increment the `likes` field of all users with the name 'Joe' by 10. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. The `$inc` operator is a MongoDB update operator that increments the value of a field by a specified amount. In this case, we are incrementing the `likes` field by 10.
    const user = await User.findOne({ name: 'Joe' }); // Use the Mongoose `findOne` method to retrieve a single user from the database with the name 'Joe'. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. The result is a user document that matches the query.
    assert(user.likes === 10); // Use the `assert` function to check if the `likes` field of the retrieved user is equal to 10. This verifies that the `likes` field has been successfully incremented by 10 in the database. If the assertion fails, an error will be thrown, indicating that the test has failed.
  });
});
```

## Section 7: Thinking About Schema Design ##
### Challenges of Nested Resources ###
1. How to design large MongoDB DBs?
	1. With more relationships
2. Shortcomings:
	1. Example: List of blog-posts
		1. Post title, Author
			1. It is not easy to display list of blogposts of multiple users
			
			```javascript
			User.find({})
			  .then((users) => {
			    users.flatMap(user => user.posts);
			});
			```
			
				1. Problems:
					1. We want to show a finite list of posts and they have to be an even number
						1. If we limit the number of users, they may not have any posts
				2. Use-case:
					1. Display all the posts of a particular user
						1. Easy with nested posts

### Embedded Documents vs Seprate Collections ###
1. If each post has comments
	1. How to record who made the comments?
		1. They belong to different users
2. Approach 1:
	1. `user.posts[0].title`
	2. `user.name`
	3. `user.posts[0].content`
	4. Comments?
		1. How to get comments written by another person?
	5. Solution:
		1. User collection
			1. Has an array of post ids
		2. Post collection
			1. Has an array of comment ids
			2. We can get top 10 posts
		3. Comment collection
			1. Has a user id
	6. Problem:
		1. Get all users and get post for each user (N + 1 problem)
			1. We don't have single operation joins in MongoDB
				1. We need to send multiple queries and do the joins in the application

### BlogPosts vs Posts ###
1. `src/blogPost.js`

```javascript
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

const BlogPostSchema = new Schema({
  title: String,
  content: String,
});
```

2. `src/comment.js`

```javascript

```

### Constructing Associations with Refs ###
1. `src/blogPost.js`

```javascript
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

const BlogPostSchema = new Schema({
  title: String,
  content: String,
  comments: [{ type: Schema.Types.ObjectId, ref: 'comment' }], // The `comments` field is an array of ObjectIds that reference documents in the 'comment' collection. Each element in the `comments` array represents a comment associated with the blog post. The `ref` property specifies the name of the model that the ObjectId refers to, allowing Mongoose to establish a relationship between the BlogPost and Comment models. This enables us to populate the comments when querying for blog posts, making it easier to retrieve related data from the database.
});

const BlogPost = mongoose.model('blogPost', BlogPostSchema); // 'BlogPost' is a collection. It is automatically created in the database if it doesn't exist. `BlogPostSchema` is the schema for the collection. It defines the structure of the documents in the collection. `BlogPost` is a class that we can use to create new blog posts and interact with the 'BlogPost' collection in the database.

module.exports = BlogPost; // Export the BlogPost model so that it can be used in other files.
```

2. `src/comment.js`

```javascript
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

const CommentSchema = new Schema({
  content: String,
  user: { type: Schema.Types.ObjectId, ref: 'user' }, // The `user` field is an ObjectId that references a document in the 'user' collection. It establishes a relationship between the Comment and User models, allowing us to associate a comment with a specific user. The `ref` property specifies the name of the model that the ObjectId refers to, enabling Mongoose to populate the user data when querying for comments.
});

const Comment = mongoose.model('comment', CommentSchema); // 'comment' is a collection. It is automatically created in the database if it doesn't exist. `CommentSchema` is the schema for the collection. It defines the structure of the documents in the collection. `Comment` is a class that we can use to create new comments and interact with the 'comment' collection in the database.

module.exports = Comment; // Export the Comment model so that it can be used in other files.
```

### Test Setup for Associations ###
1. `test_helper.js`

```javascript
beforeEach(async function () {
  this.timeout(10000); // Increase the timeout for the beforeEach hook to 10 seconds. This is useful if the database connection takes longer than the default timeout period.

  await mongoose.connection.collections.users.drop(); // Drop the 'users' collection before each test to ensure a clean state. This prevents tests from interfering with each other by ensuring that the database is empty before each test runs.
  await mongoose.connection.collections.comments.drop(); // Drop the 'comments' collection before each test to ensure a clean state. This prevents tests from interfering with each other by ensuring that the database is empty before each test runs.
  await mongoose.connection.collections.blogposts.drop(); // Drop the 'blogposts' collection before each test to ensure a clean state. This prevents tests from interfering with each other by ensuring that the database is empty before each test runs.
});
```

2. `association_test.js`

```javascript
const mongoose = require('mongoose');
const User = require('../src/user');
const Comment = require('../src/comment');
const BlogPost = require('../src/BlogPost');

describe('Associations', () => {});
```

### Wiring Up Has Many and Has one Relations ###
1. We cannot drop multiple collections in MongoDB at the same time anyway
	1. Sequentially dropping collections is okay
2. `test/association_test.js`

```javascript
const mongoose = require('mongoose');
const User = require('../src/user');
const Comment = require('../src/comment');
const BlogPost = require('../src/blogPost');

describe('Associations', () => {
  let joe, blogPost, comment;

  beforeEach(async () => {
    joe = new User({ name: 'Joe' });
    blogPost = new BlogPost({
      title: 'JS is Great',
      content: 'Yes it really is',
    });
    comment = new Comment({ content: 'Congrats on great post' });

    // Establish associations
    joe.blogPosts.push(blogPost); // Add the `blogPost` instance to the `blogPosts` array of the `joe` instance. This establishes a relationship between the user and the blog post, indicating that Joe is the author of the blog post. Mongoose will handle the ObjectId reference automatically when saving the documents to the database.
    blogPost.comments.push(comment); // Add the `comment` instance to the `comments` array of the `blogPost` instance. This establishes a relationship between the blog post and the comment, indicating that the comment is associated with the blog post. Mongoose will handle the ObjectId reference automatically when saving the documents to the database.
    comment.user = joe; // Set the `user` field of the `comment` instance to reference the `joe` instance. This establishes a relationship between the comment and the user, indicating that Joe is the author of the comment. Mongoose will handle the ObjectId reference automatically when saving the documents to the database.
  });
});
```

### Promise.All for Parallel Operations ###
1. `association_test.js`

```javascript
const assert = require('assert');
const mongoose = require('mongoose');
const User = require('../src/user');
const Comment = require('../src/comment');
const BlogPost = require('../src/blogPost');

describe('Associations', () => {
  let joe, blogPost, comment;

  beforeEach(async () => {
    joe = new User({ name: 'Joe' });
    blogPost = new BlogPost({
      title: 'JS is Great',
      content: 'Yes it really is',
    });
    comment = new Comment({ content: 'Congrats on great post' });

    // Establish associations
    joe.blogPosts.push(blogPost); // Add the `blogPost` instance to the `blogPosts` array of the `joe` instance. This establishes a relationship between the user and the blog post, indicating that Joe is the author of the blog post. Mongoose will handle the ObjectId reference automatically when saving the documents to the database.
    blogPost.comments.push(comment); // Add the `comment` instance to the `comments` array of the `blogPost` instance. This establishes a relationship between the blog post and the comment, indicating that the comment is associated with the blog post. Mongoose will handle the ObjectId reference automatically when saving the documents to the database.
    comment.user = joe; // Set the `user` field of the `comment` instance to reference the `joe` instance. This establishes a relationship between the comment and the user, indicating that Joe is the author of the comment. Mongoose will handle the ObjectId reference automatically when saving the documents to the database.

    await Promise.all([joe.save(), blogPost.save(), comment.save()]); // Use `Promise.all` to save all three instances (`joe`, `blogPost`, and `comment`) to the database concurrently. This ensures that all documents are saved before proceeding with the tests, and it improves performance by allowing the saves to happen in parallel rather than sequentially.
  });

  it.only('saves a relation between a user and a blog post', async () => {
    const user = await User.findOne({ name: 'Joe' }).populate('blogPosts'); // Use the Mongoose `findOne` method to find a user with the name 'Joe' and populate the `blogPosts` field. The `populate` method replaces the ObjectId references in the `blogPosts` array with the actual blog post documents, allowing us to access the full blog post data associated with the user.
    assert(user.blogPosts[0].title === 'JS is Great'); // Use the `assert` function to check if the title of the first blog post associated with the user is 'JS is Great'. If the assertion fails, an error will be thrown, indicating that the test has failed.
  });
});
```

### Populating Queries ###
1. Query:
	1. `User.findOne({ name: 'Joe' }).<modifier>.then()`
		1. `User` - In my User collection
		2. `findOne` - Find the first record with this criteria
			1. It only returns a query but not send it to MongoDB
		3. `then`
			1. This sends query to the database
				1. Older syntax: `exec`
		4. `<modifier>`
			1. To enhance the query in some way
				1. More specific
				2. More broad
				3. Custome query
				4. Load data
			2. `populate`
				1. Modifier used to load associated sub-documents
					1. `User.findOne({ name: 'Joe' }).populate('blogPosts').then()`
			3. Mongoose does not let us recursively load all the nested documents
				1. We can explicitly load them
2. `assocition_test.js`

```javascript
const assert = require('assert');
const mongoose = require('mongoose');
const User = require('../src/user');
const Comment = require('../src/comment');
const BlogPost = require('../src/blogPost');

describe('Associations', () => {
  let joe, blogPost, comment;

  beforeEach(async () => {
    joe = new User({ name: 'Joe' });
    blogPost = new BlogPost({
      title: 'JS is Great',
      content: 'Yes it really is',
    });
    comment = new Comment({ content: 'Congrats on great post' });

    // Establish associations
    joe.blogPosts.push(blogPost); // Add the `blogPost` instance to the `blogPosts` array of the `joe` instance. This establishes a relationship between the user and the blog post, indicating that Joe is the author of the blog post. Mongoose will handle the ObjectId reference automatically when saving the documents to the database.
    blogPost.comments.push(comment); // Add the `comment` instance to the `comments` array of the `blogPost` instance. This establishes a relationship between the blog post and the comment, indicating that the comment is associated with the blog post. Mongoose will handle the ObjectId reference automatically when saving the documents to the database.
    comment.user = joe; // Set the `user` field of the `comment` instance to reference the `joe` instance. This establishes a relationship between the comment and the user, indicating that Joe is the author of the comment. Mongoose will handle the ObjectId reference automatically when saving the documents to the database.

    await Promise.all([joe.save(), blogPost.save(), comment.save()]); // Use `Promise.all` to save all three instances (`joe`, `blogPost`, and `comment`) to the database concurrently. This ensures that all documents are saved before proceeding with the tests, and it improves performance by allowing the saves to happen in parallel rather than sequentially.
  });

  it('saves a relation between a user and a blog post', async () => {
    const user = await User.findOne({ name: 'Joe' }).populate('blogPosts'); // Use the Mongoose `findOne` method to find a user with the name 'Joe' and populate the `blogPosts` field. The `populate` method replaces the ObjectId references in the `blogPosts` array with the actual blog post documents, allowing us to access the full blog post data associated with the user.
    assert(user.blogPosts[0].title === 'JS is Great'); // Use the `assert` function to check if the title of the first blog post associated with the user is 'JS is Great'. If the assertion fails, an error will be thrown, indicating that the test has failed.
  });
});
```

### Loading Deeply Nested Associations ###
1. `association_test.js`

```javascript
  it('saves a full relation graph', async () => {
    const user = await User.findOne({ name: 'Joe' }).populate({
      path: 'blogPosts', // Specify the path to populate, which is the `blogPosts` field of the user. This tells Mongoose to replace the ObjectId references in the `blogPosts` array with the actual blog post documents.
      populate: {
        path: 'comments', // Specify the path to populate within the `blogPosts` documents, which is the `comments` field. This tells Mongoose to replace the ObjectId references in the `comments` array of each blog post with the actual comment documents.
        model: 'comment', // Specify the model to use for populating the `comments` field, which is the 'comment' model. This ensures that Mongoose knows which collection to query for the comment documents.
        populate: {
          path: 'user', // Specify the path to populate within the `comments` documents, which is the `user` field. This tells Mongoose to replace the ObjectId reference in the `user` field of each comment with the actual user document.
          model: 'user', // Specify the model to use for populating the `user` field, which is the 'user' model. This ensures that Mongoose knows which collection to query for the user documents.
        },
      },
    });
    assert(user.name === 'Joe'); // Use the `assert` function to check if the name of the user is 'Joe'. If the assertion fails, an error will be thrown, indicating that the test has failed.
    assert(user.blogPosts[0].title === 'JS is Great'); // Use the `assert` function to check if the title of the first blog post associated with the user is 'JS is Great'. If the assertion fails, an error will be thrown, indicating that the test has failed.
    assert(user.blogPosts[0].comments[0].content === 'Congrats on great post'); // Use the `assert` function to check if the content of the first comment associated with the first blog post is 'Congrats on great post'. If the assertion fails, an error will be thrown, indicating that the test has failed.
    assert(user.blogPosts[0].comments[0].user.name === 'Joe'); // Use the `assert` function to check if the name of the user associated with the first comment of the first blog post is 'Joe'. If the assertion fails, an error will be thrown, indicating that the test has failed.
  });
```

## Section 8: Mongoose Middleware ##
### Cleaning Up with Middleware ###
1. BlogPost and Comment need User to exist - usually
	1. If we delete `User`, then `BlogPost`s and `Comment`s should be deleted
		1. It is not efficient to iterate through sub-documents and delete them
			1. Solution: Middleware
				1. Pre and post hooks
					1. Functions that execute before and after a distinct event
						1. Example:
							1. `save` event
							
							```
							        middleware#1
									middleware#2 (pre)
							save ---------------
							        middleware#3 (post)
									middleware#4
							```
							
	2. Event: `remove`

### Dealing with Cycling Requires ###
1. Events:
	1. `init`
	2. `validate`
	3. `save`
	4. `remove`
2. Avoiding cyclic dependencies
	1. `BlogPost` has `require('User');
	2. `User` has `require('BlogPost');
3. `user.js`

```javascript
UserSchema.pre('deleteOne', function () {
  const user = this; // The `user` variable refers to the current user document that is being deleted. The `this` keyword in this context refers to the document instance on which the `deleteOne` operation is being performed.
  const BlogPost = mongoose.model('blogPost'); // Retrieve the 'blogPost' model from Mongoose. This allows us to interact with the 'blogPost' collection in the database and perform operations such as finding and deleting blog posts associated with the user being deleted.
});
```

### Pre-Remove Middleware ###
1. `user.js`

```javascript
UserSchema.pre('deleteOne', { document: true }, async function () {
  const user = this; // The `user` variable refers to the current user document that is being deleted. The `this` keyword in this context refers to the document instance on which the `deleteOne` operation is being performed.
  const BlogPost = mongoose.model('blogPost'); // Retrieve the 'blogPost' model from Mongoose. This allows us to interact with the 'blogPost' collection in the database and perform operations such as finding and deleting blog posts associated with the user being deleted.
  await BlogPost.deleteMany({ _id: { $in: user.blogPosts } });
});
```

### Required Pre Remove Hook Updates ###
1. Later version update:

```javascript
UserSchema.pre('deleteOne', { document: true }, function (next) {
  const BlogPost = mongoose.model('blogPost');
  // this === joe
  BlogPost.deleteMany({ _id: { $in: this.blogPosts } }).then(() => next());
});
```

2. `middleware_test.js`

```javascript
it('users clean up dangling blogposts on remove', (done) => {
  joe
    .deleteOne()
	.then(() => BlogPost.countDocuments())
	.then((count) => {
	  assert(count === 0);
	  done();
	});
});
```

### Testing Pre-Remove Middleware ###
1. `test/middleware_test.js`

```javascript
const mongoose = require('mongoose');
const assert = require('assert');
const User = require('../src/user');
const BlogPost = require('../src/blogPost');

describe('Middleware', () => {
  let joe, blogPost;
  beforeEach(async () => {
    joe = new User({ name: 'Joe' });
    blogPost = new BlogPost({
      title: 'JS is Great',
      content: 'Yes it really is',
    });

    // Establish associations
    joe.blogPosts.push(blogPost); // Add the `blogPost` instance to the `blogPosts` array of the `joe` instance. This establishes a relationship between the user and the blog post, indicating that Joe is the author of the blog post. Mongoose will handle the ObjectId reference automatically when saving the documents to the database.

    await Promise.all([joe.save(), blogPost.save()]); // Use `Promise.all` to save both the `joe` and `blogPost` instances to the database concurrently. This ensures that both documents are saved before proceeding with the tests, and it improves performance by allowing the saves to happen in parallel rather than sequentially.
  });

  it('users clean up dangling blogposts on delete', async () => {
    await joe.deleteOne(); // Use the `deleteOne` method on the `joe` instance to delete it from the database. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. The `deleteOne` method is an instance method that removes the specific document from the collection.
    const blogPostCount = await BlogPost.countDocuments({}); // Use the Mongoose `countDocuments` method to count the number of documents in the 'blogPost' collection. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. The result is the total number of blog post documents currently in the collection.
    assert(blogPostCount === 0); // Use the `assert` function to check if the `blogPostCount` is equal to 0. This verifies that all blog posts associated with the deleted user have been successfully removed from the database. If the assertion fails, an error will be thrown, indicating that the test has failed.
  });
});
```

## Section 9: Handling Big Collections with Pagination ##
### Skip and Limit ###
1. User collection
	1. User
	2. User
	3. User
	4. ...
		1. Too many records for fetching
			1. Solution: Pagination
				1. We want to show a few records at once
2. Query modifiers
	1. `skip`
		1. 0, limit, 2 * limit, ...
	2. `limit`
		1. Limits the number of results

### Writing Skip and Limit Queries ###
1. `test/reading_test.js`

```javascript
const assert = require('assert'); // Import the assert module from Node.js. This module provides a set of assertion functions for verifying invariants in your code. In this case, it is used to check if the user has been saved successfully to the database.
const User = require('../src/user'); // Import the User model from the user.js file. This model is used to interact with the 'user' collection in the MongoDB database.

describe('Reading users out of the database', () => {
  let joe; // Declare a variable 'joe' to hold the user instance. This variable will be used in the tests to reference the user that is created and saved to the database.

  beforeEach(async () => {
    alex = new User({ name: 'Alex' }); // Create a new instance of the User model with the name 'Alex'. This instance represents a document that will be saved to the 'user' collection in the database.
    joe = new User({ name: 'Joe' }); // Create a new instance of the User model with the name 'Joe'. This instance represents a document that will be saved to the 'user' collection in the database.
    maria = new User({ name: 'Maria' }); // Create a new instance of the User model with the name 'Maria'. This instance represents a document that will be saved to the 'user' collection in the database.
    zack = new User({ name: 'Zack' }); // Create a new instance of the User model with the name 'Zack'. This instance represents a document that will be saved to the 'user' collection in the database.

    await Promise.all([alex.save(), joe.save(), maria.save(), zack.save()]); // Use `Promise.all` to save all four user instances (`alex`, `joe`, `maria`, and `zack`) to the database concurrently. This ensures that all users are saved before proceeding with the tests, and it improves performance by allowing the saves to happen in parallel rather than sequentially.
  });

  it('finds all users with a name of Joe', async () => {
    const users = await User.find({ name: 'Joe' }); // Use the Mongoose 'find' method to retrieve all users from the database with the name 'Joe'. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. The result is an array of user documents that match the query.
    assert(users[0]._id.toString() === joe._id.toString()); // Use the 'assert' function to check if the '_id' of the first user in the 'users' array matches the '_id' of the 'joe' instance. This verifies that the user we created and saved earlier can be successfully retrieved from the database. If the assertion fails, an error will be thrown, indicating that the test has failed.
  });

  it('find a user with a particular id', async () => {
    const user = await User.findOne({ _id: joe._id }); // Use the Mongoose 'findOne' method to retrieve a single user from the database with the specific '_id' of the 'joe' instance. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. The result is a single user document that matches the query.
    assert(user.name === 'Joe'); // Use the 'assert' function to check if the 'name' of the retrieved user matches 'Joe'. This verifies that the user we created and saved earlier can be successfully retrieved from the database using its unique '_id'. If the assertion fails, an error will be thrown, indicating that the test has failed.
  });

  it('can skip and limit the result set', async () => {
    const users = await User.find({}).skip(1).limit(2); // Use the Mongoose 'find' method to retrieve all users from the database, but skip the first user and limit the result set to 2 users. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. The result is an array of user documents that match the query, with the specified skip and limit applied.
  });
});
```

### Sorting Collections ###
1. `test/reading_test.js`

```javascript
const assert = require('assert'); // Import the assert module from Node.js. This module provides a set of assertion functions for verifying invariants in your code. In this case, it is used to check if the user has been saved successfully to the database.
const User = require('../src/user'); // Import the User model from the user.js file. This model is used to interact with the 'user' collection in the MongoDB database.

describe('Reading users out of the database', () => {
  let joe; // Declare a variable 'joe' to hold the user instance. This variable will be used in the tests to reference the user that is created and saved to the database.

  beforeEach(async () => {
    alex = new User({ name: 'Alex' }); // Create a new instance of the User model with the name 'Alex'. This instance represents a document that will be saved to the 'user' collection in the database.
    joe = new User({ name: 'Joe' }); // Create a new instance of the User model with the name 'Joe'. This instance represents a document that will be saved to the 'user' collection in the database.
    maria = new User({ name: 'Maria' }); // Create a new instance of the User model with the name 'Maria'. This instance represents a document that will be saved to the 'user' collection in the database.
    zack = new User({ name: 'Zack' }); // Create a new instance of the User model with the name 'Zack'. This instance represents a document that will be saved to the 'user' collection in the database.

    await Promise.all([alex.save(), joe.save(), maria.save(), zack.save()]); // Use `Promise.all` to save all four user instances (`alex`, `joe`, `maria`, and `zack`) to the database concurrently. This ensures that all users are saved before proceeding with the tests, and it improves performance by allowing the saves to happen in parallel rather than sequentially.
  });

  it('finds all users with a name of Joe', async () => {
    const users = await User.find({ name: 'Joe' }); // Use the Mongoose 'find' method to retrieve all users from the database with the name 'Joe'. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. The result is an array of user documents that match the query.
    assert(users[0]._id.toString() === joe._id.toString()); // Use the 'assert' function to check if the '_id' of the first user in the 'users' array matches the '_id' of the 'joe' instance. This verifies that the user we created and saved earlier can be successfully retrieved from the database. If the assertion fails, an error will be thrown, indicating that the test has failed.
  });

  it('find a user with a particular id', async () => {
    const user = await User.findOne({ _id: joe._id }); // Use the Mongoose 'findOne' method to retrieve a single user from the database with the specific '_id' of the 'joe' instance. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. The result is a single user document that matches the query.
    assert(user.name === 'Joe'); // Use the 'assert' function to check if the 'name' of the retrieved user matches 'Joe'. This verifies that the user we created and saved earlier can be successfully retrieved from the database using its unique '_id'. If the assertion fails, an error will be thrown, indicating that the test has failed.
  });

  it('can skip and limit the result set', async () => {
    const users = await User.find({}).sort({ name: 1 }).skip(1).limit(2); // Use the Mongoose 'find' method to retrieve all users from the database, sort them by name in ascending order, skip the first user, and limit the result set to 2 users. This operation is asynchronous, so we use 'await' to wait for it to complete before proceeding. The result is an array of user documents that match the query, sorted and limited according to the specified criteria. `1` - Sort in ascending order, `-1` - Sort in descending order.
    assert(users.length === 2);
    assert(users[0].name === 'Joe');
    assert(users[1].name === 'Maria');
  });
});
```

## Section 10: Putting Your Skills to the Test ##
### Required Starter Files - DO NOT SKIP ###
1. Download the zip file
2. `cd UpStarMusic`
3. `npm install --legacy-peer-deps`

### Project Overview ###
1. `database/models`, `database/queries`
	1. `queries/FindArtist.js`
	
	```
	module.exports = (_id) => {
	};
	```

### First Step - Artist and Album Models ###
1. We can refresh local connection
	1. `upstar_music`
		1. `artists`
			1. `name`
			2. `age`
			3. `image`
			4. ...
		2. `albums`
2. Fix:
	1. [http://github.com/davidchin/react-input-range](http://github.com/davidchin/react-input-range)
		1. `npm i react-input-range --legacy-peer-deps`
	2. Remove failing `link` in `index.html`
	3. Do the following to start the application in windows:
	
	```bash
	npx webpack-dev-server
	npx electron .
	```
	
		1. Option 2:
			1. Install `concurrently`
			
			```bash
			npm install --save-dev concurrently wait-on --legacy-peer-deps
			```
			
			2. `package.json`
			
			```json
			"scripts": {
			  "dev": "concurrently \"webpack-dev-server\" \"wait-on http://localhost:4172 && electron .\""
			},
			```
			
			3. Run the application
			
			```bash
			npm run dev
			```
			
3. NOTE:

```
`--legacy-peer-deps` is an npm installation flag that tells npm to ignore peer dependency conflicts and use the dependency resolution behavior from npm 6 and earlier.

It is commonly used when installing older projects (like the one you're currently working on) that were created before npm enforced peer dependencies strictly.
```

4. Models
	1. Artist
		1. name
		2. age
		3. yearsActive
		4. image
		5. genre
		6. website
		7. netWorth
		8. labelName
		9. retired
		10. [Albums]
	2. Album
		1. title
		2. date
		3. copiesSold
		4. numberTracks
		5. image
		6. revenue

### The Album Schema ###
1. `database/models/album.js`

```javascript
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

const AlbumSchema = new Schema({
  title: String,
  date: Date,
  copiesSold: Number,
  numberTracks: Number,
  image: String,
  revenue: Number
});

module.exports = AlbumSchema;
```

### The Artist Model ###
1. `database/models/artist.js`

```javascript
const mongoose = require('mongoose');
const AlbumSchema = require('./album');
const Schema = mongoose.Schema;

const ArtistSchema = new Schema({
  name: String,
  age: Number,
  yearsActive: Number,
  image: String,
  genre: String,
  website: String,
  netWorth: Number,
  labelName: String,
  retired: Boolean,
  albums: [AlbumSchema]
});

const Artist = mongoose.model('artist', ArtistSchema);

module.exports = Artist;
```

### Finding Particular Records ###
1. `database/queries/FindArtist.js`
2. Return `Promise`

### FindOne vs FindById ###
1. `database/queries/FindArtist.js`: `findOne`

```javascript
const Artist = require('../models/artist');

/**
 * Finds a single artist in the artist collection.
 * @param {string} _id - The ID of the record to find.
 * @return {promise} A promise that resolves with the Artist that matches the id
 */
module.exports = (_id) => {
  return Artist.findOne({ _id: _id });
};
```

2. Mongoose Docs: API Docs

```javascript
  return Artist.findById(_id);
```

### The CreateArtist Operation ###
1. `database/queries/CreateArtist.js`

### Solution to Constructing Artists ###
1. `database/queries/CreateArtist.js`

```javascript
const Artist = require('../models/artist');

/**
 * Finds a single artist in the artist collection.
 * @param {object} artistProps - Object containing a name, age, yearsActive, and genre
 * @return {promise} A promise that resolves with the Artist that was created
 */
module.exports = (artistProps) => {
  return Artist.create(artistProps);
};
```

```javascript
const Artist = require('../models/artist');

/**
 * Finds a single artist in the artist collection.
 * @param {object} artistProps - Object containing a name, age, yearsActive, and genre
 * @return {promise} A promise that resolves with the Artist that was created
 */
module.exports = (artistProps) => {
  const artist = new Artist(artistProps);
  return artist.save();
};
```

### Deleting Singular Records ###
1. `database/queries/DeleteArtist.js`

```javascript
const Artist = require('../models/artist');

/**
 * Deletes a single artist from the Artists collection
 * @param {string} _id - The ID of the artist to delete.
 * @return {promise} A promise that resolves when the record is deleted
 */
module.exports = (_id) => {
  return Artist.findByIdAndDelete(_id);
};
```

### Solution to Removing ###
1. `database/queries/DeleteArtist.js`

```javascript
return Artist.findById(_id)
  .then((artist) => artist.remove()); // Touches DB twice
```

2. There is usually a one-step solution to an operation

### Editing Records ###
1. `database/queries/EditArtist.js`

```javascript
const Artist = require('../models/artist');

/**
 * Edits a single artist in the Artists collection
 * @param {string} _id - The ID of the artist to edit.
 * @param {object} artistProps - An object with a name, age, yearsActive, and genre
 * @return {promise} A promise that resolves when the record is edited
 */
module.exports = (_id, artistProps) => {
  return Artist.findByIdAndUpdate(_id, artistProps);
};
```

	1. Mongoose automatically converts strings to numbers and saves where the type is `Number`

### How to Edit Single Artists ###
1. `database/queries/EditArtist.js`

```javascript
return Artist.update({ _id }, artistProps);
```

## Section 11: Hard Mode Engage ##
### Minimum and Maximum Values in a Collection ###
1. Search panel
	1. Age slider
	2. Years Active slider
2. Find min years active and max years active
	1. An approach: Sort and fetch the first record
		1. Two sorts are required
3. `database/queries/GetAgeRange.js`

```javascript
const Artist = require('../models/artist');

/**
 * Finds the lowest and highest age of artists in the Artist collection
 * @return {promise} A promise that resolves with an object
 * containing the min and max ages, like { min: 16, max: 45 }.
 */
module.exports = () => {
  return Promise.all(Artist.findOne({}).sort({ age: 1 }), Artist.findOne({}).sort({ age: -1 }));
};
```

### Solution to Min and Max Queries ###
1. `database/queries/GetAgeRange.js`

```javascript
const Artist = require('../models/artist');

/**
 * Finds the lowest and highest age of artists in the Artist collection
 * @return {promise} A promise that resolves with an object
 * containing the min and max ages, like { min: 16, max: 45 }.
 */
module.exports = () => {
  const minQuery = Artist
    .find({})
    .sort({ age: 1 })
    .limit(1)
    .then(artists => artists[0].age); // We only need the age

  const maxQuery = Artist
    .find({})
    .sort({ age: -1 })
    .limit(1)
    .then(artists => artists[0].age);
  
  return Promise.all([minQuery, maxQuery])
    .then(ages => { 
      return {min: ages[0], max: ages[1]}
    });
};
```

2. `database/queries/GetYearsActiveRange.js`

```javascript
const Artist = require('../models/artist');

/**
 * Finds the lowest and highest yearsActive of artists in the Artist collection
 * @return {promise} A promise that resolves with an object
 * containing the min and max yearsActive, like { min: 0, max: 14 }.
 */
module.exports = () => {
  const minYearsActive = Artist
    .find({})
    .sort({ yearsActive: 1 })
    .limit(1)
    .then(artists => artists[0].yearsActive);

  const maxYearsActive = Artist
    .find({})
    .sort({ yearsActive: -1 })
    .limit(1)
    .then(artists => artists[0].yearsActive);

  return Promise.all([minYearsActive, maxYearsActive]).then(yearsActive => {
    return {
      min: yearsActive[0],
      max: yearsActive[1]
    };
  });
};
```

### Challenge Mode - Search Query ###
1. `database/quaries/SearchArtist.js`

```javascript
const Artist = require('../models/artist');

/**
 * Searches through the Artist collection
 * @param {object} criteria An object with a name, age, and yearsActive
 * @param {string} sortProperty The property to sort the results by
 * @param {integer} offset How many records to skip in the result set
 * @param {integer} limit How many records to return in the result set
 * @return {promise} A promise that resolves with the artists, count, offset, and limit
 */
module.exports = (criteria, sortProperty, offset = 0, limit = 20) => {
  return Artist
    .find(criteria)
    .sort({ [sortProperty] : 1 })
    .skip(offset)
    .limit(limit)
    .then(artists => {
      return {
      all: artists,
      count: artists.length,
      offset,
      limit
    }
  });
};
```

### Sorting, Limiting, and Skipping Together ###
1. ES5 approach

```
const sortOrder = {};
sortOrder[sortProperty] = 1;

Artist.find({})
  .sort(sortOrder)
```

2. Solution:

```javascript
  const query = Artist.find({})
    .sort({ [sortProperty]: 1 })
    .skip(offset)
    .limit(limit);

  return Promise.all([query, Artist.countDocuments()])
    .then((results) => {
      return {
        all: results[0],
        count: results[1],
        offset,
        limit
      }
    });
```

### Danger! Big Challenge Ahead ###
### Filtering By Single Properties ###
1. `SearchArtis.js`

```javascript
const Artist = require('../models/artist');

/**
 * Searches through the Artist collection
 * @param {object} criteria An object with a name, age, and yearsActive
 * @param {string} sortProperty The property to sort the results by
 * @param {integer} offset How many records to skip in the result set
 * @param {integer} limit How many records to return in the result set
 * @return {promise} A promise that resolves with the artists, count, offset, and limit
 */
module.exports = (criteria, sortProperty, offset = 0, limit = 20) => {
  const query = Artist
    .find(buildQuery(criteria))
    .sort({ [sortProperty]: 1 })
    .skip(offset)
    .limit(limit);

  return Promise.all([query, Artist.countDocuments()])
    .then((results) => {
      return {
        all: results[0],
        count: results[1],
        offset,
        limit
      }
    });
};

const buildQuery = (criteria) => {
  const query = {};

  if (criteria.age) {
    query.age = {
      $gte: criteria.age.min,
      $lte: criteria.age.max
    }
  }

  return query;
}
```

### Filtering with Multiple Props ###
1. `SearchArtist.js`

```javascript
const Artist = require('../models/artist');

/**
 * Searches through the Artist collection
 * @param {object} criteria An object with a name, age, and yearsActive
 * @param {string} sortProperty The property to sort the results by
 * @param {integer} offset How many records to skip in the result set
 * @param {integer} limit How many records to return in the result set
 * @return {promise} A promise that resolves with the artists, count, offset, and limit
 */
module.exports = (criteria, sortProperty, offset = 0, limit = 20) => {
  const query = Artist
    .find(buildQuery(criteria))
    .sort({ [sortProperty]: 1 })
    .skip(offset)
    .limit(limit);

  return Promise.all([query, Artist.countDocuments()])
    .then((results) => {
      return {
        all: results[0],
        count: results[1],
        offset,
        limit
      }
    });
};

const buildQuery = (criteria) => {
  const query = {};

  if (criteria.age) {
    query.age = {
      $gte: criteria.age.min,
      $lte: criteria.age.max
    }
  }

  if (criteria.yearsActive) {
    query.yearsActive = {
      $gte: criteria.yearsActive.min,
      $lte: criteria.yearsActive.max
    }
  }

  return query;
}
```

### Handling Text Search ###
1. Documentation

```javascript
const Artist = require('../models/artist');

/**
 * Searches through the Artist collection
 * @param {object} criteria An object with a name, age, and yearsActive
 * @param {string} sortProperty The property to sort the results by
 * @param {integer} offset How many records to skip in the result set
 * @param {integer} limit How many records to return in the result set
 * @return {promise} A promise that resolves with the artists, count, offset, and limit
 */
module.exports = (criteria, sortProperty, offset = 0, limit = 20) => {
  const query = Artist
    .find(buildQuery(criteria))
    .sort({ [sortProperty]: 1 })
    .skip(offset)
    .limit(limit);

  return Promise.all([query, Artist.countDocuments()])
    .then((results) => {
      return {
        all: results[0],
        count: results[1],
        offset,
        limit
      }
    });
};

const buildQuery = (criteria) => {
  const query = {};

  if (criteria.name) {
    query.$text = {
      $search: criteria.name
    };
  }

  if (criteria.age) {
    query.age = {
      $gte: criteria.age.min,
      $lte: criteria.age.max
    }
  }

  if (criteria.yearsActive) {
    query.yearsActive = {
      $gte: criteria.yearsActive.min,
      $lte: criteria.yearsActive.max
    }
  }

  return query;
}
```

	1. Error: Text index required for $text query

### Indexes and Text Search ###
1. Index:
	1. To make efficient queries
		1. Example: Users collection
			1. Index is automatically reacted on `_id` field of every record
				1. For very fast lookups
					1. `findById` - uses index
	2. Own index
		1. Example: email field (unique)
	3. Mongo supports only indexes only on a single text field (combination of text fields is not supported)
2. Start mongo shell: `mongo`
	1. `use upstart_music` **(M)** (switches database)
	2. `show dbs` **(M)**
	3. `db.artists.createIndex({ name: "text" })` **(M)**
		1. `text` - type of index
		2. `db` - current db
		3. `artists` - collections
		4. `name` - field

### Batch Updates ###
1. Updating multiple documents
2. `SetRetired.js`

```javascript
const Artist = require('../models/artist');

/**
 * Sets a group of Artists as retired
 * @param {array} _ids - An array of the _id's of of artists to update
 * @return {promise} A promise that resolves after the update
 */
module.exports = (_ids) => {
  return Artist.updateMany(
    { _id: { $in: _ids } },
    { $set: { retired: true } }
  );
};
```

### The Hidden 'Multi' Setting ###
1. `SetRetired.js`

```javascript
module.exports = (_ids) => {
  return Artist.update(
    { _id: { $in: _ids } },
    { retired: true }
  );
};
```

	1. Updates only one document
2. Solution:

```javascript
module.exports = (_ids) => {
  return Artist.update(
    { _id: { $in: _ids } },
    { retired: true },
    { multi: true }
  );
};
```

3. `SetNotRetired.js`

```javascript
const Artist = require('../models/artist');

/**
 * Sets a group of Artists as not retired
 * @param {array} _ids - An array of the _id's of of artists to update
 * @return {promise} A promise that resolves after the update
 */
module.exports = (_ids) => {
  return Artist.update(
    { _id: { $in: _ids } },
    { retired: false },
    { multi: true }
  );
};
```

### Seeding Many Records ###
1. `faker` library
	1. For generating fake data
		1. Name
		2. Image
		3. URL
		4. Company name
		5. Date
		6. ...
	2. Helps generate huge data and test performance
2. `src/seeds.js`

```
const MINIMUM_ARTISTS = 200;
const ARTISTS_TO_ADD = 15000;
```

3. Refresh the app

### Counting the Result Set ###
1. Count is wrong in `SearchArtist.js`

```javascript
const Artist = require('../models/artist');

/**
 * Searches through the Artist collection
 * @param {object} criteria An object with a name, age, and yearsActive
 * @param {string} sortProperty The property to sort the results by
 * @param {integer} offset How many records to skip in the result set
 * @param {integer} limit How many records to return in the result set
 * @return {promise} A promise that resolves with the artists, count, offset, and limit
 */
module.exports = (criteria, sortProperty, offset = 0, limit = 20) => {
  const query = Artist
    .find(buildQuery(criteria))
    .sort({ [sortProperty]: 1 })
    .skip(offset)
    .limit(limit);

  return Promise.all([query, Artist
    .find(buildQuery(criteria)).countDocuments()])
    .then((results) => {
      return {
        all: results[0],
        count: results[1],
        offset,
        limit
      }
    });
};

const buildQuery = (criteria) => {
  const query = {};

  if (criteria.name) {
    query.$text = {
      $search: criteria.name
    };
  }

  if (criteria.age) {
    query.age = {
      $gte: criteria.age.min,
      $lte: criteria.age.max
    }
  }

  if (criteria.yearsActive) {
    query.yearsActive = {
      $gte: criteria.yearsActive.min,
      $lte: criteria.yearsActive.max
    }
  }

  return query;
}
```

## Section 12: MongoDB with Node and Express ##
### App Overview ###
1. API to serve data
2. Overview

```
	MongoDB
[Drivers Collection]
		^
		|
		v
	Node/Express
		^
		|
		v
	API Request
```

### Designing API Routes ###
1. Overview
	1. User opens a map
	2. User views all drivers nearby around them
	3. Check if they are available
2. Collection of drivers
	1. Ways to modify this collection?
		1. Add a driver
			1. When a driver signs up
		2. Delete a driver
			1. Admin wants to delete
			2. Driver exits the app
		3. Edit a driver
			1. To toggle active or inactive
		4. Find Drivers near me
			1. Within a certain radius only

### Project Setup ###
1. Requests
	1. Add a driver
		1. `POST` to `/api/drivers`
	2. Delete a driver
		1. `DELETE` to `/api/drivers/id`
	3. Edit a driver
		1. `PUT` to `/api/drivers/id`
	4. Find drivers near me
		1. `GET` to `/api/drivers`
2. Node/Express
	1. Takes incoming API request
	
	```
	POST /api/drivers HTTP/1.1
	User-Agent: Mozilla/4.0 (cmpatible; MSIE5.01; Windows NT)
	Host: www.muber.com
	Content-Type: application/json
	Accept-Language: en-us
	Accept-Encoding: gzip, deflate
	Connection: Keep-Alive
	
	{"email": "test@test.com"}
	```
	
		1. URL
		2. Headers
		3. Body

### HTTP Request Methods ###
1. Request Methods
	1. Creation - POST
	2. Deleting - DELETE
	3. Editing - PUT
	4. Reading - GET
2. Architecture:

```
client Side App
	Creation of Driver: POST to /api/drivers
	Delete a Driver: DELETE to /api/drivers/id
	Edit a Driver: PUT to /api/drivers/id
	Find Drivers new me: GET to /api/drivers
	|
	v
Node/Express Server
	Process incoming request, modify Drivers collection as appropriate
	|
	v
Mongo
```

### The Basics of Express ###
1. `mkdir muber`
2. `cd muber`
	1. `npm init`
	2. Defaults
	3. `npm install --save mongoose express mocha`
3. Node vs Express
	1. Node: Engine for running Javascript outside of a browser environment. Can work with HTTP requests
	2. Express: Framework to simplify working with HTTP requests
		1. Makes it easier to work with HTTP requests
			1. For very common use-cases
				1. Interpreting HTTP requests and what to do with them

### Express Boilerplate ###
1. Express app

```
POST to /api/drivers
  |
  v
Router
  |
  v
Controller <-> Model
  |
  v
MongoDB
```

2. `app.js`

```javascript
const express = require('express');
const app = express(); // Create an instance of the Express application. This instance will be used to define routes, middleware, and other configurations for the web server.

modules.export = app;
```

3. `index.js`

```javascript
const app = require('./app');

app.listen(3050, () => {
  console.log('Running on port 3050');
});
```

### Handling Requests with Express ###
1. Request handlers handle requests sent to particular routes
2. Architecture

```
req -> Express
res <- Express
```

	1. `req` - request object
	2. `res` - response object
3. `node index.js`
	1. Open: `http://localhost:3050/api`
4. `app.js`

```javascript
const express = require('express');
const app = express(); // Create an instance of the Express application. This instance will be used to define routes, middleware, and other configurations for the web server.

// Watch for incoming requests of method GET to the route http://localhost:3050/api
app.get('/api', (req, res) => {
  res.send({
    hi: 'there',
  });
});

module.exports = app;
```

### Testing Express Apps with Mocha ###
1. `npm i --save supertest`
2. `test/app_test.js`

```javascript
const assert = require('assert');
const request = require('supertest');
const app = require('../app');

describe('The express app', () => {
  it('handles a GET request to /api', async () => {
    await request(app)
      .get('/api')
      .end((err, response) => {
        console.log(response);
      });
  });
});
```

### Running Mocha ###
1. `npm i --save nodemon`
2. `package.json`

```json
  ...
  "scripts": {
    "test": "nodemon --exec \"mocha --recursive -R min\""
  },
  ...
```

3. `npm i --save supertest`
4. `test/app_test.js`

```javascript
const assert = require('assert');
const request = require('supertest');
const app = require('../app');

describe('The express app', () => {
  it('handles a GET request to /api', async () => {
    const response = await request(app).get('/api');
    assert(response.body.hi === 'there');
  });
});
```

### Project Structure ###
1. Router
	1. Looks at incoming request (URL and Method) and sends to the appropriate handler
	2. We can place all the handlers in a controller
2. Controller
	1. It works with a Model
3. Model
	1. Mongoose model

### Refactoring for Controllers and Models ###
1. `controllers/drivers_controller.js`

```javascript
module.exports = {
  greeting(req, res) {
    res.send({
      hi: 'there',
    });
  },
};
```

2. `routes/routes.js`

```javascript
const DriversController = require('../controllers/drivers_controller');

module.exports = (app) => {
  // Watch for incoming requests of method GET to the route http://localhost:3050/api
  app.get('/api', DriversController.greeting);
};
```

3. `app.js`

```javascript
const express = require('express');
const routes = require('./routes/routes');
const app = express(); // Create an instance of the Express application. This instance will be used to define routes, middleware, and other configurations for the web server.

routes(app);

module.exports = app;
```

### The Driver Model ###
1. Driver
	1. email: String
	2. driving: Boolean
	3. location: ???
		1. Deferred for now
2. `models/drivers.js`

```javascript
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

const DriverSchema = new Schema({
  email: {
    type: String,
    required: true,
  },
  driving: {
    type: Boolean,
    default: false,
  },
});

const Driver = mongoose.model('driver', DriverSchema);

module.exports = Driver;
```

### The Create Drivers Route ###
1. `routes/routes.js`

```javascript
const DriversController = require('../controllers/drivers_controller');

module.exports = (app) => {
  // Watch for incoming requests of method GET to the route http://localhost:3050/api
  app.get('/api', DriversController.greeting);

  app.post('/api/drivers', DriversController.instantiate);
};
```

2. `controllers/drivers_controller.js`

```javascript
module.exports = {
  greeting(req, res) {
    res.send({
      hi: 'there',
    });
  },
  instantiate(req, res) {},
};
```

### The BodyParser Middleware ###
1. POST request has request body
2. Node receives the body as follows:
	1. New request!
	2. Here's a part of it... (a tiny chunk is received at a time)
	3. Here's a part of it...
	4. ...
	5. Done! Call the route handler.
3. Express doesn't handle request body
	1. Solution: Body parser library
		1. [https://www.npmjs.com/package/body-parser](https://www.npmjs.com/package/body-parser)
			1. `req.body`
		2. `npm i --save body-parser` **(M)**
4. `app.js`

```javascript
const express = require('express');
const bodyParser = require('body-parser');
const routes = require('./routes/routes');
const app = express(); // Create an instance of the Express application. This instance will be used to define routes, middleware, and other configurations for the web server.

app.use(bodyParser.json()); // Assume that incoming request is JSON and parse it to an object. Placed before `routes(app)`

routes(app);

module.exports = app;
```

### Testing Driver Creation ###
1. `controllers/drivers_controller.js`

```javascript
module.exports = {
  greeting(req, res) {
    res.send({
      hi: 'there',
    });
  },
  instantiate(req, res) {
    console.log(req.body);
    res.send({
      hi: 'there',
    });
  },
};
```

2. `test/controllers/drivers_controller_test.js`

```javascript
const assert = require('assert');
const request = require('supertest');
const app = require('../../app');

describe('Drivers controller', () => {
  it('Post to /api/drivers instantiates a new driver', async () => {
    const response = await request(app)
      .post('/api/drivers')
      .send({ email: 'test@test.com' });
  });
});
```

### More on Testing Driver Creation ###
1. `drivers_controller_test.js`

```javascript
const assert = require('assert');
const request = require('supertest');
const app = require('../../app');
const mongoose = require('mongoose');
const Driver = require('../../models/driver');

describe('Drivers controller', () => {
  it('Post to /api/drivers instantiates a new driver', async () => {
    const count = await Driver.countDocuments();
    const response = await request(app)
      .post('/api/drivers')
      .send({ email: 'test@test.com' });
    const newCount = await Driver.countDocuments();
    assert(count + 1 === newCount);
  });
});
```

### Additional Mongoose Setup ###
1. `app.js`

```javascript
const express = require('express');
const bodyParser = require('body-parser');
const mongoose = require('mongoose');
const routes = require('./routes/routes');
const app = express(); // Create an instance of the Express application. This instance will be used to define routes, middleware, and other configurations for the web server.

mongoose.Promise = global.Promise;
mongoose.connect('mongodb://127.0.0.1:27017/muber');

app.use(bodyParser.json()); // Assume that incoming request is JSON and parse it to an object. Placed before `routes(app)`

routes(app);

module.exports = app;
```

2. `test/controllers/drivers_controller_test.js`

```javascript
const assert = require('assert');
const request = require('supertest');
const app = require('../../app');
const mongoose = require('mongoose');
const Driver = mongoose.model('driver');

describe('Drivers controller', () => {
  it('Post to /api/drivers instantiates a new driver', async () => {
    const count = await Driver.countDocuments();
    const response = await request(app)
      .post('/api/drivers')
      .send({ email: 'test@test.com' });
    const newCount = await Driver.countDocuments();
    assert(count + 1 === newCount);
  });
});
```

### Driver Implementation ###
1. `controllers/drivers_controller.js`

```javascript
const Driver = require('../models/driver');

module.exports = {
  greeting(req, res) {
    res.send({
      hi: 'there',
    });
  },
  instantiate(req, res) {
    const driverProps = req.body;
    Driver.create(driverProps).then((driver) => {
      res.send(driver);
    });
  },
};
```

### Testing Endpoints with Postman ###
1. POST: http://localhost:3050/api/drivers
2. Body:

```json
{
  "email": "test@test.com"
}
```

```json
{
    "email": "test@test.com",
    "driving": false,
    "_id": "6a62f7071a71a6f50e69e038",
    "__v": 0
}
```

3. Two tasks:
	1. Clean up database before testing
	2. Handle errors

### Dev vs Test Environments ###
1. We don't want to drop a Dev database
	1. When running our server for development (or production)
		1. Server Startup
		2. Connect to DB
			1. Leave data as it is
	2. When running our server for test
		1. Server startup
		2. Connect to DB
		3. Drop collections

### Separate Test Databases ###
1. Machine
	1. Environment Variable
		1. `NODE_ENV`
			1. To specify `dev`, `test`, or `prod`
	2. Node
		1. `process.env.NODE_ENV`
2. `package.json`

```json
  "scripts": {
    "test": "NODE_ENV=test nodemon --exec \"mocha --recursive -R min\""
  },
```

3. `app.js`

```javascript
const express = require('express');
const bodyParser = require('body-parser');
const mongoose = require('mongoose');
const routes = require('./routes/routes');
const app = express(); // Create an instance of the Express application. This instance will be used to define routes, middleware, and other configurations for the web server.

mongoose.Promise = global.Promise;
if (process.env.NODE_ENV !== 'test') {
  mongoose.connect('mongodb://127.0.0.1:27017/muber');
}

app.use(bodyParser.json()); // Assume that incoming request is JSON and parse it to an object. Placed before `routes(app)`

routes(app);

module.exports = app;
```

4. Fix:

```
npm i --save-dev cross-env
```

```json
  "scripts": {
    "test": "cross-env NODE_ENV=test nodemon --exec \"mocha --recursive -R min\""
  },
```

5. `test/test_helper.js`

```javascript
const mongoose = require('mongoose');

before(async () => {
  await mongoose.connect('mongodb://127.0.0.1:27017/muber_test');
  await mongoose.connection
    .once('open', () => {
      console.log('Connection has been made, now make fireworks...');
    })
    .on('error', (error) => {
      console.warn('Warning', error);
    });
});

beforeEach(async () => {
  const { drivers } = mongoose.connection.collections;
  try {
    await drivers.drop();
  } catch (error) {
    console.warn(error);
  }
});
```

### Middlewares in Express ###
1. If no body is sent, it hangs
	1. Solution: Middleware
2. Middleware

```
Incoming Request (req) ----+
                           |
						   v
						   middleware
						   |
						   v
						   middleware
						   |
						   v
		                   handler
				           | (if error)
						   v
				(res) <-   middleware
```

	1. They intercept requests and do some processing
		1. Either on `req` object or on `res` object
		2. If anything goes wrong, we pass on to a middleware
3. `controllers/drivers_controller.js`

```javascript
const Driver = require('../models/driver');

module.exports = {
  greeting(req, res) {
    res.send({
      hi: 'there',
    });
  },
  instantiate(req, res, next) {
    const driverProps = req.body;
    Driver.create(driverProps)
      .then((driver) => res.send(driver))
      .catch(next);
  },
};
```

4. `test/test_helper.js`

```javascript
const mongoose = require('mongoose');

before(async () => {
  await mongoose.connect('mongodb://127.0.0.1:27017/muber_test');
  await mongoose.connection
    .once('open', () => {
      console.log('Connection has been made, now make fireworks...');
    })
    .on('error', (error) => {
      console.warn('Warning', error);
    });
});

beforeEach(async () => {
  const { drivers } = mongoose.connection.collections;
  try {
    await drivers.drop();
  } catch (error) {
    console.warn(error);
  }
});
```

5. `app.js`

```javascript
const express = require('express');
const bodyParser = require('body-parser');
const mongoose = require('mongoose');
const routes = require('./routes/routes');
const app = express(); // Create an instance of the Express application. This instance will be used to define routes, middleware, and other configurations for the web server.

mongoose.Promise = global.Promise;
if (process.env.NODE_ENV !== 'test') {
  mongoose.connect('mongodb://127.0.0.1:27017/muber');
}

app.use(bodyParser.json()); // Assume that incoming request is JSON and parse it to an object. Placed before `routes(app)`

routes(app); // Needs to call `next`

app.use((err, req, res, next) => {
  // `err` - populated if a previous middleware threw an error. It will be set to the error that was thrown
  // `req`, `res` - incoming request and outgoing response respectively
  // `next` - function that can be called that passes control to the next middleware. It is optional
  // console.log(err);
  res.status(422).send({ error: err.message });
});

module.exports = app;
```

### Handling Editing of Drivers ###
1. `routes/routes/js`

```javascript
  app.put('/api/drivers/:id', DriversController.edit);
```

2. `controllers/drivers_controller.js`

```javascript
  edit(req, res, next) {
    const driverId = req.params.id;
    const driverProps = req.body;
    Driver.findByIdAndUpdate({ _id: driverId }, driverProps)
      .then(() => {
        Driver.findById({ _id: driverId }).then((driver) => res.send(driver));
      })
      .catch(next);
  },
```

### Testing Driver Updates ###
1. `test/drivers_controller_test.js`

```javascript
  it('PUT to /api/drivers/:id edits an existing driver', async () => {
    const driver = new Driver({ email: 't@t.com', driving: false });
    await driver.save();
    await request(app)
      .put(`/api/drivers/${driver._id}`)
      .send({ driving: true });
    const sameDriver = await Driver.findOne({ email: 't@t.com' });
    assert(sameDriver.driving === true);
  });
```

### Handling Deletion of Drivers ###
1. `controllers/drivers_controller.js`

```javascript
  delete(req, res, next) {
    const driverId = req.params.id;
    Driver.findByIdAndDelete({ _id: driverId })
      .then((driver) => {
        res.status(204).send(driver);
      })
      .catch(next);
  },
```

2. `routes/routes.js`

```javascript
  app.delete('/api/drivers/:id', DriversController.delete);
```

### Testing Driver Deletion ###
1. `test/controllers/drivers_controller_test.js`

```javascript
  it('DELETE to /api/drivers/:id deletes an existing driver', async () => {
    const driver = new Driver({ email: 't@t.com' });
    await driver.save();
    const count = await Driver.countDocuments();
    assert(count == 1);
    await request(app).delete(`/api/drivers/${driver._id}`);
    const newCount = await Driver.countDocuments();
    assert(newCount === 0);
  });
```

2. Another approach:

```javascript
  it('DELETE to /api/drivers/:id deletes an existing driver', async () => {
    const driver = new Driver({ email: 't@t.com' });
    await driver.save();
    await request(app).delete(`/api/drivers/${driver._id}`);
    const sameDriver = await Driver.findOne({ email: 't@t.com' });
    assert(sameDriver === null);
  });
```

### Geography with MongoDB ###
1. To find drivers within a certain radius
	1. Users should pass their current location
2. Mongo uses [Longitue, Latitude]
	1. First-class support
		1. Latitude: y direction
		2. Longitude: x direction
3. Mapping systems:
	1. 2d
		1. Assumes 2d plane
			1. Distance is determined by Pythagorian theorem
		2. Good for small slices of the earth
	2. 2d sphere
		1. More complex
		2. More realistic
		3. Distance between u to v
			1. Along the surface of a sphere
		4. Good for long distances compared to the earth

### The GeoJSON Schema ###
1. GeoJSON - used to store longitude and latitude
	1. [geojson.org](geojson.org)
		1. `Point` type
		
		```json
		{
		  "type": "Feature",
		  "geometry": {
		    "type": "Point",
			"coordinates": [125.6, 10.1]
		  },
		  "properties": {
		    "name": "Dinagat Islands"
		  }
		}
		```
		
2. `models/driver.js`

```javascript
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

const PointSchema = new Schema({
  type: {
    type: String,
    default: 'Point',
  },
  coordinates: {
    type: [Number],
    index: '2dsphere', // For geojson type queries
  },
});

const DriverSchema = new Schema({
  email: {
    type: String,
    required: true,
  },
  driving: {
    type: Boolean,
    default: false,
  },
  geometry: PointSchema,
});

const Driver = mongoose.model('driver', DriverSchema);

module.exports = Driver;
```

### GeoNear Queries ###
1. [mongoosejs.com/docs/guide.html](mongoosejs.com/docs/guide.html)
	1. Search: `Model.geoNear(GeoJSON, options, [callback])`
2. `routes/routes.js`

```javascript
  app.get('/api/drivers', DriversController.index);
```

3. `controllers/drivers_controller.js`

```javascript
  index(req, res, next) {
    const { lng, lat } = req.query;
    Driver.geoNear(
      {
        type: 'Point',
        coordinates: [lng, lat],
      },
      {
        spherical: true,
        maxDistance: 200000, // meters, 200 Km
      },
    );
  },
```

### Major GeoNear Aggregation Update ###
1. Old style: `geoNear` wrapped documents in an object with the structure `{obj: document, dis: distance}`
2. New style: `geoNear` doesn't do the wrapping
	1. Instead of the following:
	
	```
	Driver.geoNear(
	  { type: 'Point', coordinates: [parseFloat(lng), parseFloat(lat)] },
	  { spherical: true, maxDistance: 200000 }
	)
	  .then(drivers => res.send(drivers))
	  .catch(next);
	```
	
	2. Do the following:
	
	```
	Driver.aggregate([
	  {
	    $geoNear: {
	      near: { type: 'Point', coordinates: [parseFloat(lng), parseFloat(lat)] },
		  spherical: true,
		  maxDistance: 200000,
		  distanceField: 'dist'
		}
	  }
	])
	  .then(drivers => {
	    const wrappedDrivers = drivers.map(driver => ({ obj: driver }));
		res.send(wrappedDrivers);
	  })
	  .catch(next);
	},
	```

### Testing a GeoNear Query ###
1. `test/controllers/drivers_controller_test.js`

```javascript
  it('GET to /api/drivers finds drivers in a location', async () => {
    const seattleDriver = new Driver({
      email: 'seattle@test.com',
      geometry: {
        type: 'Point',
        coordinates: [-122.4759902, 47.6147628],
      },
    });
    const miamiDriver = new Driver({
      email: 'miami@test.com',
      geometry: {
        type: 'Point',
        coordinates: [-80.253, 25.791],
      },
    });
    await Promise.all([seattleDriver.save(), miamiDriver.save()]);
    const response = await request(app).get('/api/drivers?lng=-80&lat=25');
    console.log(response);
  });
```

### One Big Gotcha ###
1. `muber_test` doesn't have 2d or 2dsphere index
	1. Index gets dropped if collection is dropped
		1. Fix: `test_helper.js`
		
```javascript
beforeEach(async () => {
  const { drivers } = mongoose.connection.collections;
  try {
    await drivers.drop(); // kills indixes, too
    await drivers.createIndex({
      'geometry.coordinates': '2dsphere',
    });
  } catch (error) {
    console.warn(error);
  }
});
```

2. Fix: `controllers/drivers_controller.js`

```javascript
  index(req, res, next) {
    const { lng, lat } = req.query;
    Driver.aggregate([
      {
        $geoNear: {
          near: {
            type: 'Point',
            coordinates: [parseFloat(lng), parseFloat(lat)],
          },
          spherical: true,
          maxDistance: 200000,
          distanceField: 'dist',
        },
      },
    ])
      .then((drivers) => res.send(drivers))
      .catch(next);
  },
```

### Another Big Gotcha ###
1. Fix: `lng`, and `lat` are strings. They must be parsed using `parseFloat`

### Testing GeoQueries ###
1. Empty `body`
	1. Typo
2. `test/controllers/drivers_controller_test.js`

```javascript
  it('GET to /api/drivers finds drivers in a location', async () => {
    const seattleDriver = new Driver({
      email: 'seattle@test.com',
      geometry: {
        type: 'Point',
        coordinates: [-122.4759902, 47.6147628],
      },
    });
    const miamiDriver = new Driver({
      email: 'miami@test.com',
      geometry: {
        type: 'Point',
        coordinates: [-80.253, 25.791],
      },
    });
    await Promise.all([seattleDriver.save(), miamiDriver.save()]);
    const response = await request(app).get('/api/drivers?lng=-80&lat=25');
    assert(response.body.length === 1);
    assert(response.body[0].email === 'miami@test.com');
  });
```

## Section 13: Extras ##
### Bonus! ###
1. [ChatGPT and LangChain](https://www.udemy.com/course/chatgpt-and-langchain-the-complete-developers-masterclass/?couponCode=4CCDA21198171837F008)
2. [SQL and PostgreSQL: The Complete Developer's Guide](https://www.udemy.com/course/sql-and-postgresql/?couponCode=983CEA231DA59F4596C2)