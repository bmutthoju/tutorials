# MongoDB - The Complete Dev BootCamp | Beginner-Expert #
## Installation and Setup ##
### Installation of MongoDB ###
1. Download from: [https://www.mongodb.com/docs/manual/installation/](https://www.mongodb.com/docs/manual/installation/)
2. Use community edition or enterprise edition
	1. Docker: Only enterprise edition
	2. Windows:
		1. Install MongoDB Server + Compas
			1. Complete - recommended
				1. MongoDB + Tools
		2. Install Mongosh

### Update - Installation of MongoDB - (New) ###
1. Current version is: 7.x

### Starting MongoDB Server and Client Connection ###
1. One window: Run Mongo
	1. `mongod --config /usr/local/etc/mongod.conf` **(M)**
		1. If we stop this, we cannot connect
	2. Starting Mongo as a background service:
		1. `brew services start mongodb/brew/mongodb-community` **(M)**
2. Second window: Send commands to Mongo server
	1. `mongo` **(M)** (Windows: [https://www.mongodb.com/try/download/shell](https://www.mongodb.com/try/download/shell))
		1. `show dbs` **(M)**

### Update - Starting MongoDB Server and Client Connection - (New) ###
1. Mac OS: `brew services start mongodb-community@6.0`
	1. Stop: `brew services stop mongodb-community@6.0`
2. Use `mongosh` **(M)** instead of `mongo`
	1. Visit mongodb homepage for regular updates

### Read Me Please! ###
1. Look for latest MongoDB updates
	1. To ensure optimal utilization of the database system
		1. Visit the documentation: [https://www.mongodb.com/docs/v6.0/administration/install-community/](https://www.mongodb.com/docs/v6.0/administration/install-community/)
			1. For:
				1. New features
				2. Improvements
				3. Installation instructions

### Compass Installation ###
1. It is a GUI for MongoDB
	1. It is an interactive tool for querying, optimizing, and analyzing MongoDB data
	2. Download
		1. Install
	3. Open
		1. Connect
		2. Databases

## Database | Collection | Document | Data ##
### Class - Database vs Collection vs Document vs Data ###
1. MongoDB Server
	1. We can have multiple databases inside a server
		1. We can have multiple collections inside each database
			1. We can have multiple documents inside each collection
				1. We can have multiple data inside each document
2. Collection:
	1. Synonymous to Table in RDBMS
3. Document:
	1. Synonymous to Rows in RDBMS

## Database ##
### Class - Understanding Database in MongoDB ###
1. Database contains the collection of documents
2. View Database:
	1. `show dbs` **(M)**

### Class - Database Naming Rules in MongoDB ###
1. Names are case-sensitive
	1. `schooldb` and `schoolDb` are different
		1. `db.schooldb` - okay
			1. `db.schoolDb` - not okay
		2. `use schoolDB` - doesn't work
			1. There is resemblance
	2. Windows users: The following are not allowed to be in the name of the DB
		1. /
		2. \
		3. .
		4. "
		5. $
		6. *
		7. :
		8. |
		9. ?
	3. Unix/Linux Users:
		1. /
		2. \
		3. .
		4. $
		5. "
	4. Names can not be null
	5. A database cannot be empty
		1. `show dbs` **will not show an empty database**
	6. Fewer than 64 characters

### Class - Constructing a Database ###
1. There is no specific command to construct a database
	1. It gets automatically created for us
		1. How is it created?
	
				use school

			1. If it is an existing db, MongoDB will switch to it, without constructing a new one
			2. If it doesn't exist, it will be created for us & switch to it
			3. To see in which db we are
			
					db

			4. New DB:

					use school

### Lab - Constructing a Database ###
1. Check available dbs:

		show dbs

	1. Only system generated dbs exist
2. New DB:

		use school
		show dbs

	1. Doesn't show `school`
3. Check DB:

		db
		
	1. Shows `school`
4. New DB

		use james

		show dbs

	1. `school` and `james` are not in the list

### Class - Deleting a Database ###
1. Drop Database
2. Example: Let us assume there are dbs with data
3. To delete a DB, we need to go to the DB

		use school

		db.dropDatabase() # **(M)**

	1. `school` will be removed from the system

## Collection ##
### Class - Understanding Collection in MongoDB ###
1. What is a collection?
	1. It is a group of documents
		1. Assuming they have some similarites (depends on requirements), the documents are grouped into collections
	2. RDBMS:
		1. Table
2. Comparison:
	1. Database - Database
	2. Table - Collection
	3. Rows - Documents
	4. Columns - Fields

### Class - Naming Rules for Collection ###
1. It must start with a character or underscore
2. The name cannot contain:
	1. $
	2. Empty string: ("  ")
	3. Null character
	4. Cannot beging with `system.prefix` (for internal use)

### Class & Lab - Constructing Collection ###
1. We use the `createCollection()` **(M)** method
2. Syntax:

		db.createCollection(name, options) # **(M)**

	1. `name` - string
	2. `options` - document
		1. `capped` **(M)** - Boolean
			1. Fixed-size collection or not
		2. `autoIndexId` **(M)** - Boolean
			1. `true` - generates an auto-index id
		3. `size` **(M)** - Number
			1. Maximum size of the cap in bytes
		4. `max` **(M)** - Number
			1. Maximum number of documents we can put in the collection
3. Example:

		> db.createCollection("students")
		{"OK": 1}
	
	1. `1` - One collection has been created in the `school` database
4. Commands:

		db.createCollection("students")
		show dbs # shows school

	1. It also shows in Compas
5. Collection with options:

		db.createCollection("student", {capped: true, autoIndexId: true, size: 6142800, max: 1000})

6. Commands:

		use users
		db.createCollection("people", {capped: true, autoIndexId: true, 6142800, max: 1000})
		show dbs

7. `show collections` **(M)** - shows all collections in the database
8. Commands:

		use users
		db
		show collections 

		use school
		show collections

9. It is not important for me to instantiate a collection beforehand
	1. We can directly insert a document into a non-existing collection
		1. MongoDB constructs is automatically

				db.shoes.insert({"name": "Adidas"})

			1. `shoes` - created automatically

10. New database:
	
		use wear
		db
		show collections
		db.shoe.insert({"name": "Adidas"})
		show collections
		show dbs

11. Dopping a collection:

		show collections
		db.shoe.drop() # **(M)**

## Data Type ##
### Class - Understanding MongoDB Data Type ###
1. String
	1. UTF-8 - encoding standard to be used
	2. `"<string>"`
2. Integer
	1. Numerical values
		1. 32 bit - depends on server
		2. 64 bit - depends on server
3. Boolean
	1. true/false
4. Double
	1. Floating values:
		1. 10.5
		2. 100.67
5. min/max key
	1. For BSON elements, we use the min/max key to compare values against lowest or highest values
6. Arrays
	1. multiple values
	2. List
	3. Array
	4. key/value pairs
		1. value can be
			1. multiple values
			2. list
			3. array
7. null
8. Objects
	1. Used to embedded documents
9. Symbol
	1. For symbols specific to a language
10. Timestamp
	1. ctimestamp
11. Date
	1. To store date or time in unix format
	2. We can construct a date object and specify
		1. month
		2. year
		3. day
		4. time
12. ObjectID
	1. For document id
13. Binary Data
14. Code
	1. Language code
		1. JavaScript code
15. Regular Expression

## JSON vs BSON ##
### Class - Understanding JSON and BSON ###
1. JSON
	1. JavaScript Object Notation
	2. We see it in 
		1. API
		2. Log messages
		3. Configuration files
		4. Database Storage
	3. Encoding: UTF-8
	4. Data Support:
		1. Numbers
		2. Array
		3. String
		4. Boolean
	5. Readability
		1. Human
		2. Machine
2. BSON (superset of JSON)
	1. Binary JSON
	2. Created for MongoDB
	3. Anything represented in JSON can be represented in BSON
		1. Internally JSON is BSON
		2. BSON can be retieved as readable JSON format using MongoDB driver
	4. JSON documented is stored as BSON document internally by MongoDB
	5. BSON example:

		\x16\x00\x00\... - machine language (BSON language)

	6. Encoding: Binary
	7. Data Support:
		1. Numbers
		2. Array
		3. String
		4. Boolean
		5. Date
		6. Binary
		7. ...
	8. Readability
		1. Machine

## MongoDB Documents | Data Modelling ##
### Class - Understanding MongoDB Document ###
1. We need to convert JSON into BSON (Binary representation of JSON)
	1. JSON is used to design documents
	2. BSON is used to store a document
2. Syntax of a document:

		{
			"__id": ObjectId("424f...."),
			"name": "James",
			"phone": "2842833232"
		}

	1. key/value notation is used
	2. `__id` - it is for the entire document (Object)
		1. Optional
			1. System automatically generates
		2. It is **Primary Key** field
		3. We can give a number manually
	3. The strings on the left are called **fields**
	4. The **values** are on the right side
	5. `".."` - **double quotes are optional**

			name: Fred
			"first name": Fred # here it is required

	6. A document is a row in MongoDB
	7. Group of documents makes a collection
	8. `:` - separator between key and value

### Class - JSON Syntax ###
1. Name: Peter, Age: 20, Gender: Male
2. JSON:

		{
			"name": "Peter",
			"age": 20,
			"gender": "male"
		}
		
		{"name:"Peter","age":20,"gender":"male"}

	1. keys
	2. values
3. MongoDB:

		{
			name: "Peter",
			age: 20,
			gender: "male"
		}

### Class - Array in JSON ###
1. Skill: 
	1. Programming:
		1. Python
		2. SQL
		3. MongoDB
	2. JSON representation: Array

			{
				"name": "Peter",
				"age": 20,
				"gender": "male",
				"skills": [
					"Python",
					"SQL",
					"MongoDB"
				]
			}

### Class - Array Containing Object ###
1. Syntax:

		[
			{
				"name": "James",
				"age": 22
			},
			{
				"name": "Peter",
				"age": 30
			},
			{
				"name": "Jane",
				"age": 18
			}
		]

### Class - Important Points on Mongo DB Document ###
1. `_id` - reserved for unique primary key
	1. We can decide to change it to any type except an array
2. `""` - optional
3. Field name cannot be null
4. Field value can be null
5. Field name cannot be duplicated
	1. In MongoDB

			name: James
			name: Ahmed

		1. Not allowed

6. To access the elements of a document, we can use `.`
7. If there is a space between names, put `""`
8. Fields in BSON document are ordered

		{
			a: 1,
			b: 2,
			c: 3
		}
			// Not the same as

		{
			b: 2,
			a: 1,
			c: 3
		}

9. Keep the ordered fields except `_id` (it is on top)
10. Schemaless
	1. Collection can have documents with different fields

			{
				"name: "a",
				"age:" 35
			}

11. Document size: 16MB Max
	1. If we want bigger documents: Use GridFS
		1. GridFS - specification to store documents above 16MB
12. JSON is converted into BSON using **MongoDB Driver**

### Class - Embedded Documents ###
1. Document inside another document
2. Example: Address

		{
			"house_no": 3434,
			"stree": "",
			"city": "",
			"state": "",
			"country": "",
		}

		{
			name: "Peter",
			age: 34,
			"gender": "male",
			"skill": [
				"python",
				"sql",
				"mongodb",
			],
			"address": {
				house_number: "22 Vic",
				street: "James Close",
				city: "New Oil",
				state: "Bush",
				country: "Mars"
			}
		}

### Class - Embedded Nested Documents by Example ###
1. Example:

		{
			name: "Kase",
			gender: "female",
			department: {
				_id: ObjectId("sdgsdfdsfdsf"),
				name: "sssdfdsf"
			},
			"address": {
				//...
			}
		}

	1. We can nest 100 documents

### Class - Important Points on Embedded Documents ###
1. Upto 100 levels of nesting
2. Support maximum size of 16MB
3. Can be accessed using the dot notation

### Class - Patterns in Document Writing ###
1. Pattern in Document Writing:
	1. `{" ": " "}`
	2. `{" ": " ", " ": " ", ...}`
	3. `[{...}, {...}, ..., {...}]`
	4. `[" ", " ", " ", " "]`
	5. `[ , " ", , , " ", ]`

## Ways of Inserting / Constructing Documents ##
### Class - Understanding Document Insertion ###
1. Inserting documents into collection
	1. Three methods:
		1. `insertOne()` **(M)**
			1. One document only
		2. `insertMany()` **(M)**
			1. Many documents/ Mutliple documents
			2. It cannot be used for one
		3. `insert()` **(M)**
			1. One or many documents

## Understanding insertOne() ##
### Class - Syntax ###
1. `insertOne()`
2. Syntax:

		db.<collection>.insertOne(<document>, [writeConcern])

	1. `<collection>` - name of the collection we want to insert document into
	2. `db` - refers to the current database
		1. `db` command returns the current database
			1. `use <db-name>` to switch the db
	3. `writeConcern` - The level of acknowledgement we need from MongoDB for a write operation
		1. `1` - Operation was successful
		2. `0` - Operation was not successful

### Class - InsertOne() by Example ###
1. Example:

		db.student.insertOne({
			name: "Peter",
			last_name: "Andrew",
			email: "peter@gmail.com"
		})

	1. Output:
			
			{
				acknowledged: true,
				insertedId: ObjectId("23432....")
			}

### Lab - InsertOne() by Example ###
1. Verification

		db
		show dbs
		use school
		show collections

		db.student.insertOne({
			name: "Peter",
			last_name: "Andrew",
			email: "peter@gmail.com"
		})

	1. Collection is automatically created

			show collections

### Class & Lab - Finding Documents in a Collection ###
1. Listing data in collection: `find()` **(M)**

		db.<collection>.find() # output is messy
		db.<collection>.find().pretty() # **(M)** formatted output

### Class - InsertOne() by Example II ###
1. Example:

		db.student.insertOne({
			fname: "Jane",
			lname: "Mike",
			mail: "jna@yahoo.com"
		})

	1. It is allowed
		1. MongoDB doesn't depend on schema
			1. To change any column, we don't have to redesign the table

### Lab - InsertOne() by Example II ###
1. Insert:
	1. Both documents get inserted

### Class - How to Manually Insert_id ###
1. Inserting id manually

		db.student.insertOne({
			_id: 1,
			first_name: "Peter",
			last_name: "Andrew",
			email: "peter@gmail.com"
		}

### Lab - How to Manually Insert_Id ###
1. Insert id manually

		{
			"acknowledged": true,
			"insertedId: 3
		}

### Class & Lab - Error in Inserting Existing_Id ###
1. Try to insert an existing _id

		db.student.insertOne({
			_id: 1
		})

		MongoServerError
		E11000 duplicate key error

## Understanding insertMany() ##
### Class - Syntax ###
1. Syntax:

		db.<collection>.insertMany([
			<document-1>,
			<document-2>,
			...
		], 
		{
			writeConcern: <document>,
			ordered: <boolean>
		})

### Class - InsertMany() by Example ###
1. Insertion:

		db.employees.insertMany([
			{
				fname: "Anthony",
				lname: "Wood",
				email: "wood@a.com"
			},
			{
				fname: "Tude",
				lname: "Ben",
				email: "ben@a.com"
			},
				fname: "Jane",
				lname: "Cook",
				email: "cook@a.com"
			}
		])

### Lab - InsertMany() by Example ###
1. Command:

		use abc_ltd
		db
		db.abc_ltc.insertMany([
			//...
		])

		db.employees.find().pretty()

### Class & Lab - Custom ID ###
1. Custom ID:

		{
			_id: 1,
			...
		},
		{
			_id: 2,
			...
		},
		{
			_id: 3,
			...
		}

## Understanding insert() ##
### Class - Understanding insert() ###
1. Two options
	1. One/single
	2. Multiple/many
2. Syntax:

		db.<collection>.insert(
			<document>, OR
			[<document>, <document>, ....],
			[writeConcern],
			[ordered]
		)

### Class & Lab - Insert by Example ###
1. Example:

		db.student.insert(
			{
				name: "Peter James"
			}
		)

		db.student.insert(
			[
				{
					name: "Peter James"
				},
				{
					name: "Ahmed Khan"
				}
			]
		)

		db.student.insert({
			first_name: "Peter",
			last_name: "Andrew",
			emai: "peter@gmail.com"
		})

		db.staff2.insert([
			{
				fname: "Anthony",
				lname: "Wood",
				email: "wood@a.com"
			},
			{
				fname: "Tude",
				lname: "Ben",
				email: "ben@a.com"
			},
				fname: "Jane",
				lname: "Cook",
				email: "cook@a.com"
			}	
		])

### Class & Lab - Understanding ORDERED | true ###
1. By default: ordered is true
	1. If we give id to only one document in the list, Mongo will stop working after reaching that document
		1. It will report the number of documents inserted until it reaches the document
2. Example:

		db.staff2.insert(
			[
				{
					fname: "Dan222",
					lname: "Wood",
					email: "d@a.com"
				},
				{
					_id: 1,
					fname: "Kate222",
					lname: "Ben",
					email: "k@a.com"
				},
				{
					fname: "Paul222",
					lname: "Cook",
					email: "p@a.com"
				}
			]
		)

	1. We already have a document with id `1`
		1. One gets inserted
			1. Error: duplicate key
	2. Order is true:
		1. **Order of execution must be in the order of documents specified in the request**

### Class & Lab - Understanding ORDERED | false ###
1. Example:

		db.staff2.insert(
			[
				{
					fname: "Dan222",
					lname: "Wood",
					email: "d@a.com"
				},
				{
					_id: 1,
					fname: "Kate222",
					lname: "Ben",
					email: "k@a.com"
				},
				{
					fname: "Paul222",
					lname: "Cook",
					email: "p@a.com"
				}
			],
			{
				ordered: false
			}
		)

	1. It will jump over the invalid document and processes the third document as well
	2. Execution:
		1. nInserted: 2
		2. errmsg: "... duplicate key..."

## Constructing Documents - More Practice ##
### Class - Understanding Brackets in JSON ###
1. Brackets: `[]`
	1. Use it for group of values or objects
	2. We refer to it as an array
	3. Example:

			names: ["Peter", "James", "Anne"]

2. Braces: `{}`
	1. Must contain: key: value pairs

			people: [
						{ name: "Vic" },
						{ name: "Anthony" },
						{ name: "Mike" }
					]

### Class & Lab - Exercise and Solution - 1 ###
1. Using the table the below construct documents for eachfo the students in MongoDB

		db.examRecord.insert(
			[
				{
					name: "Jessica",
					math: "A",
					science: "B",
					history: "B"	
				},
				{
					name: "Amber",
					math: "C",
					science: "A",
					history: "B"
				}
			]
		)

### CODE: Exercise and Solution - 1 ###
### Class & Lab - Exercise and Solution - 2 ###
1. Example: Peter's city, state, and country are Ajah, Lagos, and Nigeria respectively. The location point coordinates of his address are lat: 6.466667 and lon: 3.566667. If Peter is a student, construct a document for peter in MongoDB

		db.student.insertOne({
			name: "Peter",
			address: {
				city: "Ajah",
				state: "Lagos",
				country: "Nigeria"
			},
			location: {
				type: "point",
				coordinates: {
					lat: 6.466667,
					lon: 3.566667
				}
			}
		})

### CODE: Exercise and Solution - 2 ###
### Class 7 Lab - Exercise and Solution - 3 ###
1. Eric John whose employee ID is 49873 is a developer with ABC Inc. He can program in Java, Python, and Rust. He has three children: Anne, 3; Ben 5, and Victor 8. He recently bought a 2022 white Suzuki Swift (Hatchback). Construct a document in MongoDB for this information.

		db.employee.insert(
			{
				employeeId: 49873,
				firstName: "Eric",
				lastName: "John",
				designation: "developer",
				company: "ABC Inc",
				skills: [
					"Java",
					"Python",
					"Rust"
				],
				children: [
					{
						name: "Anne",
						age: 3
					},
					{
						name: "Ben",
						age: 5
					},
					{
						name: "Victor",
						age: 8
					}
				],
				car: {
					makeYear: 2022,
					color: "white",
					makeModel: "Suzuki Switft",
					type: "hatchback"
				}
			}
		)

### CODE: Exercise and Solution - 3 ###
1. The following are staff in each department of JK Inc. Use `insertMany()` to construct two documents for the departments.
	1. "accounting":
	
			"firstName": "Peter",
			"lastName" : "Ken",
			"age"      : 20

			"firstName": "Jane",
			"lastName": "Vic",
			"age"      : 41

	2. "sales":

			"firstName": "Larry",
			"lastName" : "Stone",
			"age"      : 31

			"firstName": "Eric",
			"lastName" : "Rain",
			"age"      : 52

2. Solution:

		db.department.insertMany([
			{ 
				"accounting": [
					{
						firstName: "Peter",
						lastName: "Ken",
						age: 20	
					},
					{
						firstName: "Jane",
						lastName: "Vic",
						age: 41
					}
				]
			}, 
			{
				"sales": [
					{
						firstName: "Larry",
						lastName: "Stone",
						age: 31
					},
					{
						firstName: "Eric",
						lastName: "Rain",
						age: 52
					}
				]
			}
		])

### Lab - Exercise and Solution - 4 ###
1. A colleague of yours is having problem running the code below. What is wrong with the code? Correct it and construct a document for the event.

		db.reports.insert(
			{
				"Event": {
					"date": "2020-03-12",
					"thread_level_id": "1",
					"info": "testevent",
					"published": false,
					"analysis": false,
					"distribution": "0",
					"Attribute": {
							"type": "domain",
							"category": ""Network activity",
							"to_ids": false,
							"distribution": "0",
							"comment": "kldgljdflsdfdsff",
							"value": "test.com"
					}
				}
			}
		)

### CODE: Exercise and Solution - 4 ###
### Class - Exercise and Solution - 5 ###
### CODE: Exercise and Solution - 5 ###
### Class & Lab - Exercise and Solution - 6 ###
1. Use the information below to construct a document for invoice number 00000200

		db.sales.insert(
		{
			"invoiceNo": "00000200",
			"invoiceDate": "12 March 2022",
			"purchaseOrder": "12345",
			"items":[
				{
					"qty": "1",
					"ItemName": "House",
					"amt": "1000000.00"
				},
				{
					"qty": "2",
					"ItemDescription: "Some old piece of junk",
					"amt": "50.00"
				}
			]
		})			

### CODE: Exercise and Solution - 6

## Sample Documents | Datasets ##
### Lab - Sample Data ###

			db.customers.insert([
		    {
		      "id": "2",
		      "company": "Company B",
		      "last_name": "Gratacos Solsona",
		      "first_name": "Antonio",
		      "email_address": "NULL",
		      "job_title": "Owner",
		      "business_phone": "(123)555-0100",
		      "home_phone": "NULL",
		      "mobile_phone": "NULL",
		      "fax_number": "(123)555-0101",
		      "address": "123 2nd Street",
		      "city": "Boston",
		      "state_province": "MA",
		      "zip_postal_code": "99999",
		      "country_region": "USA",
		      "web_page": "NULL",
		      "notes": "NULL",
		      "attachments": "",
		      "skills": ["Hardware", "Psychologists", "Analysts,", "Meeting,", "Other"],
		      "interests": ["Watching movies", "Videophilia", "Pottery", "Hiking", "Weightlifting"]
		    },
		    {
		      "id": "3",
		      "company": "Company C",
		      "last_name": "Axen",
		      "first_name": "Thomas",
		      "email_address": "NULL",
		      "job_title": "Purchasing Representative",
		      "business_phone": "(123)555-0100",
		      "home_phone": "NULL",
		      "mobile_phone": "NULL",
		      "fax_number": "(123)555-0101",
		      "address": "123 3rd Street",
		      "city": "Los Angelas",
		      "state_province": "CA",
		      "zip_postal_code": "99999",
		      "country_region": "USA",
		      "web_page": "NULL",
		      "notes": "NULL",
		      "attachments": "",
		      "skills": ["Sales", "Specialists", "Craft", "Managers", "Career/Technical"],
			  "interests": ["Hooping", "Microscopy", "Cryptography", "Mahjong", "Rugby league football"]
		    },
		    {
		      "id": "4",
		      "company": "Company D",
		      "last_name": "Lee",
		      "first_name": "Christina",
		      "email_address": "NULL",
		      "job_title": "Purchasing Manager",
		      "business_phone": "(123)555-0100",
		      "home_phone": "NULL",
		      "mobile_phone": "NULL",
		      "fax_number": "(123)555-0101",
		      "address": "123 4th Street",
		      "city": "New York",
		      "state_province": "NY",
		      "zip_postal_code": "99999",
		      "country_region": "USA",
		      "web_page": "NULL",
		      "notes": "NULL",
		      "attachments": "",
		      "skills": ["Architects", "Gaming", "Communications,", "Producers,", "Paralegals"],
		      "interests": ["Coloring", "Dance", "Videophilia", "Book restoration", "Die-cast toy"]
		    },
		    {
		      "id": "5",
		      "company": "Company E",
		      "last_name": "O’Donnell",
		      "first_name": "Martin",
		      "email_address": "NULL",
		      "job_title": "Owner",
		      "business_phone": "(123)555-0100",
		      "home_phone": "NULL",
		      "mobile_phone": "NULL",
		      "fax_number": "(123)555-0101",
		      "address": "123 5th Street",
		      "city": "Minneapolis",
		      "state_province": "MN",
		      "zip_postal_code": "99999",
		      "country_region": "USA",
		      "web_page": "NULL",
		      "notes": "NULL",
		      "attachments": "",
		        "skills": ["Physicists", "Teaching", "Convention", "Displayers", "Drafters,"],
		    "interests": ["Hunting", "Debate", "Table tennis", "Curling", "Skimboarding"]
		    },
		    {
		      "id": "6",
		      "company": "Company F",
		      "last_name": "Pérez-Olaeta",
		      "first_name": "Francisco",
		      "email_address": "NULL",
		      "job_title": "Purchasing Manager",
		      "business_phone": "(123)555-0100",
		      "home_phone": "NULL",
		      "mobile_phone": "NULL",
		      "fax_number": "(123)555-0101",
		      "address": "123 6th Street",
		      "city": "Milwaukee",
		      "state_province": "WI",
		      "zip_postal_code": "99999",
		      "country_region": "USA",
		      "web_page": "NULL",
		      "notes": "NULL",
		      "attachments": "",
		    "skills": ["Family", "Farmers,", "Fashion", "Interior", "Operators,"],
		    "interests": ["Leather crafting", "Brazilian jiu-jitsu", "Motor sports", "Exhibition drill", "Hunting"]
		    },
		    {
		      "id": "7",
		      "company": "Company G",
		      "last_name": "Xie",
		      "first_name": "Ming-Yang",
		      "email_address": "NULL",
		      "job_title": "Owner",
		      "business_phone": "(123)555-0100",
		      "home_phone": "NULL",
		      "mobile_phone": "NULL",
		      "fax_number": "(123)555-0101",
		      "address": "123 7th Street",
		      "city": "Boise",
		      "state_province": "ID",
		      "zip_postal_code": "99999",
		      "country_region": "USA",
		      "web_page": "NULL",
		      "notes": "NULL",
		      "attachments": "",
		    "skills": ["Cartographers", "Administrative", "Occupations,", "Museum", "Management"],
		    "interests": ["Sudoku", "Board games", "Baseball", "Mushroom hunting/Mycology", "Drama"]
		    },
		    {
		      "id": "8",
		      "company": "Company H",
		      "last_name": "Andersen",
		      "first_name": "Elizabeth",
		      "email_address": "NULL",
		      "job_title": "Purchasing Representative",
		      "business_phone": "(123)555-0100",
		      "home_phone": "NULL",
		      "mobile_phone": "NULL",
		      "fax_number": "(123)555-0101",
		      "address": "123 8th Street",
		      "city": "Portland",
		      "state_province": "OR",
		      "zip_postal_code": "99999",
		      "country_region": "USA",
		      "web_page": "NULL",
		      "notes": "NULL",
		      "attachments": "",
		    "skills": ["Fashion", "Historians", "Administrative", "Information", "Chief"],
		    "interests": ["Drawing", "Flag Football", "Fishing", "Cricket", "Birdwatching"]
		    },
		    {
		      "id": "9",
		      "company": "Company I",
		      "last_name": "Mortensen",
		      "first_name": "Sven",
		      "email_address": "NULL",
		      "job_title": "Purchasing Manager",
		      "business_phone": "(123)555-0100",
		      "home_phone": "NULL",
		      "mobile_phone": "NULL",
		      "fax_number": "(123)555-0101",
		      "address": "123 9th Street",
		      "city": "Salt Lake City",
		      "state_province": "UT",
		      "zip_postal_code": "99999",
		      "country_region": "USA",
		      "web_page": "NULL",
		      "notes": "NULL",
		      "attachments": "",
		    "skills": ["Graduate", "Postsecondary", "Drama", "Information", "Judges,"],
		    "interests": ["Poker", "Gardening", "Action figure", "Drama", "Seashell collecting"]
		    },
		    {
		      "id": "10",
		      "company": "Company J",
		      "last_name": "Wacker",
		      "first_name": "Roland",
		      "email_address": "NULL",
		      "job_title": "Purchasing Manager",
		      "business_phone": "(123)555-0100",
		      "home_phone": "NULL",
		      "mobile_phone": "NULL",
		      "fax_number": "(123)555-0101",
		      "address": "123 10th Street",
		      "city": "Chicago",
		      "state_province": "IL",
		      "zip_postal_code": "99999",
		      "country_region": "USA",
		      "web_page": "NULL",
		      "notes": "NULL",
		      "attachments": "",
		    "skills": ["Radio", "Coordinators", "Referees", "Kindergarten", "Geography"],
		    "interests": ["Microscopy", "Rugby league football", "Table football", "Backpacking", "Sculpting"]
		    },
		    {
		      "id": "11",
		      "company": "Company K",
		      "last_name": "Krschne",
		      "first_name": "Peter",
		      "email_address": "NULL",
		      "job_title": "Purchasing Manager",
		      "business_phone": "(123)555-0100",
		      "home_phone": "NULL",
		      "mobile_phone": "NULL",
		      "fax_number": "(123)555-0101",
		      "address": "123 11th Street",
		      "city": "Miami",
		      "state_province": "FL",
		      "zip_postal_code": "99999",
		      "country_region": "USA",
		      "web_page": "NULL",
		      "notes": "NULL",
		      "attachments": "",
		    "skills": ["Appraisers", "Probation", "Geoscientists,", "Geological", "Educational,"],
		    "interests": ["Scrapbooking", "Flying disc", "Sports", "Cheerleading", "Amateur radio"]
		    },
		    {
		      "id": "12",
		      "company": "Company L",
		      "last_name": "Edwards",
		      "first_name": "John",
		      "email_address": "NULL",
		      "job_title": "Purchasing Manager",
		      "business_phone": "(123)555-0100",
		      "home_phone": "NULL",
		      "mobile_phone": "NULL",
		      "fax_number": "(123)555-0101",
		      "address": "123 12th Street",
		      "city": "Las Vegas",
		      "state_province": "NV",
		      "zip_postal_code": "99999",
		      "country_region": "USA",
		      "web_page": "NULL",
		      "notes": "NULL",
		      "attachments": "",
		    "skills": ["Dancers", "Ethnic", "Architects,", "Electrical", "Specialties"],
		    "interests": ["Kart racing", "Reading", "Crocheting", "Action figure", "Shortwave listening"]
		    },
		    {
		      "id": "13",
		      "company": "Company M",
		      "last_name": "Ludick",
		      "first_name": "Andre",
		      "email_address": "NULL",
		      "job_title": "Purchasing Representative",
		      "business_phone": "(123)555-0100",
		      "home_phone": "NULL",
		      "mobile_phone": "NULL",
		      "fax_number": "(123)555-0101",
		      "address": "456 13th Street",
		      "city": "Memphis",
		      "state_province": "TN",
		      "zip_postal_code": "99999",
		      "country_region": "USA",
		      "web_page": "NULL",
		      "notes": "NULL",
		      "attachments": "",
		    "skills": ["Services", "Emergency", "Chemical", "Career/Technical", "Historians"],
		    "interests": ["Aqua-lung", "Acting", "Baseball", "Sudoku", "Stand-up comedy"]
		    },
		    {
		      "id": "14",
		      "company": "Company N",
		      "last_name": "Grilo",
		      "first_name": "Carlos",
		      "email_address": "NULL",
		      "job_title": "Purchasing Representative",
		      "business_phone": "(123)555-0100",
		      "home_phone": "NULL",
		      "mobile_phone": "NULL",
		      "fax_number": "(123)555-0101",
		      "address": "456 14th Street",
		      "city": "Denver",
		      "state_province": "CO",
		      "zip_postal_code": "99999",
		      "country_region": "USA",
		      "web_page": "NULL",
		      "notes": "NULL",
		      "attachments": "",
		    "skills": ["Financial", "Examiners", "Landscape", "Aerospace", "Museum"],
		    "interests": ["Tennis", "Rugby league football", "Fashion", "Action figure", "Lacrosse"]
		    },
		    {
		      "id": "15",
		      "company": "Company O",
		      "last_name": "Kupkova",
		      "first_name": "Helena",
		      "email_address": "NULL",
		      "job_title": "Purchasing Manager",
		      "business_phone": "(123)555-0100",
		      "home_phone": "NULL",
		      "mobile_phone": "NULL",
		      "fax_number": "(123)555-0101",
		      "address": "456 15th Street",
		      "city": "Honolulu",
		      "state_province": "HI",
		      "zip_postal_code": "99999",
		      "country_region": "USA",
		      "web_page": "NULL",
		      "notes": "NULL",
		      "attachments": "",
		    "skills": ["Business", "Atmospheric", "Choreographers", "Teaching", "Philosophy"],
		    "interests": ["Roller skating", "Playing musical instruments", "Aircraft spotting", "Skateboarding", "Jukskei"]
		    },
		    {
		      "id": "16",
		      "company": "Company P",
		      "last_name": "Goldschmidt",
		      "first_name": "Daniel",
		      "email_address": "NULL",
		      "job_title": "Purchasing Representative",
		      "business_phone": "(123)555-0100",
		      "home_phone": "NULL",
		      "mobile_phone": "NULL",
		      "fax_number": "(123)555-0101",
		      "address": "456 16th Street",
		      "city": "San Francisco",
		      "state_province": "CA",
		      "zip_postal_code": "99999",
		      "country_region": "USA",
		      "web_page": "NULL",
		      "notes": "NULL",
		      "attachments": "",
		    "skills": ["Court", "Architects", "Athletes,", "Geography", "Kindergarten"],
		    "interests": ["Hooping", "Hooping", "Scrapbooking", "Roller skating", "Origami"]
		    },
		    {
		      "id": "17",
		      "company": "Company Q",
		      "last_name": "Bagel",
		      "first_name": "Jean Philippe",
		      "email_address": "NULL",
		      "job_title": "Owner",
		      "business_phone": "(123)555-0100",
		      "home_phone": "NULL",
		      "mobile_phone": "NULL",
		      "fax_number": "(123)555-0101",
		      "address": "456 17th Street",
		      "city": "Seattle",
		      "state_province": "WA",
		      "zip_postal_code": "99999",
		      "country_region": "USA",
		      "web_page": "NULL",
		      "notes": "NULL",
		      "attachments": "",
		    "skills": ["Clergy", "Database", "Cartographers", "Health", "Workers"],
		    "interests": ["Computer programming", "Mushroom hunting/Mycology", "Beekeeping", "Writing", "Tennis"]
		    },
		    {
		      "id": "18",
		      "company": "Company R",
		      "last_name": "Autier Miconi",
		      "first_name": "Catherine",
		      "email_address": "NULL",
		      "job_title": "Purchasing Representative",
		      "business_phone": "(123)555-0100",
		      "home_phone": "NULL",
		      "mobile_phone": "NULL",
		      "fax_number": "(123)555-0101",
		      "address": "456 18th Street",
		      "city": "Boston",
		      "state_province": "MA",
		      "zip_postal_code": "99999",
		      "country_region": "USA",
		      "web_page": "NULL",
		      "notes": "NULL",
		      "attachments": "",
		    "skills": ["Substitute", "Designers", "Geography", "Database", "Cartographers"],
		    "interests": ["Kart racing", "Ice skating", "Swimming", "Handball", "Taekwondo"]
		    },
		    {
		      "id": "19",
		      "company": "Company S",
		      "last_name": "Eggerer",
		      "first_name": "Alexander",
		      "email_address": "NULL",
		      "job_title": "Accounting Assistant",
		      "business_phone": "(123)555-0100",
		      "home_phone": "NULL",
		      "mobile_phone": "NULL",
		      "fax_number": "(123)555-0101",
		      "address": "789 19th Street",
		      "city": "Los Angelas",
		      "state_province": "CA",
		      "zip_postal_code": "99999",
		      "country_region": "USA",
		      "web_page": "NULL",
		      "notes": "NULL",
		      "attachments": "",
		    "skills": ["Actuaries", "Foreign", "Teaching", "Technical", "Architects"],
		    "interests": ["Cheerleading", "Knife making", "Scouting", "Surfing", "Squash"]
		    },
		    {
		      "id": "20",
		      "company": "Company T",
		      "last_name": "Li",
		      "first_name": "George",
		      "email_address": "NULL",
		      "job_title": "Purchasing Manager",
		      "business_phone": "(123)555-0100",
		      "home_phone": "NULL",
		      "mobile_phone": "NULL",
		      "fax_number": "(123)555-0101",
		      "address": "789 20th Street",
		      "city": "New York",
		      "state_province": "NY",
		      "zip_postal_code": "99999",
		      "country_region": "USA",
		      "web_page": "NULL",
		      "notes": "NULL",
		      "attachments": "",
		    "skills": ["Occupations", "Archivists", "Researchers", "Geographers", "Library"],
		    "interests": ["Speed skating", "Kabaddi", "Rugby", "Graffiti", "Drama"]
		    },
		    {
		      "id": "21",
		      "company": "Company U",
		      "last_name": "Tham",
		      "first_name": "Bernard",
		      "email_address": "NULL",
		      "job_title": "Accounting Manager",
		      "business_phone": "(123)555-0100",
		      "home_phone": "NULL",
		      "mobile_phone": "NULL",
		      "fax_number": "(123)555-0101",
		      "address": "789 21th Street",
		      "city": "Minneapolis",
		      "state_province": "MN",
		      "zip_postal_code": "99999",
		      "country_region": "USA",
		      "web_page": "NULL",
		      "notes": "NULL",
		      "attachments": "",
		    "skills": ["Compliance", "Physical", "Postsecondary", "Geographers", "Science"],
		    "interests": ["Snowboarding", "Sculpting", "Antiquing", "Bus spotting", "LARPing"]
		    },
		    {
		      "id": "22",
		      "company": "Company V",
		      "last_name": "Ramos",
		      "first_name": "Luciana",
		      "email_address": "NULL",
		      "job_title": "Purchasing Assistant",
		      "business_phone": "(123)555-0100",
		      "home_phone": "NULL",
		      "mobile_phone": "NULL",
		      "fax_number": "(123)555-0101",
		      "address": "789 22th Street",
		      "city": "Milwaukee",
		      "state_province": "WI",
		      "zip_postal_code": "99999",
		      "country_region": "USA",
		      "web_page": "NULL",
		      "notes": "NULL",
		      "attachments": "",
		    "skills": ["Marriage", "Management", "Drafters", "Management", "Foreign"],
		    "interests": ["Australian rules football", "Foraging", "Chess", "Sketching", "Couponing"]
		    },
		    {
		      "id": "23",
		      "company": "Company W",
		      "last_name": "Entin",
		      "first_name": "Michael",
		      "email_address": "NULL",
		      "job_title": "Purchasing Manager",
		      "business_phone": "(123)555-0100",
		      "home_phone": "NULL",
		      "mobile_phone": "NULL",
		      "fax_number": "(123)555-0101",
		      "address": "789 23th Street",
		      "city": "Portland",
		      "state_province": "OR",
		      "zip_postal_code": "99999",
		      "country_region": "USA",
		      "web_page": "NULL",
		      "notes": "NULL",
		      "attachments": "",
		    "skills": ["Teachers", "Forensic", "Civil", "Gaming", "Physical"],
		    "interests": ["Flower collecting and pressing", "Backpacking", "Gaming (tabletop games and role-playing games)", "Breakdancing", "Paintball"]
		    },
		    {
		      "id": "24",
		      "company": "Company X",
		      "last_name": "Hasselberg",
		      "first_name": "Jonas",
		      "email_address": "NULL",
		      "job_title": "Owner",
		      "business_phone": "(123)555-0100",
		      "home_phone": "NULL",
		      "mobile_phone": "NULL",
		      "fax_number": "(123)555-0101",
		      "address": "789 24th Street",
		      "city": "Salt Lake City",
		      "state_province": "UT",
		      "zip_postal_code": "99999",
		      "country_region": "USA",
		      "web_page": "NULL",
		      "notes": "NULL",
		      "attachments": "",
		    "skills": ["Adult", "Coordinators", "Workers", "Court", "Psychology"],
		    "interests": ["Creative writing", "Lacrosse", "Element collecting", "Photography", "Creative writing"]
		    },
		    {
		      "id": "25",
		      "company": "Company Y",
		      "last_name": "Rodman",
		      "first_name": "John",
		      "email_address": "NULL",
		      "job_title": "Purchasing Manager",
		      "business_phone": "(123)555-0100",
		      "home_phone": "NULL",
		      "mobile_phone": "NULL",
		      "fax_number": "(123)555-0101",
		      "address": "789 25th Street",
		      "city": "Chicago",
		      "state_province": "IL",
		      "zip_postal_code": "99999",
		      "country_region": "USA",
		      "web_page": "NULL",
		      "notes": "NULL",
		      "attachments": "",
		    "skills": ["Interior", "Animal", "Surveying", "Agricultural", "Occupations"],
		    "interests": ["Gardening", "Golfing", "Knitting", "Bowling", "Urban exploration"]
		    },
		    {
		      "id": "26",
		      "company": "Company Z",
		      "last_name": "Liu",
		      "first_name": "Run",
		      "email_address": "NULL",
		      "job_title": "Accounting Assistant",
		      "business_phone": "(123)555-0100",
		      "home_phone": "NULL",
		      "mobile_phone": "NULL",
		      "fax_number": "(123)555-0101",
		      "address": "789 26th Street",
		      "city": "Miami",
		      "state_province": "FL",
		      "zip_postal_code": "99999",
		      "country_region": "USA",
		      "web_page": "NULL",
		      "notes": "NULL",
		      "attachments": "",
		    "skills": ["Dancers", "Public", "Except", "Economists", "Property"],
		    "interests": ["American football", "Table tennis", "Writing", "Coin collecting", "Squash"]
		    },
		    {
		      "id": "27",
		      "company": "Company AA",
		      "last_name": "Toh",
		      "first_name": "Karen",
		      "email_address": "NULL",
		      "job_title": "Purchasing Manager",
		      "business_phone": "(123)555-0100",
		      "home_phone": "NULL",
		      "mobile_phone": "NULL",
		      "fax_number": "(123)555-0101",
		      "address": "789 27th Street",
		      "city": "Las Vegas",
		      "state_province": "NV",
		      "zip_postal_code": "99999",
		      "country_region": "USA",
		      "web_page": "NULL",
		      "notes": "NULL",
		      "attachments": "",
		    "skills": ["Executives", "Occupations", "Education,", "Marine", "Conservation"],
		    "interests": ["Antiquing", "Driving", "Glassblowing", "Sculling or Rowing", "Auto racing"]
		    },
		    {
		      "id": "28",
		      "company": "Company BB",
		      "last_name": "Raghav",
		      "first_name": "Amritansh",
		      "email_address": "NULL",
		      "job_title": "Purchasing Manager",
		      "business_phone": "(123)555-0100",
		      "home_phone": "NULL",
		      "mobile_phone": "NULL",
		      "fax_number": "(123)555-0101",
		      "address": "789 28th Street",
		      "city": "Memphis",
		      "state_province": "TN",
		      "zip_postal_code": "99999",
		      "country_region": "USA",
		      "web_page": "NULL",
		      "notes": "NULL",
		      "attachments": "",
		    "skills": ["Education", "Zoologists", "Statisticians", "Dancers", "Cartographers"],
		    "interests": ["Seashell collecting", "Lacemaking", "Card collecting", "Mahjong", "Table tennis"]
		    },
		    {
		      "id": "29",
		      "company": "Company CC",
		      "last_name": "Lee",
		      "first_name": "Soo Jung",
		      "email_address": "NULL",
		      "job_title": "Purchasing Manager",
		      "business_phone": "(123)555-0100",
		      "home_phone": "NULL",
		      "mobile_phone": "NULL",
		      "fax_number": "(123)555-0101",
		      "address": "789 29th Street",
		      "city": "Denver",
		      "state_province": "CO",
		      "zip_postal_code": "99999",
		      "country_region": "USA",
		      "web_page": "NULL",
		      "notes": "NULL",
		      "attachments": "",
		    "skills": ["Meeting", "Wholesale", "Business", "Child,", "Legislators"],
		    "interests": ["Creative writing", "Field hockey", "Worldbuilding", "BASE jumping", "Worldbuilding"]
		    }	
		  ]
		)

### CODE: Sample Data (Customers) ###
### CODE: Sample Data (Food) ###

		db.foods.insert(
			{
				"id": "0001",
				"type": "donut",
				"name": "Cake",
				"ppu": 0.55,
				"batters":
				{
					"batter":
					[
						{ "id": "1001", "type": "Regular" },
						{ "id": "1002", "type": "Chocolate" },
						{ "id": "1003", "type": "Blueberry" },
						{ "id": "1004", "type": "Whiteberry" }
					]
				},
				"topping":
				[
					{ "id": "5001", "type": "None" },
					{ "id": "5002", "type": "Glazed" },
					{ "id": "5005", "type": "Sugar" },
					{ "id": "5007", "type": "Powdered Sugar" },
					{ "id": "5006", "type": "Chocolate with Sprinkles" },
					{ "id": "5003", "type": "Chocolate" },
					{ "id": "5004", "type": "Maple" }
				]
			}
		)

### CODE: Sample Data (Product_Suppliers) ###

		db.products_suppliers.insert([
			{
				"apple": {
					"suppliers": [
						{"name":"Dan Cain", "phone":"0125412"},
						{"name":"Ruth Ike", "phone":"0125745"}
					],
					"shipper": {"name":"National Express"}
				}
			}, 
			{
				"mango": {
					"suppliers": [
						{"name":"Steve Bright", "phone":"01412457"},
						{"name":"Gate Matt", "phone":"01415474"}
					],
					"shipper": {"name": "Federal Express"}
				}
			}
		])

### Lab - Importing CSV File to MongoDB Using Compass ###
1. Import csv file in Compas:
	1. Click: Create database: tutData
	2. Click: Create collection: sales
	3. Click: Import data
		1. CSV
		2. Import

### CODE: Importing CSV File to MongoDB Using Compass ###
### Lab - Converting String to Double ###
1. To change data-type:
	1. Go to right and change for each document
2. Through code:

		db.sales.find().forEach(d => {
				d['unitPrice'] = parseFloat(d['unitPrice']);
				db.sales.save(d);
			})

### CODE: Converting String to Double ###

## Finding One Document ##
### Class & Lab - Understanding findOne() ###
1. How to search for documents in a collection (one or more documents)
2. Two methods:
	1. `findOne()` **(M)**
		1. Just one
	2. `find()` **(M)**
		1. One or many
3. `findOne()`:
	1. Syntax:

			db.<collection>.findOne(query, projection) **(M)**

		1. Just first document:

				db.<collection>.findOne() # gives the first document in the collection

	2. Example:

			db.exam.findOne() # first document

	3. `query` - filter
		1. Example:

				db.exams.findOne({name: "Geoff"}) # finds first match
				# Even if there are multiple that matched

				db.exams.find({Math: "C"}) # finds all that match

### CODE: Understanding findOne() ###

		db.exam.insert(
			[
				{
					name:"Jessica",
					Math:"A",
					Science:"B",
					History:"B"
				},
				{
					name:"Amber",	
					Math:"C",
					Science:"A",
					History:"B"
				},
				{
					name:"Lauren",	
					Math:"B",
					Science:"C",
					History:"A"
				},
				{
					name:"Geoff",	
					Math:"C",
					Science:"A",
					History:"B"
				},
				{
					name:"Caleb",	
					Math:"B",
					Science:"B",
					History:"B"
				}
			]
		)

### Class & Lab - No Match ###
1. Returns `null` if there is no match

### Class & Lab - Query Operators ###
1. `db.exam.findOne({price: {$gt: 200}})`
	1. First document that the criterion
	2. Example:

			db.sales.findOne({unitPrice: {$gt: 18}})
			db.sales.findOne({unitPrice: {$lt: 18}})
			db.sales.findOne({unitPrice: {$lt: 5, $gt: 18}})

### Lab - Exercise and Solution I ###

		db.customers.findOne({city: "Las Vegas"})

### CODE - Exercise and Solution I ###
### Lab - Exercise and Solution II ###
	
		db.sales.findOne({unitPrice: {$eq: 40}})
		db.sales.findOne({unitPrice: {$gt: 18}})

### CODE - Exercise and Solution II ###

## Projection ##
### Class & Lab - Understanding Projection ###
1. 

### CODE: Understanding Projection ###
### Lab - Exercise and Solution I ###
### CODE: Exercise and Solution I ###
### Lab - Exercise and Solution II ###
### CODE: Exercise and Solution II ###

## Finding Multiple Documents ##
### Class & Lab - Understanding find() ###
### CODE: Understanding find() ###
### Class & Lab - Query Operators with find() ###
### CODE: Query Operators with find() ###
### Class - Projection with find() ###
### Class & Lab - Embedded Documents ###
### CODE: Embedded Documents - Dataset ###
### Class & Lab - Querying Array Elements ###
### CODE: Querying Array Elements ###
### Class & Lab - Querying Array Elements with IN, ALL and SIZE ###
### CODE: Querying Array Elements with IN, ALL and SIZE ###
### Exercise 1 ###
### CODE: Exercise 1 Solution ###
### Exercise 2 ###
### CODE: Exercise 2 Solution ###
### Exercise 3 ###
### CODE: Exercise 3 Solution ###

## updateOne() ##
### Class & Lab - Understanding updateOne() ###
### CODE: Understanding updateOne() ###
### Class & Lab - updateOne() by Example ###
### CODE: updateOne() by Example ###
### Class & Lab - Multiple Fields Update ###
### Code: Multiple Fields Update ###
### Class & Lab - Options in updateOne() ###
### CODE: Options in updateOne() ###
### Class & Lab - Update Operators - $set | $inc | $min | $max | $rename | $mul ... ###
### CODE: Update Operators - $set | $inc | $min | $max | $rename | $mul | $unset ###

## updateMany() and update() ##
### Lab - World Cities Dataset ###
### CODE: World Cities Dataset ###
### Lab - USA Cities Dataset ###
### CODE: USA Cities Dataset ###
### Class - Understanding How to Update Multiple Documents ###
### Class - Understanding updateMany() and update() ###
### Lab - Exercise and Solution - ($unset | $multi) - updateMany() ###
### CODE: Exercise and Solution - ($unset | $multi) - updateMany() ###
### Lab - Exercise and Solution - ($set | $multi) - updateMany() ###
### CODE: Exercise and Solution - ($set | $multi) - updateMany() ###
### Lab - Exercise and Solution - ($mul) - updateMany() ###
### CODE: Exercise and Solution - ($mul) - updateMany() ###
### Lab - Exercise and Solution - ($min) - update() ###
### CODE: Exercise and Solution - ($min) - update() ###
### Lab - Exercise and Solution - ($rename) ###
### CODE: Exercise and Solution - ($rename) ###

## setOnInsert() vs set() ##
### Class & Lab - Understanding the Difference Between setOnInsert() and set() - I ###
### CODE: Understanding the Difference Between setOnInsert() and set() - I ###
### Class & Lab - Understanding the Difference Between setOnInsert() and set() - II ###
### CODE: Understanding the Difference Between setOnInsert() and set() - II ###
### Class & Lab - Understanding the Differnce Between setOnInsert() and set() - III ###
### CODE: Understanding the Difference Between setOnInsert() and set() - III ###
### Class & Lab - Understanding the Difference Between setOnInsert() and set() - IV ###
### CODE: Understanding the Difference Between setOnInsert() and set() - IV ###

## Deleting Documents ##
### Class - Introduction to Deleting Documents ###
### Class - deleteOne() ###
### Lab - deleteOne() ###
### CODE: deleteOne() ###
### Class - remove() ###
### Lab - Exercise and Solution - remove() - I ###
### CODE: Exercise and Solution - remove() - I ###
### Lab - Exercise and Solution - remove() - II ###
### CODE: Exercise and Solution - remove() - II ###
### Class - Exercise and Solution - justOne() ### 
### CODE: Exercise and Solution - justOne() ###
### Class - deleteMany() ###
### Lab - Exercise and Solution - deleteMany() ###
### CODE: Exercise and Solution - deleteMany() ###

## Limit and Skip ##
### Understanding Limit ###
### Lab - Understanding Limit ###
### CODE: Understanding Limit ###
### Lab - Understanding Skip ###
### CODE: Understanding Skip ###
### Class - Combining Limit and Skip ###
### Lab - Combining Limit and Skip ###
### CODE: Combining Limit and Skip II ###

## sort() ##
### Class - Understanding sort() ###
### Lab - Understanding sort() ###
### CODE: Understanding sort() II ###

## Indexes ##
### Class - Understanding Indexes ###
### Lab - How to Construct Indexes ###
### CODE: How to Construct Indexes ###
### Class - OPTIONS in createIndex() ###
### Lab - Unique Index ###
### CODE - How to Construct Indexes ###
### Class - OPTIONS in createIndex() ###
### Lab - Unique Index ###
### CODE: Unique Index ###
### Class & Lab - Compound Fields Indexing ###
### CODE: Compound Fields Indexing ###
### Lab - Multi-Key Index ###
### Code: Multi-Key Index ###
### Class & Lab - Listing Indexes ###
### Code: Listing Indexes ###
### Class - Deleting Indexes ###
### Lab - Deleting Indexes - Example 1 ###
### Code: Deleting Indexes - Example 1 ###
### Lab - Deleting Indexes - Example 2 ###
### Code - Deleting Indexes - Example 2 ###

## Mongo DB Operator Types in General ##
### Class - MongoDB Operator Types in General ###

## Comparison Operators | $gt, $lt, $gte, $lte, $eq, $in, $ne ##
### Class - Understanding Comparison Operators ###
### Lab - Documents Dataset for Practice ###
### CODE: Documents for Practice ###
### Lab - $gt - Exercise and Solution 1 ###
### CODE: $gt - Exercise and Solution 1 ###
### Lab - $gt - Exercise and Solution 2 ###
### CODE: $gt - Exercise and Solution 2 ###
### Lab - $lt - Exercise and Solution 1 ###
### CODE: $lt - Exercise and Solution 1 ###
### Lab - $lt - Exercise and Solution 2 ###
### CODE: $lt - Exercise and Solution 2 ###
### Lab - $eq - Exercise and Solution ###
### $eq - Exercise and Solution - CODE ###
### Lab - $gte - Exercise and Solution ###
### CODE: $get - Exercise and Solution ###
### Lab - $lte - Exercise and Solution ###
### CODE: $lte - Exercise and Solution ###
### Lab - $in - Exercise and Solution 1 ###
### CODE: $in - Exercise and Solution 1 ###
### Lab - $in - Exercise and Solution 2 ###
### CODE: $in - Exercise and Solution 2 ###
### Class - $nin - Exercise and Solution ###
### CODE: $nin - Exercise and Solution ###
### Lab - $ne - Exercise and Solution ###
### CODE: $ne - Exercise and Solution ###

## Logical Operators | $and, $or, $nor, $not ##
### Class - Understanding Logical Operators ###
### Class - Secret to Writing Effective Query ###
### Lab - $and - Exercise and Solution 1 ###
### CODE: $and - Exercise and Solution 1 ###
### Lab - $and - Exercise and Solution 2 ###
### CODE: $and - Exercise and Solution 2 ###
### Lab - $or - Exercise and Solution 1 ###
### CODE: $or - Exercise and Solution 1 ###
### Lab - $or - Exercise and Solution 2 ###
### CODE: $or - Exercise and Solution 2 ###
### Lab - $nor - Exercise and Solution ###
### CODE: $nor - Exercise and Solution ###
### Lab - $not - Exercise and Solution ###
### CODE: $not - Exercise and Solution ###

## Element Operators | $exist, $type ##
### Class - Understanding the Element Operators ###
### Lab - $exists - Exercise and Solutions 1 ###
### CODE: $exists - Exercise and Solutions 1 ###
### Lab - $exists - Exercise and Solutions 2 ###
### $exists - Exercise and Solution 2 - CODE ###
### Lab - $exists - Exercise and Solutions 3 ###
### CODE: $exists - Exercise and Solutions 3 ###
### Lab - $exists - Exercise and Solutions 4 ###
### CODE: $exists - Exercise and Solutions 4 ###
### Lab - $type - Exercise and Solutions 1 ###
### CODE: $type - Exercise and Solutions 1 ###
### Lab - $type - Exercise and Solutions 2 ###
### CODE: $type - Exercise and Solutions 2 ###
### Lab - $type - Exercise and Solutions 3 ###
### CODE: $type - Exercise and Solutions 3 ###

## Evaluation Operators | $mod, $text, $language, $caseSensitive, $diacriticSensitive ##
### Class - Understanding the Evaluation Operators ###
### Lab - Dataset ###
### CODE: Dataset ###
### Lab - $mod - Syntax with an Example ###
### CODE: $mod - Syntax with an Example ###
### Lab - $mod - Possible Errors ###
### Lab: $mode - Floating Points Arguments ###
### CODE: $mod - Floating Points Arguments ###
### Lab - $mod - Exercise and Solution ###
### CODE: $mod - Exercise and Solution ###
### Lab - $text - Understanding the $text Operator ###
### Lab: $text - Searching for a Single Word ###
### CODE: $text - Searching for a Single Word ###
### Lab - $text - Searching for Different Words ###
### CODE: $text - Searching for Different Words ###
### Lab - $text - Searching for a Phrase ###
### CODE: $text - Searching for a Phrase ###
### Lab - $text - Exclude Documents That Contain a Term ###
### CODE: $text - Exclude Documents That Contain a Term ###
### Lab - $text - $caseSensitive ###
### CODE: $text - $caseSensitive ###
### Lab - $text - $diacriticSensitive ###
### CODE: $text - $diacriticSensitive ###
### Lab - $text - $search | Search Score ###
### CODE: $text - $search | Search Score ###
### Lab - $text - Sorting ###
### CODE: $text - Sorting ###
### Lab - $text - Score & Sort ###
### CODE: $text - Score & Sort ###
### Lab - $text - Score & Sort II ###
### CODE: $text - Score & Sort II ###

## Regular Expression (Regex) ##
### Class - Understanding Regular Expression ###
### Lab - Understanding Regular Expression ###
### CODE: Dataset ###
### CODE: Understanding Regular Expression ###
### Class - Anchors ###
### Lab - Hands-on | Anchors ###
### CODE: Hands-on | Anchors ###
### Class - Quantifier ###
### Lab - Quantifier ###
### CODE: Quantifier ###
### Class - Group Range ###
### Lab - Group Range ###
### CODE: Group Range ###
### Class - Common MetaCharacters ###
### Lab - Common MetaCharacters ###
### CODE: Common MetaCharacters ###
### Class - Character Classes ###
### Lab -Character Classes ###
### CODE: Character Classes ###
### Class - Options ###
### Lab - Options ###
### CODE: Options ###

## GeoSpatial in MongoDB | $geoIntersects, $geoWithin, $centreSpere, $near, $box ##
### Class - Introduction to GeoSpatial ###
### Class - Geometry Types ###
### Class - GeoSpatial Syntax ###
### Class - GeoSpatial Operators ###
### Lab - Insertin GeoSpatial Data - Example I ###
### Code: Inserting GeoSpatial Data - Example I ###
### Lab - Inserting GeoSpatial Data - Example II ###
### CODE: Inserting GeoSpatial Data - Example II ###
### Lab - Inserting GeoSpatial Data - Example III ###
### CODE: Inserting GeoSpatial Data - Example III ###
### Lab - Importing Restaurants & Neighbourhoods GeoJSON Data via Compass ###
### CODE: Restaurants.JSON File ###
### CODE: Neighbourhoods.JSON File ###
### Lab - Importing Restaurants & Neighbourhoods GeoJSON Data via Terminal ###
### CODE: Importing Restaurants & Neighbourhoods GeoJSON Data via Terminal ###
### Lab - Ways of Constructing Index on Document of GeoSpatial Data ###
### CODE: Ways of Constructing Index on Document of GeoSpatial Data ###
### Lab - Querying GeoSpatial Data Without Index ###
### CODE: Querying GeoSpatial Data Without Index ###
### Lab - Querying GeoSpatial Data With Index ###
### CODE: Querying GeoSpatial Data With Index ###
### Lab - $nearSphere - Exercise and Solution ###
### CODE: $nearSphere - Exercise and Solution ###
### Lab - $geoIntersects - Exercise and Solution ###
### CODE: $geoIntersects - Exercise and Solution ###
### Lab - $geoWithin - Exercise and Solution ###
### CODE: $geoWithin - Exercise and Solution ###
### Lab - $centerSphere with $geoWithin - Exercise & Solution ###
### CODE: $centerSphere with $geoWithin - Exercise & Solution ###
### Lab - $near - Exercise and Solution ###
### CODE: $near - Exercise and Solution ###
### Lab - $box with $geoWithin - Exercise and Solution ###
### CODE: $box with $geoWithin - Exercise and Solution ###

## MongoDB Cursor | next(), forEach(), hasNext(), isExhausted(), map(), toArray() ##
### Class - Understanding MongoDB Cursor ###
### Class - Cursor Methods ###
### Lab - next() - Exercise and Solution I ###
### CODE: next() - Exercise and Solution I ###
### lab - next() - Exercise and Solution II ###
### CODE: next() - Exercise and Solution II ###
### Lab - count() ###
### CODE: count() ###
### Lab - itcount() ###
### Lab - forEach() ###
### CODE: forEach() ###
### Lab - hasNext() ###
### CODE: hasNext() ###
### Lab - isExhausted() ###
### CODE: isExhausted() ###
### Lab - limmit(), skip(), sort() ###
### CODE: limit(), skip(), sort() ###
### Lab - map() ###
### CODE: map() ###
### Lab - toArray() ###
### CODE: toArray() ###
### Lab - size() ###
### CODE: size() ###
### Lab - objsLeftInBatch() ###
### CODE: objsLeftInBatch() ###

## Aggregation in MongoDB ##
### Class - Understanding Aggregation in MongoDB ###
### Class - Manual Aggregation ###
### Class - Syntax ###
### Class - Stages, Expression, and Accumulators ###
### CODE: Dataset ###
### Class & Lab - Aggregation Example I ###
### CODE: Aggregation Example I ###
### Class & Lab - Aggregation Example II ###
### CODE: Aggregation Example II ###
### Class & Lab - Aggregation Example III ###
### CODE: Aggregation Example III ###
### Class & Lab - Aggregation Example IV ###
### CODE: Aggregation Example IV ###
### Class - Comparing SQL and MongoDB Clauses/Operating ###

## $match - Exercises and Solutions ##
### Lab - $match - Exercise and Solution I ###
### CODE: $match - Exercise and Solution I ###
### Lab - $match - Exercise and Solution II ###
### CODE: $match - Exercise and Solution II ###
### Lab - $match - Exercise and Solution III ###
### CODE: $match - Exercise and Solution III ###
### Lab - $match - Exercise and Solution IV ###
### CODE: $match - Exercise and Solution IV ###
### Lab - $match - Exercise and Solution V ###
### CODE: $match - Exercise and Solution V ###

## $project - Exercises and Solutions ##
### Lab - $project - Exercise and Solution I ###
### CODE: $project - Exercise and Solution I ###
### Lab - $project - Exercise and Solution II ###
### CODE: $project - Exercise and Solution II ###
### Lab - $project - Exercise and Solution III ###
### CODE: $project - Exercise and Solution III ###

## $group Exercises and Solutions ##
### Lab - $group - Exercise and Solution I ###
### CODE: $group - Exercise and Solution I ###
### Lab - $group - Exercise and Solution II ###
### CODE: $group - Exercise and Solution II ###
### Lab - $group - Exercise and Solution III ###
### CODE: $group - Exercise and Solution III ###
### Lab - $group - Exercise and Solution IV ###
### CODE: $group - Exercise and Solution IV ###
### Lab - $group - Exercise and Solutoin IV ###
### CODE: $group - Exercise and Solution IV ###
### Lab - $group - Exercise and Solution V ###
### CODE: $group - Exercise and Solution V ###
### Lab - $group - Exercise and Solution VI ###
### CODE: $group - Exercise and Solution VI ###

## Conditional Statement (if...else and switch...case) ##
### Class - if...else Syntax ###
### Class & Lab - if...else - Exercise and Solution 1 ###
### CODE: if...else - Exercise and Solution 1 ###
### Class & Lab - if...else - Exercise and Solution 2 ###
### CODE: if...else - Exercise and Solution 2 ###
### Class & Lab - if...else - Exercise and Solution 3 ###
### CODE: if...else - Exercise and Solution 3 ###
### Class & Lab - if ...else - Exercise and Solution 4 ###
### CODE: if...else - Exercise and Solution 4 ###
### Class - Switch...Case Syntax ###
### CODE: Switch...Case - Exercise and Solution 1 ###
### Class & Lab - Switch...case - Exercise and Solution 2 ###
### CODE: Switch...Case - Exercise and Solution 2 ###

## $lookup (JOINS) in MongoDB ##
### Class & Lab - Understanding MongoDB $lookup ###
### CODE: Understanding MongoDB $lookup ###
### Class: $lookup by Example ###
### CODE: $lookup by Example ###

## MongoD Dates and Times ##
### Class - Understanding the MongoDB Dates and Times ###
### Class & Lab - Date() ###
### CODE: Date() ###
### Class & Lab - new Date() & ISODate ###
### CODE: new Date() & ISODate ###
### Lab - new Date() & ISODate - More Example ###
### CODE: new Date() & ISODate - More Example ###
### Lab - Exercise and Solution 1 ###
### CODE: Exercise and Solution 1 ###
### Class - Exercise and Solution 2 ###
### CODE: Exercise and Solution 2 ###

## Schema Validation ##
### Class - Understanding MongoDB Schema Validation ###
### Class - Validation Rules ###
### Class - Options in Validation ###
### Class - Recommended Operator for Validation ###
### Lab - Constructing Validation for a New Collection by Example ###
### CODE: Constructing Validation for a New Collection by Example ###
### Lab - Constructing Validation for a New Collection by Example 2 ###
### CODE: Constructing Validation for a New Collection by Example 2 ###
### Class - Constructing Validation for an Existing Collection by Example ###
### CODE: Constructing Validation for an Existing Collection by Example ###

## SQL vs MongoDB: Practical Demonstration ##
### Class - MongoDB vs MySQL Term/Concept ###
### Class - Constructing Tables, Collection and Inserting Data ###
### Lab - Constructing Tables, Collection and Inserting Data LAB ###
### CODE: Constructing Tables, Collection and Inserting Data LAB ###
### Class & Lab - Exercise and Solution 1 - SQL vs MongoDB ###
### CODE: Exercise and Solution 2 - SQL vs MongoDB ###
### Class & Lab - Exercise and Solution 3 - SQL vs MongoDB ###
### CODE: Exercise and Solution 3 - SQL vs MongoDB ###
### Class & Lab - Exercise and Solution 4 - SQL vs MongoDB ###
### CODE: Exercise and Solution 4 - SQL vs MongoDB ###
### Class & Lab - Exercise and Solution 5 - SQL vs MongoDB ###
### CODE: Exercise and Solution 5 - SQL vs MongoDB ###
### Class & Lab - Exercise and Solution 6 - SQL vs MongoDB ###
### CODE: Exercise and Solution 6 - SQL vs MongoDB ###
### Class & Lab - Exercise and Solution 7 - SQL vs MongoDB ###
### CODE: Exercise and Solution 7 - SQL vs MongoDB ###
### Class & Lab - Exercise and Solution 8 - SQL vs MongoDB ###
### CODE: Exercise and Solution 8 - SQL vs MongoDB ###
### Class & Lab - Exercise - SQL vs MongoDB ###
### CODE: Exercise - SQL vs MongoDB ###

## Replication in MongoDB ##
### Class: Introduction to MongoDB Replication ###
### Class: Definition and Advantages of Replication ###
### Class: How Replication Works ###
### Class: Replica Set ###
### Class: Arbiter Node ###
### Class: HeartBeat Signal ###
### Class: Asynchronous Replication ###
### Class: Failover and the Process of FailOver ###
### Lab: Demonstrating How Replication Works ###
### CODE: Demonstration How Replication Works ###

## MongoDB Associate Developer Exam - #1 ##
### Practice Test 1: Exam #1 ###

## MongoDB Associate Developer Exam - #2 ##
### Practice Test 2: Exam #2 ###

## Check These Out ##
### Check Out My Other Courses ###