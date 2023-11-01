# PostgreSQL Tutorial #
1. Goals:
	1. If looking for learning PostgreSQL fast
	2. If need to develop applications using PostgreSQL as the back-end database management system
	3. If migrating from other database management systems such as MySQL, Oracle, and Microsoft SQL Server to PostgreSQL

## Getting Started with PostgreSQL ##
1. Topics:
	1. How to install PostgreSQL on Windows, Linux, and MacOS
	2. How to connect to PostgreSQL using psql tool
	3. How to load a sample database into PostgreSQL for practice
### Getting Started ###
#### What is PostgreSQL ####
1. Abstract:
	1. Introduction to PostgreSQL and its applications in today's software stack
2. What is PostgreSQL?
	1. It is an **advanced, enterprise-class, open-source relational database system**
	2. It supports **SQL** (relational) and **JSON** (non-relational) querying.
	3. **It is highly stable** (> 20 years of development)
	4. Used as primary database for many **web-applications** & **mobile applications** & **analytics applications**

##### History #####
1. Started in UC Berkeley
2. Goal: **To add minimal features needed to support multiple data types**
3. PostgreSQL can run on Windows, Linux, MacOS, Solaris

##### Common Use Cases of PostgreSQL #####
1. A Robust Databsea in the LAPP Stack
	1. LAPP (Linux Apache PostgreSQL PHP/Python/Perl)
	2. **PostgreSQL is primarily used as robust back-end database that powers dynamic websites & web-applications**
2. General Purpose Transaction Database
	1. Large corporations & startups support PostgreSQL as primary db to support their apps & products
3. Geospatial Database
	1. [PostGIS extension](https://postgis.net/) - An extension of PostgreSQL that supports geospatial databases for geographic information systems (GIS)
4. Language Support
	1. Python
	2. Java
	3. C#
	4. C/C++
	5. Ruby
	6. JavaScript (Node.js)
	7. Perl
	8. Go
	9. Tcl
5. PostgreSQL Feature Highlights
	1. **User-defined Types**
		1. How does PostgreSQL support user-defined types?
			1. PostgreSQL supports user-defined types through the CREATE TYPE statement. This feature allows users to define their own custom data types, extending the set of built-in types provided by the database.
			2. Here's an overview of how PostgreSQL supports user-defined types:
				1. `CREATE TYPE`: The CREATE TYPE statement is **used to define a new user-defined type**. It **allows you to specify the name of the type, the underlying data type it is based on (e.g., integer, text, etc.), and any additional constraints or behaviors**.
				2. **Attribute Definition**: **User-defined types can have attributes, similar to columns in a table**. **Each attribute has a name and a data type, which can be either a built-in type or another user-defined type**.
				3. **Composite Types**: PostgreSQL supports composite types, which are **user-defined types that consist of multiple attributes**. These **types are defined using the** `CREATE TYPE` **statement and can be used to represent structured data**.
				4. **Enumerated Types**: PostgreSQL also supports **enumerated types**, which **are user-defined types that represent a fixed set of values**. Enumerated types are **defined using** the `CREATE TYPE` statement, **specifying the allowed values for the type**.
				5. **Domain Types**: **Domain types allow you to define a new type based on an existing type, adding additional constraints or behaviors**. For **example**, you can define a domain type **"email" based on the built-in text type, but with a constraint that ensures the value is a valid email address**.
				6. **Operator Overloading**: **PostgreSQL allows you to define custom operators for user-defined types, enabling you to perform operations on your custom types using syntax similar to built-in types**.
				7. **Functions and Methods**: You **can define functions and methods specific to your user-defined types, allowing you to implement custom behavior for operations on those types**.
				8. **Input and Output Functions**: PostgreSQL allows you to define **custom input and output functions for user-defined types**. These **functions are responsible for converting the type to and from a textual representation**.
				9. **Type Casting**: You can define **custom type casting functions to allow automatic or explicit type conversions between your user-defined types and built-in types**.
			3. By supporting user-defined types, PostgreSQL offers flexibility and extensibility to its users, enabling them **to define custom data structures and behaviors that suit their specific application requirements**.
	2. **Table inheritance**
		1. What is table inheritance in PostgreSQL?
			1. Table inheritance in PostgreSQL is a feature that allows you to create a hierarchy of tables based on a parent-child relationship. It enables you to define a parent table with a common set of columns and then create child tables that inherit those columns and add their own specific columns. This inheritance relationship provides several benefits, including code reusability, data partitioning, and query simplification.
			2. Here are the key aspects of table inheritance in PostgreSQL:
				1. **Parent Table**: The parent table serves as the template for the child tables. It contains a complete set of columns that will be inherited by the child tables. The parent table itself cannot have any data rows because it is primarily used as a blueprint.
				2. **Child Tables**: Child tables inherit the structure and columns of the parent table and can also define their additional columns. Each child table represents a specific subset or partition of the data. Child tables can have their indexes, constraints, and triggers independent of the parent table.
				3. **Inheritance Hierarchy**: You can create a hierarchy of tables by defining multiple levels of inheritance, where child tables themselves become parents for further child tables. This allows you to create more specialized subsets of data.
				4. **Column Inheritance**: Columns defined in the parent table are automatically inherited by the child tables. Any changes made to the parent table's columns, such as adding or altering columns, are reflected in the child tables.
				5. **Constraints and Triggers**: Child tables can have their own unique constraints and triggers, in addition to those inherited from the parent table. This allows you to enforce specific rules or behaviors for individual tables within the inheritance hierarchy.
				6. **Querying and Partitioning**: When querying the parent table, PostgreSQL automatically includes the data from all child tables. This allows you to retrieve data from the entire hierarchy as if it were a single table. Additionally, table inheritance can be used for data partitioning, where each child table stores a subset of data based on specific criteria (e.g., time ranges, geographical regions).
			3. Table inheritance in PostgreSQL provides a way to organize and structure data, enabling code reuse and simplifying queries while still maintaining flexibility for individual child tables. It is important to note that table inheritance is different from relational database concepts like foreign keys, as it focuses on table structure and data organization rather than enforcing referential integrity.
	3. **Sophisticated locking mechanism**
		1. What sophisticated locking mechanisms exist in PostgreSQL?
			1. PostgreSQL, an open-source relational database management system, offers various sophisticated locking mechanisms **to ensure data consistency and transaction isolation**. Here are some of the prominent locking mechanisms available in PostgreSQL:
				1. **Row-Level Locking**: PostgreSQL supports row-level locking, **allowing multiple transactions to read or write different rows simultaneously**. This **approach minimizes contention and increases concurrency**.
				2. **Table-Level Locking**: PostgreSQL also supports table-level locking, where **a transaction can acquire an exclusive lock on an entire table**. This lock **prevents other transactions from reading or modifying the table until the lock is released**.
				3. **Advisory Locks**: Advisory locks are **flexible locks that allow applications to coordinate their activities based on custom-defined lock keys**. **These locks are not automatically enforced by the database system but provide a way for applications to implement their own locking mechanisms**.
					1. Give more details about advisory locks.
						1. Certainly! Advisory locks in PostgreSQL are a form of locking mechanism that **allows applications to implement their own custom locking semantics**. Unlike traditional locks in PostgreSQL, **advisory locks are not automatically enforced by the database system but provide a way for applications to coordinate activities and synchronize access to resources using user-defined lock keys**.
						2. Here are some key details about advisory locks in PostgreSQL:
							1. **Lock Keys**: Advisory locks are based on lock keys, which are **32-bit signed integers**. **Applications can use any value as a lock key, such as an ID or a combination of values that uniquely identify a resource or a section of code**.
							2. **Shared and Exclusive Locks**: Advisory locks **can be acquired in either shared mode or exclusive mode**. **Multiple transactions can acquire shared locks on the same lock key simultaneously**. However, **exclusive locks are mutually exclusive, meaning only one transaction can hold an exclusive lock on a particular key at a given time**.
							3. **Lock Scope**: **Advisory locks are session-based**, meaning they are **automatically released at the end of the session or when the transaction holding the lock is committed or rolled back**. **Advisory locks are not persistent and do not survive database restarts**.
							4. **Lock Functions**: PostgreSQL provides a **set of built-in functions for managing advisory locks**:
								1. `pg_advisory_lock(key)` **acquires an exclusive advisory lock on the specified key**.
								2. `pg_advisory_lock_shared(key)` **acquires a shared advisory lock on the specified key**.
								3. `pg_try_advisory_lock(key)` **attempts to acquire an exclusive advisory lock but returns immediately (without blocking) if the lock is unavailable**.
								4. `pg_try_advisory_lock_shared(key)` **attempts to acquire a shared advisory lock but returns immediately if the lock is unavailable**.
								5. `pg_advisory_unlock(key)` **releases an advisory lock previously acquired by the current session**.
								6. `pg_advisory_unlock_all()` **releases all advisory locks held by the current session**.
							5. **Lock Compatibility**: **Advisory locks do not conflict with regular row-level or table-level locks**. **They operate independently and can coexist with other lock types in PostgreSQL**.
							6. **Application-Level Semantics**: The **actual meaning and usage of advisory locks depend on how an application chooses to interpret them**. **Developers can define their own conventions for using advisory locks to synchronize access to resources or coordinate actions across multiple transactions or processes**.
						3. Advisory locks are **particularly useful in scenarios where applications need to coordinate actions or enforce custom locking semantics beyond the built-in locking mechanisms provided by PostgreSQL**. They provide a **flexible tool for implementing application-level synchronization and coordination**.
				4. **Deadlock Detection**: PostgreSQL **employs a deadlock detection mechanism to identify and resolve deadlocks automatically**. **When two or more transactions are waiting for resources held by each other, PostgreSQL detects the deadlock and aborts one of the transactions to resolve the conflict**.
				5. **Serializable Isolation Level**: PostgreSQL **provides the Serializable isolation level**, which **guarantees the highest level of isolation**. It **ensures that transactions appear to execute serially, even though they may run concurrently**. **Serializable isolation prevents phenomena like dirty reads, non-repeatable reads, and phantom reads**.
					1. What is non-repeatable reads?
						1. Non-repeatable reads is a phenomenon that can occur in a concurrent transaction environment when a transaction reads the same data multiple times within its own execution but obtains different values each time due to updates made by other concurrent transactions. This inconsistency can lead to unexpected and incorrect results in certain situations.
						2. To understand non-repeatable reads, let's consider the following scenario involving two transactions, T1 and T2:
							1. Transaction T1 begins and reads a certain row of data.
							2. Transaction T2 begins and updates the same row of data.
							3. Transaction T1 reads the same row of data again after T2 has made its update.
						3. In this scenario, if the value read by T1 in the second read differs from the value obtained in the first read, a non-repeatable read has occurred. The reason behind this inconsistency is that T1's read is influenced by the concurrent update made by T2. Consequently, the data read by T1 is no longer consistent within its own transaction.
						4. Non-repeatable reads can occur when transactions are operating under a lower isolation level, such as the Read Committed isolation level, which allows unrepeatable reads. In this isolation level, a transaction can see the changes made by other committed transactions during its own execution. As a result, if a transaction re-reads the same data within its own execution, it might encounter different values due to concurrent updates.
						5. To mitigate non-repeatable reads, higher isolation levels like Repeatable Read and Serializable can be used. These isolation levels provide stronger guarantees by ensuring that a transaction's reads remain consistent throughout its execution, even in the presence of concurrent updates. By holding locks or using multi-version concurrency control (MVCC) techniques, these isolation levels prevent other transactions from modifying data that is being read, thus avoiding non-repeatable reads.
				6. **Advisory Lock Functions**: PostgreSQL offers a set of built-in functions for managing advisory locks, such as pg_advisory_lock(key), pg_try_advisory_lock(key), pg_advisory_unlock(key), and pg_advisory_unlock_all(). These functions allow applications to acquire, release, and check the status of advisory locks.
				7. **Locking Statements**: PostgreSQL provides explicit locking statements that allow transactions to acquire specific locks on tables or rows. The LOCK TABLE statement can lock tables with different modes (e.g., ACCESS SHARE, ROW SHARE, ROW EXCLUSIVE, SHARE UPDATE EXCLUSIVE, EXCLUSIVE), while the SELECT ... FOR UPDATE statement can acquire row-level locks within a transaction.
			2. It's important to note that the choice of locking mechanism depends on the specific requirements and concurrency control strategy of your application. Proper understanding and usage of these locking mechanisms can help ensure data integrity, concurrency, and avoid performance bottlenecks.
	4. [Foreign key referential integrity](https://www.postgresqltutorial.com/postgresql-foreign-key/)
	5. [Views](https://www.postgresqltutorial.com/postgresql-views/), rules, [subquery](https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-subquery/)
	6. **Nested transactions (savepoints)**
	7. **Multi-version concurrency control (MVCC)**
	8. **Asynchronous replication**
	9. **Native Microsoft Windows Server version**
	10. **Tablespaces**
	11. **Point-in-time recovery**
	12. Advantages:
		1. Designed to be extensible:
			1. We can define our own datatypes
			2. We can define our own index types
			3. **We can define our own functional Languages**
			4. ...
			5. We can develop **custom plugin** to meet our requirements if we do not like any part of the system
				1. Example: **Adding a new optimizer**
6. Who uses PostgreSQL
	1. Companies:
		1. Apple
		2. Fujitsu
		3. Red Hat
		4. Cisco
		5. Juniper Network
		6. Instagram
		7. ...

#### Introduction to PostgreSQL Sample Database ####
1. Abstract:
	1. Sample data to help learn PostgreSQL fast
		1. Database name: `dvdrental`
2. DVD rental database:
	1. Represents the business processes of a DVD rental store
	2. Objects:
		1. 15 Tables
		2. 1 trigger
		3. 7 Views
		4. 8 Functions
		5. 1 domain
		6. 13 sequences
3. 15 Tables:
	1. actor - stores actors data including first name & last name
	2. film - stores film data such as title, release year, length, rating, etc
	3. film_actor - stores the relationships between films and actors
	4. category - stores film's categories data
	5. film_category - stores the relationships between films and categories
	6. store - contains the store data including manager staff and address
	7. inventory - stores inventory data
	8. rental - stores rental data
	9. payment - stores customer's payments
	10. staff - stores staff data
	11. customer - stores customer data
	12. address - stores address data for staff and customers
	13. city - stores city names
	14. country - stores country names
4. [Download DVD Rental Sample Database](https://www.postgresqltutorial.com/wp-content/uploads/2019/05/dvdrental.zip)
	1. Extract it to `dvdrental.tar` before loading it to PostgreSQL database

#### Download Printable ER Diagram ####
1. [Download the Printable ER Diagram](https://www.postgresqltutorial.com/wp-content/uploads/2018/03/printable-postgresql-sample-database-diagram.pdf)

### PostgreSQL on Windows ###
#### Install PostgreSQL on Windows ####
1. Summary: Step by step on how to install PostgreSQL on local system
2. Installer for Windows system since version 8.0
3. Version used for tutorial: 12
4. Steps:
	1. Download PostgreSQL installer for Windows
	2. Install PostgreSQL
	3. Verify the installation

##### Download PostgreSQL Installer for Windows #####
1. Open [PostgreSQL Installers on the EnterpriseDB](https://www.enterprisedb.com/downloads/postgres-postgresql-downloads)
2. Click on **Windows x86-64** link

##### Install PostgreSQL on Window Step by Step #####
1. Admin privileges needed to install on Windows
2. Steps:
	1. Double click on the installer file
	2. Click the Next button
	3. Specify installation folder (keep default)
	4. Click the Next button
	5. Select software components to install:
		1. 

##### Verify the Installation #####

#### Connect to PostgreSQL Database Server ####
#### Load the Sample Database into the PostgreSQL Database Server ####

### PostgreSQL on Linux ###
#### Install PostgreSQL on Ubuntu ####

### PostgreSQL on MacOS ###
#### Install PostgreSQL on MacOS ####

## Basic PostgreSQL Tutorial ##
1. Basic data querying techniques:
	1. Selecting data
	2. Sorting result sets
	3. Filtering rows
2. Advanced queries:
	1. Joining multiple Tables
	2. Using set operations
	3. Constructing Subquery
3. Managing database tables:
	1. Constructing new table
	2. Modifying an existing table's structure

## Section 1: Querying Data ##
1. Summary: How to use the basic PostgreSQL SELECT statement to query data from a table
2. Querying data from table using `SELECT` statement is the most common task
3. `SELECT` is the most complex statement in PostgreSQL
	1. It has many clauses that can be used to form flexible query
4. `SELECT` statement has following clauses:
	1. Select distinct rows using `DISTINCT` operator
	2. Sort rows using `ORDER BY` clause
	3. Filter rows using `WHERE` clause
	4. Select a subset of rows from a table using `LIMIT` and `FETCH` clause
	5. Group rows into groups using `GROUP BY` clause
	6. Filter groups using `HAVING` clause
	7. Join with tables using joins such as `INNER JOIN`, `LEFT JOIN`, `FULL OUTER JOIN`, `CROSS JOIN` clauses
	8. Perform set operations using `UNION`, `INTERSECT`, and `EXCEPT`
	
##### PostgreSQL SELECT Statement Syntax #####
1. Retrieve data from a single table:

		SELECT
			select_list
		FROM
			table_name;
			
	1. Select list: column or list of columns in a table from which we want to retrieve data
		1. List of columns: place `,` between two columns to separate them.
		2. `*`: all columns
		3. Can also contain **expressions** or **literal values**
	2. `FROM`: used to specify the name of the table we want to query
		1. **It is optional**
			1. If we don't want to query any table
2. PostgreSQL evaluates `FROM` clause before `SELECT` clause in `SELECT` statement
	1. SQL keywords are case-insensitive
	
##### PostgreSQL SELECT examples #####
1. Consider `customer` table:

		customer
			* customer_id
			store_id
			first_name
			last_name
			email
			address_id
			activebool
			create_date
			last_update
			active
			
2. To query data from one column:
	1. Get first names of all customers from `customer` table:
	
			SELECT first_name FROM customer;
			
3. `;` - it is not part of SQL Statement
	1. It signals the end of SQL statement.
	2. It is also used to separate two SQL statements.
	
##### Using PostgreSQL SELECT statement to query data from multiple columns example #####
1. Example:

		SELECT
			first_name,
			last_name,
			email
		FROM
			customer;

##### Using PostgreSQL SELECT statement to query data from all columns of a table example #####
1. Example:

		SELECT * FROM customer;
		
	1. *: shorthand for all columns
2. Cons:
	1. Not a good practice when we embed SQL statements in application code like Python, Java, Node.js or PHP
		1. Database performance:
			1. If we have a table with a lot of data. We will end up fetching all columns of the table which may not be necessary for the application
		2. Application performance:
			1. Retrieving unnecessary data from database increases traffic between database server and application server
				1. Application might get slower to respond and hence less scalable
	2. Solution:
		1. Explicitly mention column names whenever possible to get only the necessary data from the databases

##### Using PostgreSQL SELECT statement with expressions example #####
1. To return full names & emails:

		SELECT
			first_name || ' ' || last_name
			email
		FROM
			customer;
			
2. Concatenation operator: `||`
3. Column aliases in the next chapter

##### Using PostgreSQL SELECT statement with expressions example #####
1. Select statement with an expression:
	1. It omits **FROM** Clause
	
			SELECT 5 * 3;

### Select - How to query data from a single table ###
#### PostgreSQL SELECT statement syntax ####
#### PostgreSQL SELECT examples ####

### Column aliases - How to assign temporary names to columns or expressions in a query ###
1. Summary:
	1. Column aliases are used **to assign temporary names to columns in queries**

#### Introduction to the PostgreSQL column aliases ####
1. Column alias: 
	1. Allows to assign a column or an expression in the select list of a `SELECT` statement a temporary name
	2. It exists temporarily during the execution of the query
2. Syntax:

		SELECT column_name AS alias_name
		FROM table_name;
		
	1. `AS` - optional (it can be omitted)
	
			SELECT column_name alias_name
			FROM table_name;
			
2. Alias for an expression:

		SELECT expression AS alias_name
		FROM table_name;
		
	1. Helps make headings of query output more meaningful

##### PostgreSQL column alias examples #####
#### Assigning a column alias to a column example ####
1. Return first names & last names of all customers from `customer` table:

		SELECT
			first_name,
			last_name
		FROM
			customer;
			
2. Rename the `last_name` heading to `surname`

		SELECT
			first_name,
			last_name as surname
		FROM
			customer;

#### Assigning a column alias to an expression example ####
1. Return full-name of customer:

		SELECT
			first_name || ' ' || last_name AS full_name
		FROM
			customer;

#### Column aliases that contain spaces ####
1. If a column alias contains one or more spaces, surround it with double quotes:

		column_name AS "column alias"
		
2. Example:

		SELECT
			first_name || ' ' || last_name AS "full name"
		FROM
			customer;

#### Summary ####
1. Assign a column or an expression a column alias using the syntax: `column_name AS alias_name` or `expression AS alias_name`
2. `AS` keyword is optional
3. Use `"`s to surround a column alias that contains spaces.

### Order By - How to sort the result set returned from a query ###
1. Summary: How to sort the result set returned from the `SELECT` statement by using PostgreSQL `ORDER BY` clause.

#### Introduction to PostgreSQL ORDER BY clause ####
#### PostgreSQL ORDER BY examples ####
#### Using PostgreSQL ORDER BY clause to sort rows by one column ####
#### Using PostgreSQL ORDER BY clause to sort rows by one column in descending order ####
#### Using PostgreSQL ORDER BY clause to sort rows by multiple columns ####
#### Using PostgreSQL ORDER BY clause to sort rows by expressions ####
#### PostgreSQL ORDER BY clause and NULL ####
#### Summary ####

### Select Distinct - Clause that removes duplicate rows in a result set ###

## Section 2: Filtering Data ##
### Where - Filter rows based on specified condition ###
### Limit - Get a subset of rows generated by a query ###
### Fetch - Limit the number of rows returned by a query ###
### In - Select data that matches any value in a list of values ###
### Between - Select data that is a range of values ###
### Like - Filter data based on pattern matching ###
### Is Null - Check if a value is null or not ###

## Section 3: Joining Multiple Tables ##
### Joins - A brief overview ###
### Table aliases - How to use table aliases in a query ###
### Inner Join - Select rows in one table that has the corresponding rows in another table ###
### Left Join - Select rows from one table that may or may not have the corresponding rows in other tables ###
### Self-join - Join a table to itself by comparing a table to itself ###
### Full Outer Join - To find a row in a table that does not have a matching row in another table ###
### Cros Join - Cartesian product of the rows in two or more tables ###
### Natural Join - Join two or more tables using implicit join conditions based on common column names in joined tables ###

## Section 4: Grouping Data ##
### Group By - Divide rows into groups and apply an aggregate function on each ###
### Having - Apply conditions to groups ###

## Section 5: Set Operations ##
### Union - Combine result sets of multiple queries into a single result set ###
### Intersect - Combine result sets of two or more queries and return a single result set that has the rows appear in both result sets ###
### Except - Return the rows in the first query that does not appear in the output of the second query ###

## Section 6: Grouping sets, Cube, and Rollup ##
### Grouping Sets - Generate multiple grouping sets in reporting ###
### Cube - Define multiple grouping sets that include all possible combinations of dimensions ###
### Rollup - Generate reports that contain totals and subtotals ###

## Section 7: Subquery ##
### Subquery - Write a query nested inside another query ###
### ANY - Retrieve data by comparing a value with a set of values returned by a subquery ###
### ALL - Query data by comparing a value with a list of values returned by a subquery ###
### EXISTS - Check for the existence of rows returned by a subquery ###

## Section 8: Common Table Expressions ##
### PostgreSQL CTE - Introduction to PostgreSQL common table expressions or CTEs ###
### Recursive query using CTEs - Recursive query and learn how to apply it in various contexts ###

## Section 9: Modifying Data ##
1. How to insert data into a table with `INSERT` statement
2. How to modify data with the `UPDATE` statement
3. How to remove data with the `DELETE` statement
4. How to use `UPSERT` statement to merge data

### Insert - How to insert a single row into a table ###
### Insert multiple rows - How to insert multiple rows into a table ###
### Update - Update existing data in table ###
### Update join - Update values in a table based on values in another table ###
### Delete - Delete data in a table ###
### Upsert - Insert or update data if the new row already exists in the table ###

## Section 10: Transactions ##
### PostgreSQL Transactions - How to handle transactions in PostgreSQL using BEGIN, COMMIT, and ROLLBACK statements ###

## Section 11: Import & Export Data ##
1. How to import and export PostgreSQL data from and to CSV file format using the copy command

### Import CSV file into Table - Show you how to import CSV file into a table ###
### Export PostgreSQL Table to CSV file - Show you how to export tables to a CSV file ###

## Section 12: Managing Tables ##
1. PostgreSQL data types
2. How to construct new tables and modify the structure of existing tables

### Data types - Cover the most commonly used PostgreSQL data types ###
### Construct a table - How to construct a new table in the database ###
### Select into & Construct table as - How to construct a new table from the result set of a query ###
### Auto-increment column with SERIAL - Uses SERIAL to add an auto-increment column to a table ###
### Sequences - Sequences and how to use a sequence to generate a sequence of numbers ###
### Identity column - How to use the identity column ###
### Alter table - Modify the structure of an existing table ###
### Rename table - Change the name of a table to a new one ###
### Add column - How to use add one or more columns to an existing table ###
### Drop column - How to drop a column of a table ###
### Change column data type - How to change the data of a column ###
### Rename column - How to rename one or more columns of a table ###
### Drop table - Remove an existing table and all of its dependent objects ###
### Truncate table - Remove all data in a large table quickly and efficiently ###
### Copy a table - How to copy a table to a new one ###

## Section 13: Understanding PostgreSQL Constraints ##
### Primary key - How to define a primary key when constructing a table or adding a primary key to an existing table ###
### Foreign key - How to define foreign key constraints when constructing a new table or add foreign key constraints to existing table ###
### CHECK constraint - Add logic to check value based on Boolean expression ###
### UNIQUE constraint - Make sure that values in a column or a group of columns are unique across the table ###
### NOT NULL constraint - Ensure that values in a column are not `NULL` ###

## Section 14: PostgreSQL Data Types in Depth ##
### Boolean - Store `TRUE` and `FALSE` values with a Boolean data type ###
### CHAR, VARCHAR, and TEXT - How to use character types including `CHAR`, `VARCHAR`, and `TEXT` ###
### NUMERIC - How to use `NUMERIC` type to store values that precision is required ###
### Integer - Integer types in PostgreSQL including `SMALLINT`, `INT`, and `BIGINT` ###
### DATE - `DATE` data type for storing date values ###
### Timestamp - timestamp data types ###
### Interval - How to use interval data type to handle a period of time effectively ###
### TIME - `TIME` datatype to manage time of day values ###
### UUID - How to use `UUID` datatype and how to generate `UUID` values using supplied modules ###
### Array - How to work with array and handy functions for array manipulation ###
### hstore - data type which set of key/value pairs stored in single value ###
### JSON - How to work with JSON data type and how to use some of the most important JSON operators and functions ###
### User-defined data types - How to use `CREATE DOMAIN` and `CREATE TYPE` statements to construct user-defined data types ###

## Section 15: Conditional Expressions & Operators ##
### `CASE` - How to form conditional queries with `CASE` expression ###
### `COALESCE` - Return first non-null argument. Use it to substitute `NULL` by a default value ###
### `NULLIF` - Return `NULL` if first argument equals second one ###
### `CAST` - Convert from one data type into another e.g. from a string into an integer, from a string into a date ###

## Section 16: PostgreSQL Utilities ##
### psql commands - most common psql commands that help us interact with psql faster and more effectively ###

## Section 17: PostgreSQL Recipes ##
### How to compare two tables - How to compare data in two tables in a database ###
### How to delete duplicate rows in PostgreSQL - Ways to delete duplicate rows from a table ###
### How to generate a random number in a range - How to generate a random number in a specific range ###
### EXPLAIN statement - How to use the `EXPLAIN` statement to return the execution plan of a query ###
### PostgreSQL vs MySQL - Compare PostgreSQL with MySQL in terms of functionalities ###

## Advanced PostgreSQL Tutorial ##
1. Advanced concepts including:
	1. Stored procedures
	2. indexes
	3. Views
	4. triggers
	5. Database Administration

### PostgreSQL PL/pgSQL ###
1. Step by step how to develop PostgreSQL user-defined functions using PL/pgSQL procedural language.

### PostgreSQL Triggers ###
1. PostgreSQL trigger concept & how to manager triggers in PostgreSQL.

### PostgreSQL Views ###
1. How to manage views such as `create`, `alter`, and remove views from database

### PostgreSQL Indexes ###
1. Indexes are effective tools to enhance database performance
2. They help database server find specific rows much faster than it could do without indexes

### PostgreSQL Administration ###
1. Roles
2. Databases management
3. Backup and restore

# Q & A #
## How is PostgreSQL different from MySQL? ##
## What is the architecture of PostgreSQL database? ##
## What are the features of PostgreSQL? ##