# PostgreSQL Tutorial #
1. [https://www.postgresqltutorial.com/postgresql-getting-started/](https://www.postgresqltutorial.com/postgresql-getting-started/)
2. The tutorial helps understand PostgreSQL quickly
2. Many practical examples are given
3. How to solve the examples innovatively
4. Who is this course for?
	1. If looking to learn PostgreSQL fast and easily
	2. If we want to develop applications using PostgreSQL as a back-end database management system
	3. Migrating from other dbms such as MySQL, Oracle, Microsoft SQL Server to PostgreSQL
5. Tutorial demonstrates unique features of PostgreSQL (most advanced open-source database management system?)

## Getting Started ##
1. Introduction:
	1. How to install PostgreSQL on Windows, Linux, MacOS
	2. How to connect using psql tool
	3. How to load sample database into PostgreSQL for practicing
2. Topics
	1. How to install PostgreSQL on Windows, Linux and macOS
	2. How to connect to PostgreSQL using `psql` tool
	3. How to load sample database into PostgreSQL for practicing
3. Getting Started
	1. [What is PostgreSQL](https://www.postgresqltutorial.com/what-is-postgresql/) - Introduces PostgreSQL and it's applications in software stack
	2. [Introduction to PostgreSQL Sample Database](https://www.postgresqltutorial.com/postgresql-sample-database/) - dvdrental
4. PostgreSQL on Windows
5. PostgreSQL on Linux
6. PostgreSQL on MacOS
	1. [Install PostgreSQL on MacOS](https://www.postgresqltutorial.com/install-postgresql-macos/) - how to download, how to install, how to restore sample database into PostgreSQL database server
		1. [Download Installer](https://www.enterprisedb.com/downloads/postgres-postgresql-downloads)
	2. Launch wizard
	3. Select directory where it must be installed (`/Library/PostgreSQL/12`)
	4. Select components to install (uncheck stack builder)
	5. Specify directory where PostgreSQL stores data (`/Library/PostgreSQL/12/data`)
	6. Enter password for user account (keep it)
	7. Specify port: 5432
	8. Select locale (locale of current OS by default)
	9. Install
	10. Load sample database
		1. Launch **pgAdmin**
		2. Enter password
		3. Right click on PostgreSQL 12 and select **Create** > **Database..**
		4. Enter **dvdrental** as database
		5. Enter **postgres** as owner
		6. Click save 
	11. [Download sample database](https://www.postgresqltutorial.com/postgresql-sample-database/)
	12. Unzip it
	13. Right click on **dvdrental** and select **Restore...**
	14. Select directory as Format (1)
	15. Select directory that contains sample database as Filename (2)
	16. Enter role as **postgres**
	17. Click **Restore**

### What is PostgreSQL ###
1. It is advanced, enterprise-class open-source relational database system
2. It supports the following querying options
	1. SQL (relational)
	2. JSON (non-relational)
3. It is highly stable db backed by 20 years of development by open-source community
4. Use cases:
	1. Web applications
	2. Mobile applications
	3. Analytics applications

### Common Use Cases of PostgreSQL ###
1. Robust database in LAPP stack
	1. Linux, Apache, PostgreSQL, PHP (or Python and Perl)
	2. Usually used as robust back-end database
2. General purpose transaction database
	1. Primary database in many applications
3. Geospatial database
	1. [PostGIS extension](https://postgis.net/) - extension supports geospatial databases for geographpic information systems (GIS)
4. Language support
	1. Popular programming languages
		1. Python
		2. Java
		3. C#
		4. C/C++
		5. Ruby
		6. JavaScript (Node.js)
		7. Perl
		8. Go
		9. Tcl

### PostgreSQL Feature Highlights ###
1. Similar to the ones offered by enterprise-class database management systems:
	1. User-defined types (?)
	2. Table inheritance (?)
	3. Sophisticated locking mechanism
	4. [Foreign key referential integrity](https://www.postgresqltutorial.com/postgresql-foreign-key/)
	5. [Views](https://www.postgresqltutorial.com/postgresql-views/), rules, [Subquery](https://www.postgresqltutorial.com/postgresql-subquery/)
	6. Nested transactions (savepoints)
	7. Multi-version concurrency control (MVCC)
	8. Asynchronous replication
2. Recent versions support
	1. Native Microsoft Windows Server version
	2. Tablespaces
	3. Point-in-time recovery
3. PostgreSQL is designed to be extensible
	1. It allows user to define
		1. Own data types
		2. Own index types
		3. Own functional languages
		4. ...
	2. A custom plugin can be developed (to replace parts that we don't like)
		1. Example: adding new optimizer

### Who Uses PostgreSQL ###
1. Apple
2. Fujitsu
3. Red Hat
4. Cisco
5. Juniper Networks
6. Instagram
7. ...

### PostgreSQL Sample Database ###
1. DVD Rental Database (of a DVD rental store)
2. Objects
	1. 15 tables
		1. actor - stores actors data including first name, last name
		2. film - stores film data such as title, release year, length, rating, etc...
		3. film_actor - stores the relationships between films and actors
		4. category - stores film's categories data
		5. film_category - stores relationships between films and categories
		6. store - contains store data including manager staff and address
		7. inventory - stores inventory data
		8. rental - stores rental data
		9. payment - stores customer's payments
		10. staff - stores staff data
		11. customer - stores customer data
		12. address - stores address data for staff and customers
		13. city - stores city names
		14. country - stores country names
	2. 1 trigger
	3. 7 views
	4. 8 functions
	5. 1 domain
	6. 13 sequences
	
## Install PostgreSQL on Windows ##
1. Installing PostgreSQL on local system
2. It was developed for Unix-like platform
	1. However, it is portable
		1. It can run on MacOS, Solaris, Windows
3. PostgreSQL 8.0 onwards has installer for Windows
	1. PostgreSQL 12 will be installed on Windows 10
4. Three steps:
	1. Download PostgreSQL installer on Windows
	2. Install PosgreSQL
	3. Verify the installation

### Download PostgreSQL Installer for Windows ###
1. Go to [PosgreSQL installers on the EnterpriseDB](https://www.enterprisedb.com/downloads/postgres-postgresql-downloads)
2. Click donwload link

### Install PostgreSQL on Windows Step by Step ###
1. Pre-requisite: Admin privileges.
2. Steps:
	1. Step 1: Double click the installer
	2. Step 2: Click Next button
	3. Step 3: Specify installation folder
		1. Choose own or keep default folder
		2. Click Next
	4. Step 4: Select software components to install
		1. PostgreSQL server to install the PostgreSQL DB server
		2. pgAdmin 4 to install the PG GUI management tool
		3. Commandline tools to install psql, pg_restore, ...
			1. The tools allow us to interact with PostgreSQL DB server using commandline interface
		4. Stack builder provides GUI that allows us to download and install drivers that work with PostgreSQL
			1. Not required for the tutorial
				1. Uncheck it
	5. Step 5: Select DB directory to store data or accept default folder.
		1. Click Next
	6. Step 6: Enter password for the database superuser (postgres)
		1. PostgreSQL runs as a service in the background under service account named `postgres`
		2. If `postgres` service account is already created, give the same password
	7. Step 7: Enter port number on which PostgreSQL db server will listen
		1. Default port is 5432
			1. Ensure that no other applications are using the port
	8. Step 8: Choose the locale used by the PostgreSQL DB
		1. default locale: OS system locale is used
		2. Click Next
	9. Step 9: Setup wizard will show summary info of PostgreSQL
		1. Review it and click Next
		2. Click Next to begin installation
	10. Step 10: Click Finish to complete the installation
2. Settings:

		Installation Directory: C:\Program Files\PostgreSQL\16
		Server Installation Directory: C:\Program Files\PostgreSQL\16
		Data Directory: C:\Program Files\PostgreSQL\16\data
		Database Port: 5433
		Database Superuser: postgres
		Operating System Account: NT AUTHORITY\NetworkService
		Database Service: postgresql-x64-16
		Command Line Tools Installation Directory: C:\Program Files\PostgreSQL\16
		pgAdmin4 Installation Directory: C:\Program Files\PostgreSQL\16\pgAdmin 4
		Installation Log: C:\Users\suppo\AppData\Local\Temp\install-postgresql.log
		
### Verify the Installation ###
1. [Connect to the PostgreSQL](https://www.postgresqltutorial.com/connect-to-postgresql-database/) DB server from any client application
	1. Example: psql, pgAdmin
2. Use `psql` program
3. Search for `psql` in Windows
	1. Open SQL Shell (psql)
	2. Enter all necessary information such as server, database, port, username, and password.
		1. Press enter to accept defaults
		2. Provide password that was used during installation
4. Issue the following command: `SELECT version();` **(M)**

### Basic PostgreSQL Tutorial ###
1. Querying data from single table using basic data selection
	1. Selecting columns
	2. Sorting result sets
	3. filtering rows
2. Joining multiple tables
	1. Using set operations
	2. Constructing subquery
3. Managing database tables
	1. Creation of new table
	2. Modification of existing tables

## Section 1: Querying Data ##
1. [Select](https://www.postgresqltutorial.com/postgresql-select/) - show how to query data from single table
2. [Column aliases](https://www.postgresqltutorial.com/postgresql-column-alias/) - assigning temporary names to columns or **expressions** in query
3. [Order By](https://www.postgresqltutorial.com/postgresql-order-by/) - How to sort result set returned from query
4. [Select Distinct](https://www.postgresqltutorial.com/postgresql-select-distinct/) - Define clauses that remove duplicate rows in result set

### PostgreSQL Select ###
1. Summary: How to use basic PostgreSQL select statement to query from single table
	1. [Connecting to PostgreSQL database tutorial](https://www.postgresqltutorial.com/connect-to-postgresql-database/)
2. SELECT - statement is one of most complex statements in PostgreSQL
	1. It has many clauses to form a flexible query
3. SELECT is broken down into shorter easy-to-understand tutorials (covering the clauses)
4. Clauses of SELECT
	1. [DISTINCT](https://www.postgresqltutorial.com/postgresql-select-distinct/) - used to select distinct rows
	2. [ORDER BY](https://www.postgresqltutorial.com/postgresql-order-by/) - used to sort rows
	3. [WHERE](https://www.postgresqltutorial.com/postgresql-where/) - Filter rows using this clause
	4. [LIMIT](https://www.postgresqltutorial.com/postgresql-limit/), [FETCH](https://www.postgresqltutorial.com/postgresql-fetch/) - used to select subset of rows from table
	5. [GROUP BY](https://www.postgresqltutorial.com/postgresql-group-by/) - Group rows into groups
	6. [HAVING](https://www.postgresqltutorial.com/postgresql-having/) - Filter groups using this clause
	7. [INNER JOIN](https://www.postgresqltutorial.com/postgresql-inner-join/), [LEFT JOIN](https://www.postgresqltutorial.com/postgresql-left-join/), [FULL OUTER JOIN](https://www.postgresqltutorial.com/postgresql-full-outer-join/), [CROSS JOIN](https://www.postgresqltutorial.com/postgresql-cross-join/) - used to join tables using [joins](https://www.postgresqltutorial.com/postgresql-joins/)
	8. [UNION](https://www.postgresqltutorial.com/postgresql-union/), [INTERSECT](https://www.postgresqltutorial.com/postgresql-intersect/), [EXCEPT](https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-except/) - used to perform set operations
	
## Connect To a PostgreSQL Database Server ##
1. Summary: How to connect to the PostgreSQL DB Server via an interactive terminal program called `psql` and via **pgAdmin** application
2. Using the following tools:
	1. `psql` - terminal-based front-end to PostgreSQL db server
	2. `pgAdmin` - web-based front-end to PostgreSQL db server

### Connect to PostgreSQL Database Server using psql ###
1. `psql` - an interactive terminal program provided by PostgreSQL
	1. Can be used to:
		1. Execute SQL statements
		2. Manage database objects
	2. Launch psql and connect using `postgres` user
		1. `localhost` - default db server
	3. Issue SQL statement
	
			SELECT version();

### Connect to PosgreSQL Database Server using pgAdmin ###
1. pgAdmin application:
	1. Allows interacting with PostreSQL db server using UI
	2. Search for pgAdmin in Windows
	3. Open pgAdmin 4
		1. Application launches in web-browser
	4. Right click on **Servers** node and select **Create** > **Server...**
	5. Enter server name: **PostgreSQL** say
	6. Click **Connection** tab
	7. Enter host and password for **postgres** user and click **Save**
	8. Click on **Servers** node to expand server
		1. **postgres** db exists by default
	9. Open query tool by choosing menu item **Tool** > **Query Tool** or click lightning icon.
	10. Enter query in **Query Editor**
	11. Click **Execute** button
		1. The result will be displayed in **Data Output**

### Connect to PosgreSQL Database from Other Applications ###
1. Any app that supports ODBC or JDBC can connect to PostgreSQL db server
2. Application that uses a specific driver can also connect
	1. [Connect to PostgreSQL from Python](https://www.postgresqltutorial.com/postgresql-python/connect/)
	2. [Connect to PostgreSQL from Java](https://www.postgresqltutorial.com/postgresql-jdbc/connecting-to-postgresql-database/)
	
## Load PostgreSQL Sample Database ##
1. Launch `psql` tool
2. Enter account's information to log in to PostgreSQL db server
3. Use default values for server, db, username
4. Enter password of `postgres` user
5. New DB:

		CREATE DATABASE dvdrental;
		
6. Enter `exit` command
7. Navigate to `bin` folder of PostgreSQL installation folder:

		C:\>cd C:\Program Files\PostgreSQL\12\bin
		
8. Use `pg_restore` tool to load data into `dvdrental` database

		pg_restore -U postgres -d dvdrental C:\sampledb\dvdrental.tar
		
	1. Download: [https://www.postgresqltutorial.com/postgresql-sample-database/](https://www.postgresqltutorial.com/postgresql-sample-database/)
	2. `-U postgres` - user to login to PostgreSQL database server
	3. `-d dvdrental` - target database to load
	4. Enter password
	
### Load the DVD Rental Database using the pgAdmin ###
1. Launch **pgAdmin** tool and connect to PostgreSQL server
2. Right click **Databases** and select **Create** > **Database...** menu
3. Enter database name: `dvdrental` and click **Save**
	1. You see empty database node
4. Right click on **dvdrental** database and choose **Restore...** menu item
5. Enter path to sample database **c:\sampledb\dvdrental.tar**
6. Click **Restore** button
7. Open `dvdrental` database from object browser panel
	1. Tables are in the `public` schema
	2. Other db objects are also shown in the `public` schema

## Section 1: Querying Data ##
### Select - Show you how to query data from a single table ###
1. **Summary**: Learn how to use basic **PostgreSQL** **SELECT** statement to query data from a table
2. `SELECT` - most commonly used
	1. It is one of the most complex statements in PostgreSQL
		1. It has many clauses that can be used to form a flexible query
		2. The following clauses are avaialable with `SELECT`:
			1. `DISTINCT` - Used to select distinct rows
			2. `ORDER BY` - Used to sort rows
			3. `WHERE` - Used to filter rows
			4. `LIMIT` or `FETCH` - Used to select a subset of rows from a table
			5. `GROUP BY` - Used to group rows into groups
			6. `HAVING` - Used to filter groups
			7. `INNER JOIN`, `LEFT JOIN`, `FULL OUTER JOIN`, `CROSS JOIN` - Used to join with other tables
			8. `UNION`, `INTERSECT`, `EXCEPT` - Used to perform set operations
			
#### PostgreSQL SELECT Statement Syntax ####
1. Basic form that retrieves data from a single table:

		SELECT
			select_list
		FROM 
			table_name;
			
	1. `SELECT` statement in detail:
		1. *select_list* - one or more columns in a table from which you want to retrieve data
			1. Place `,` in between column names to separate them
			2. `*` - used to select data from all columns of the table
				1. Used to avoid giving a list of all column names
			3. Can also contain **expressions** or **literal values**
		2. `FROM` - used to specify the name of the table from which we want to query data
			1. It is optional
				1. If we do not want to query data from any table
			2. **This clause is evaluated before the select clause**
			
					FROM -> SELECT
					
2. SQL keywords are case-insensitive

#### PostgreSQL SELECT Examples ####
1. Examples of `SELECT` statement
2. Table:

		customer:
		*customer_id
		store_id
		first_name
		last_name
		email
		address_id
		activebool
		create_date
		last_update
		active

##### Using PostgreSQL SELECT Statement to Query Data From One Column Example #####
1. Find first names of all customers from customer table:

		SELECT first_name FROM customer;
		
	1. `;` is not part of the SQL statement
		1. It is used to signal the end of SQL statement
		2. It is also used to separate two SQL statements

##### Using PostgreSQL SELECT Statement to Query Data From Multiple Columns Example #####
1. Multiple columns example:
	1. First name, last name, and email of customers
	
			SELECT
				first_name,
				last_name,
				email
			FROM
				public.customer;

##### Using PostgreSQL SELECT Statement to Query Data From All Columns of a Table Example #####
1. Select data from all columns of a `customer` table:

		 SELECT * FROM public.customer;
		 
	1. `*` - Shorthand for all columns
		1. Saves typing
		2. **It is not a good practice to use \* when we embed SQL statements in application code like Python, Java, Node.js, or PHP because:**
			1. **Database performance**: If we have a table with many columns and a lot of data, we will end up selecting all data from all columns of a table
				1. It may not be necessary to the application
		2. **Application performance**: Retrieving unnecessary data from database increases traffic between database server and application server
			1. Application might become slower to respond and less scalable
		3. Solution: **Explicitly specify column names in** `SELECT` **clause whenever possible to get only necessary data from database**

##### Using PostgreSQL SELECT Statement with Expressions Example #####
1. Returning full names and emails of all customers:

		SELECT
			first_name || ' ' || last_name,
			email
		FROM
			customer;
			
	1. Concatenation operator: [https://www.postgresqltutorial.com/postgresql-concat-function/](https://www.postgresqltutorial.com/postgresql-concat-function/)
		1. It is used to concatenate first_name, space, and last name of every customer
	2. Column aliases can be used to name expressions

##### Using PostgreSQL SELECT Statement with Expressions Example #####
1. `SELECT` statement with expression

		SELECT 5 * 3;

### Column aliases - Learn how to assign temporary names to columns or expressions in a query ###
1. Column aliases are used to asign temporary names to columns in queries

#### Introduction to the PostgreSQL Column Aliases ####
1. Allows assigning a temporary name to a column or expression in a `SELECT` statement
	1. Column alias exists temporarily during the execution of a query
2. Syntax:

		SELECT column_name AS alias_name
		FROM table_name;
		
	1. `AS` **keyword is optional**
		1. It can be omitted
		
				SELECT column_name alias_name
				FROM table_name;
				
	2. Alias for expression in a `SELECT` clause:
	
			SELECT expression AS alias_name
			FROM table_name;

#### PostgreSQL Column Alias Examples ####
1. Using `customer` table from sample database:

		customer:
			*customer_id
			store_id
			first_name
			last_name
			email
			address_id
			activebool
			create_date
			last_update
			active

#### Assigning a Column Alias to a Column Example ####
1. Return `first_name` and `last_name` of all customers from `customer` table:

		SELECT
			first_name,
			last_name
		FROM
			customer;
			
	1. Assigning a new name to `last_name` column
	
			SELECT
				first_name,
				last_name AS surname
			FROM
				customer;
				
		1. Shorter version:
		
				SELECT
					first_name,
					last_name surname
				FROM
					customer;

#### Assigning a Column Alias to an Expression Example ####
1. Assigning an alias to expression:

		SELECT
			first_name || ' ' || last_name AS full_name
		FROM
			customer;

#### Column Aliases that Contain Spaces ####
1. If column aliases contain spaces, surround it with double quotes:

		column_name AS "column alias"
		
2. Example:

		SELECT
			first_name || ' ' || last_name AS "full name"
		FROM
			customer;
			
### PostgreSQL ORDER BY: Guide you on how to sort the result set returned from a query ###
1. How to sort result set returned from `SELECT` statement using **PostgreSQL ORDER BY** clause

#### Introduction to PostgreSQL ORDER BY Clause ####
1. `SELECT` statement returns rows in an un-specified order
	1. `ORDER BY` is used in a `SELECT` statement to sort the rows of the result set
2. `ORDER BY` allows us to sort rows returned by `SELECT` clause in ascending or descending order based on sort expression
3. Syntax of `ORDER BY`:

		SELECT
			select_list
		FROM
			table_name
		ORDER BY
			sort_expression1 [ASC | DESC],
			sort_expression2 [ASC | DESC],
			...
			sort_expressionN [ASC | DESC];
			
	1. sort_expressioni - it can be a column or an expression that we want to sort
	2. To sort result set based on multiple columns or expressions, place a `,` between two columns or expressions to separate them
	3. `ASC` - to sort rows in ascending order
		1. Default (if omitted)
	4. `DESC` - to sort rows in descending order
4. Evaluation order:

		FROM -> SELECT -> ORDER BY
		
	1. Based on the order of evaluation, if we have a column alis in `SELECT` clause, we can use it in `ORDER BY` clause

#### PostgreSQL ORDER BY Examples ####
1. `customer` table is used

#### Using PostgreSQL ORDER BY Clause to Sort Rows by One Column ####
1. Sort customers by their first names in ascending order:

		SELECT
			first_name,
			last_name
		FROM
			customer
		ORDER BY
			first_name ASC;
			
	1. `ASC` can be omitted:
	
			SELECT
				first_name,
				last_name
			FROM
				customer
			ORDER BY
				first_name;

#### Using PostgreSQL ORDER BY Clause to Sort Rows by One Column in Descending Order ####
1. Sort rows by values in the last name in descending order

		SELECT
			first_name,
			last_name
		FROM
			customer
		ORDER BY
			last_name DESC;

#### Using PostgreSQL ORDER BY Clause to Sort Rows by Multiple Columns ####
1. Sort rows by first name in ascending order and last name in descending order:

		SELECT
			first_name,
			last_name
		FROM
			customer
		ORDER BY
			first_name ASC,
			last_name DESC;

#### Using PostgreSQL ORDER BY Clause to Sort Rows by Expressions ####
1. `LENGTH()` function accepts a string and retrns the length of that string.
2. Select first names and their lengths and sort the rows by lengths of first names:

		SELECT
			first_name,
			LENGTH(first_name) len
		FROM
			customer
		ORDER BY
			len DESC;
			
	1. `ORDER BY` is executed after `SELECT` clause and hence, `len` is available in `ORDER BY` clause

#### PostgreSQL ORDER BY Clause and NULL ####
1. `NULL` - indicates missing data or data is not known at the time of recording
2. Handling `NULL`s while sorting rows:
	1. When we sort rows that contains `NULL`, we can specify the order of `NULL` with other non-null values using:
		1. `NULLS FIRST` **(M)** or
		2. `NULLS LAST` **(M)**
			1. In `ORDER BY` clause
3. Syntax:

		ORDER BY sort_expression [ASC | DESC] [NULLS FIRST | NULLS LAST]
		
	1. `NULLS FIRST` - places `NULL` before other non-null values
	2. `NULLS LAST` - places `NULL` after other non-null values
4. Creation of a table for demo:

		-- create a new table
		CREATE TABLE sort_demo (
			num INT
		);
		
		-- insert some data
		INSERT INTO sort_demo (num)
		VALUES (1), (2), (3), (null);
		
5. Query to return data from the `sort_demo` table:

		SELECT num
		FROM sort_demo
		ORDER BY num;
		
	1. Places `NULL` after other values
		1. `NULLS LAST` option is default for `ASC`
	2. The following query returns the same result:
	
			SELECT num
			FROM sort_demo
			ORDER BY num ASC NULLS LAST;
			
6. Placing `NULL` before other non-null values:

		SELECT
			num
		FROM
			sort_demo
		ORDER BY
			num ASC NULLS FIRST;
			
7. Sorting in descending order:

		SELECT num
		FROM sort_demo
		ORDER BY num DESC;
		
	1. `NULLS FIRST` is default for `DESC`
8. Putting `NULLS` last when sorting in `DESC` order:

		SELECT num
		FROM sort_demo
		ORDER BY num DESC NULLS LAST;

### Select Distinct - Provide you with a clause that removes duplicate rows in the result set ###
1. `SELECT DISTINCT` clause
	1. It is used to remove duplicate rows from a result set returned by a query

#### Introduction to PostgreSQL SELECT DISTINCT Clause ####
1. `DISTINCT` clause is used in `SELECT` statement to remove duplicate rows from a result set
	1. It keeps one row for each group of duplicates
	2. It can be applied to one or more columns in a select list of `SELECT` statement
2. Syntax:

		SELECT
			DISTINCT column1
		FROM
			table_name;
			
	1. the values of `column1` are used to evaluate the duplicate
3. **If multiple columns are specified** `DISTINCT` **will evaluate the duplicate based on the combination of values of those columns**

		SELECT
			DISTINCT column1, column2
		FROM
			table_name;
			
	1. `DISTINCT ON (expression)` **(M)**
		1. Used to keep the "first" row of each group of duplicates
		2. Syntax:
		
				SELECT
					DISTINCT ON (column1) column_alias,
					column2
				FROM
					table_name
				ORDER BY
					column1,
					column2;
					
			1. Problem: Since order of rows returned by `SELECT` is unspecified, "first" row of each group of duplicates is also unspecified
				1. Solution: Use `ORDER BY` with `DISTINCT ON (expression)` to make the result set predictable
					1. `DISTINCT ON` expression must match the leftmost expression in `ORDER BY` clause

#### PostgreSQL SELECT DISTINCT Examples ####
1. New table: `distinct_demo`
	1. Insert data into it for practicing `DISTINCT` clause
	2. Code:
	
			CREATE TABLE distinct_demo (
				id serial NOT NULL PRIMARY KEY,
				bcolor VARCHAR,
				fcolor VARCHAR
			);
			
			INSERT INTO distinct_demo (bcolor, fcolor)
			VALUES
				('red', 'red'),
				('red', 'red'),
				('red', NULL),
				(NULL, 'red'),
				('red', 'green'),
				('red', 'blue'),
				('green', 'red'),
				('green', 'blue'),
				('green', 'green'),
				('blue', 'red'),
				('blue', 'green'),
				('blue', 'blue');
				
	3. Query data:
	
			SELECT
				id,
				bcolor,
				fcolor
			FROM
				distinct_demo;

#### PostgreSQL DISTINCT One Column Example ####
1. Select unique values in `bcolor` column from `distinct_demo` table and sort the result set in alphabetical order using `ORDER BY` clause

		SELECT
			DISTINCT bcolor
		FROM
			distinct_demo
		ORDER BY
			bcolor;

#### PostgreSQL DISTINCT Multiple Columns ####
1. Using `DISTINCT` clause on multiple columns:

		SELECT
			DISTINCT bcolor,
			fcolor
		FROM
			distinct_demo
		ORDER BY
			bcolor,
			fcolor
			
	1. Since both `bcolor` and `fcolor` were specified in `SELECT DISTINCT` clause, both were combined to evaluate uniqueness of the rows
		1. Query returns the unique combinations of `bcolor` and `fcolor` from `distinct_demo` table

#### PostgreSQL DISTINCT ON Example ####
1. Sort result set by `bcolor` and `fcolor` and for each group of duplicates, keep first row in the returned result set.

		SELECT
			DISTINCT ON (bcolor) bcolor,
			fcolor
		FROM
			distinct_demo
		ORDER BY
			bcolor,
			fcolor;

### PostgreSQL WHERE ###
1. How to use PostgreSQL `WHERE` clause to filter rows returned by `SELECT` statement
	1. `SELECT` statement by default returns all rows from one or more columns in a table
		1. To select rows that satisfy a specified condition, use `WHERE` clause

#### PostgreSQL WHERE Clause Overview ####
1. Syntax:

		SELECT select_list
		FROM table_name
		WHERE condition
		ORDER BY sort_expression
		
	1. `WHERE` clause appears after `FROM` clause of `SELECT` statement
		1. It is used to filter the rows returned from `SELECT` clause
	2. `condition` must evaluate to true, false or unknown
		1. It can be a boolean expression or a combination of boolean expressions using `AND` and `OR` operators
		2. Query returns only the rows that satisfy the `condition` in the `WHERE` clause
			1. Only the rows that cause `condition` to be `true` will be included in the result set
2. Evaluation order:
		
		FROM -> WHERE -> SELECT -> ORDER BY
		
	1. If column aliases are used in `SELECT` clause, they cannot be used in the `WHERE` clause
	2. `WHERE` clause can also be used in `UPDATE` and `DELETE` statements
		1. It specifies the rows to be updated or deleted
3. The following comparison and logical operators are used to form the condition in the `WHERE` clause:
	1. `=` - Equal
	2. `>` - Greater than
	3. `<` - Less than
	4. `>=` - Greater than or equal
	5. `<=` - Less than or equal
	6. `<>`, `!=` - Not equal
	7. `AND` - Logical operator AND
	8. `OR` - Logical operator OR
	9. `IN` - Return true if the value matches any value in a list
	10. `BETWEEN` - Return true if the value is in a range of values
	11. `LIKE` - Return true if a value matches a pattern
	12. `IS NULL` **(M)** - Return true if the value is NULL
	13. `NOT` **(M)** - Negate the result of other operators

#### PostgreSQL WHERE Clause Examples ####
1. Using `customer` table from sample database

#### Using WHERE Clause With the Equal (=) Operator Example ####
1. Return customers whose first name is `Jemie`:

		SELECT
			first_name,
			last_name
		FROM
			customer
		WHERE
			first_name = 'Jamie';

#### Using WHERE Clause with the AND Operator Example ####
1. Return customers whose first name is `Jemie` and last name is `Rice`:

		SELECT
			first_name,
			last_name
		FROM
			customer
		WHERE
			first_name = 'Jamie' AND
			last_name = 'Rice';

#### Using the WHERE Clause with the OR Operator Example ####
1. Return customers whose last name is `Rodriquez` or first name is `Adam`:

		SELECT
			first_name,
			last_name
		FROM
			customer
		WHERE
			first_name = 'Adam' OR
			last_name = 'Rodriquez';

#### Using the WHERE Clause with the IN Operator Example ####
1. `IN` - is used to match any string in a list
2. Example: Return customers whose first name is `Ann`, or `Anne` or `Annie`;

		SELECT
			first_name,
			last_name
		FROM
			customer
		WHERE
			first_name IN ('Ann', 'Anne', 'Annie');

#### Using the WHERE Clause with the LIKE Operator Example ####
1. `LIKE` - is used to find strings that match a specified pattern
2. Example: Return all customers whose first names match with `Ann`

		SELECT
			first_name,
			last_name
		FROM
			public.customer
		WHERE
			first_name LIKE 'Ann%';
			
	1. `%` - wildcard that matches any string
		1. `Ann%` matches any string that starts with `Ann`

#### Using the WHERE Clause with the BETWEEN Operator Example ####
1. Find customers whose first names start with the letter `A` and contains 3 to 5 characters:

		SELECT
			first_name,
			last_name
			LENGTH(first_name) name_length
		FROM
			customer
		WHERE
			first_name LIKE 'A%' AND
			LENGTH(first_name) BETWEEN 3 AND 5;
		ORDER BY
			name_length;

#### Using the WHERE Clause with the Not Equal Operator (<>) Example ####
1. Find customers whose first name starts with `Bra` and last names are not `Motley`:

		SELECT
			first_name,
			last_name
		FROM
			customer
		WHERE
			first_name LIKE 'Bra%' AND
			last_name <> 'Motley';
			
	1. `<>` and `!=` are equivalent

## PostgreSQL LIMIT ##
1. `LIMIT` - used to get a subset of rows generated by a query

### Introduction to PosgreSQL LIMIT Clause ###
1. `LIMIT` - optional clause of `SELECT` statement
2. It constrains the number of rows returned by a query
3. Syntax:

		SELECT select_list
		FROM table_name
		ORDER BY sort_expression
		LIMIT row_count
		
	1. The statement returns `row_count` number of rows generated by the query
		1. If `row_count` is 0, query returns an empty set
		2. If `row_count` is `NULL`, query returns the same set that it would have without the `LIMIT` clause
4. `OFFSET` - used to skip a number of rows before returning `row_count` rows

		SELECT select_list
		FROM table_name
		LIMIT row_count OFFEST row_to_skip;
		
	1. First `row_to_skip` rows are skipped
	2. Then `row_count` rows are returned

### PostgreSQL LIMIT Examples ###
1. Using `film` table:

		film:
			*film_id
			title
			description
			release_year
			language_id
			rental_duration
			rental_rate
			length
			replacement_cost
			rating
			last_update
			special_features
			fulltext

### Using PostgreSQL LIMIT to Constrain the Number of Returned Row Example ###
1. Return first five films sorted by `film_id`

		SELECT
			film_id,
			title
			release_year
		FROM
			film
		ORDER BY
			film_id
		LIMIT 5;

### Using PostgreSQL LIMIT with OFFSET Example ###
1. Retrieve 4 films starting from 4th one ordered by `film_id`

		SELECT
			film_id,
			title,
			release_year
		FROM
			film
		ORDER BY
			film_id
		LIMIT 4 OFFSET 3;

### Using PostgreSQL LIMIT OFFSET to Get Top/ Bottom N Rows ###
1. `LIMIT` is often used to select highest or lowest values from a table
	1. Example: Get top 10 most expensive films in terms of rental
	
			SELECT
				film_id,
				title,
				rental_rate
			FROM
				film
			ORDER BY
				rental_rate DESC
			LIMIT 10;

## PostgreSQL FETCH ##
1. `FETCH` is used to retrieve a portion of rows returned by a query

### Introduction to PostgreSQL FETCH Clause ###
1. `LIMIT` is used by many relational database management systems
	1. MySQL
	2. H2
	3. HSQLDB
2. `LIMIT` is not SQL-standard
3. `FETCH` clause is SQL standard (introduced in SQL:2008)
	1. PostgreSQL supports `FETCH` clause to retrieve a number of rows returned by a query
4. Syntax:

		OFFSET start { ROW | ROWS }
		FETCH { FIRST | NEXT } [row_count] { ROW | ROWS } ONLY
		
	1. `ROW` is synonym for `ROWS`
	2. `FIRST` is synonym for `NEXT`
		1. They can be used interchangeably
	3. `start` - integer that must be >= 0.
		1. 0 is default if `OFFSET` clause is not specified
		2. If it is > number of rows in the result set, no rows are returned
	4. `row_count` is >= 1
		1. 1 is default if we do not specify explicity
5. Use `FETCH` clause with `ORDER BY` clause because the order of rows stored in table is unspecified
6. `OFFSET` clause must come before the `FETCH` clause in SQL:2008
	1. **The clauses can appear in any order in PostgreSQL**

### FETCH vs. LIMIT ###
1. `FETCH` is functionally equivalent to `LIMIT`
	1. Use `FETCH` to make the query compatible with other databases because it is standard SQL

### PostgreSQL FETCH Examples ###
1. Using `film` table:
2. Fetch first film sorted by titles in ascending order:

		SELECT
			film_id,
			title
		FROM
			film
		ORDER BY title
		FETCH FIRST ROW ONLY;
		
		OR
		
		SELECT
			film_id,
			title
		FROM
			film
		ORDER BY title
		FETCH FIRST 1 ROW ONLY;
		
3. Select first five films sorted by titles:

		SELECT
			film_id,
			title
		FROM
			film
		ORDER BY
			title
		FETCH FIRST 5 ROWS ONLY;
		
4. Select next 5 films after the first 5 films sorted by titles:

		SELECT
			film_id,
			title
		FROM
			film
		ORDER BY
			title
		OFFSET 5 ROWS
		FETCH NEXT 5 ROWS ONLY;

## PostgreSQL IN ##
1. Using `IN` operator in a `WHERE` clause to check if a value matches any value in a list.

### PostgreSQL IN Operator Syntax ###
1. Syntax:

		value IN (value1, value2, ...)
		
	1. `IN` operator returns true if `value` matches any value in the list (`value`, `value2`, ...)
2. List:
	1. It can be a list of literal values (numbers, strings, ...)
	2. It can be a result of a `SELECT` statement
	
			value IN (SELECT column_name FROM table_name);
			
		1. The query inside the parantheses is called a subquerry ([subquerry](https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-subquery/))
			1. A query nested inside another query

### PostgreSQL IN Operator Examples ###
1. To know rental information of customer id 1 and 2, we can use the `IN` operator in the `WHERE` clause:

		SELECT
			customer_id,
			rental_id,
			return_date
		FROM
			customer
		WHERE
			customer_id IN (1, 2)
		ORDER BY
			return_date DESC;
			
2. Using `=` and `OR` operator instead of `IN`

		SELECT
			customor_id,
			rental_id,
			return_date
		FROM
			customer
		WHERE
			customer_id = 1 OR customer_id = 2
		ORDER BY
			return_date DESC;
			
	1. Query that uses `IN` operator is shorter and more readable than query that uses `=` and `OR` operator.
		1. **PostgreSQL executes a query with IN operator much faster than the same query that uses a list of OR operators**

### PostgreSQL NOT IN Operator ###
1. We can combine `IN` operator with `NOT` operator to select rows whose values do not match the values in the list.
2. Example: Find all rentals with the customer id not 1 or 2

		SELECT
			customer_id,
			rental_id,
			return_date
		FROM
			rental
		WHERE
			customer_id NOT IN (1, 2);
			
3. Query without `NOT IN`:

		SELECT
			customer_id,
			rental_id,
			return_date
		FROM
			rental
		WHERE
			customer_id <> 1 AND
			customer_id <> 2;

### PostgreSQL IN With a Subquery ###
1. Return a list of customer ids from `rental` table with return date equal to `2005-05-27`

		SELECT customer_id
		FROM rental
		WHERE CAST (return_date AS DATE) = '2005-05-27'
		ORDER BY customer_id;
		
	1. `CAST` - [https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-cast/](https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-cast/)
		1. Converts a value of one type to another
		2. Syntax:
		
				CAST ( expression AS target_type );
				
			1. `expression` - constant, table column, expression that evaluates to a value
			2. `target_type` - data type to convert the expression to
			
2. The result can be used as input of `IN` operator because the query returns a list of values

		SELECT
			customer_id,
			first_name,
			last_name
		FROM
			customer
		WHERE
			customer_id IN (
				SELECT customer_id
				FROM rental
				WHERE CAST (return_date AS DATE) = '2005-05-27'
			)
		ORDER BY customer_id;
		
3. [Subquery](https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-subquery/)

## PostgreSQL BETWEEN ##
1. `BETWEEN` operator is used to match a value between a range of values.

### Introduction to the PostgreSQL BETWEEN Operator ###
1. `BETWEEN` operator is used to match a value between a range of values
2. Syntax:

		value BETWEEN low AND high;
		
	1. If `value` is greater than or equal to `low` value and less than or equal to `high` value, expression returns true, otherwise, it returns false
	2. The above can be written using `>=` and `<=` operators
	
			value >= low AND value <= high
			
	3. `NOT BETWEEN` - to check if value is outside a range
	
			value NOT BETWEEN low AND high;
			
		1. Another way to write the expression:
		
				value < low AND value > high;
				
3. Use-case: `BETWEEN` is used in `WHERE` clause of `SELECT`, `UPDATE`, `INSERT`, and `DELETE` statements

### PostgreSQL BETWEEN Operator Examples ###
1. Payment table:

		payment
			*payment_id
			customer_id
			staff_id
			rental_id
			amount
			payment_date
			
2. Use `BETWEEN` operator to select payments whose amount is between 8 and 9 (USD):

		SELECT
			customer_id
			payment_id
			amount
		FROM
			payment
		WHERE
			amount BETWEEN 8 AND 9;
			
3. Payments not in the range of 8 and 9 USD:

		SELECT
			customer_id,
			payment_id,
			amount
		FROM
			payment
		WHERE
			amount NOT BETWEEN 8 AND 9;
			
4. Date ranges:
	1. Need to use literal dates in ISO 8601 format: `YYYY-MM-DD`
		1. Get payment whose payment date is between `2007-02-07` and `2007-02-15`
		
				SELECT
					customer_id,
					payment_id,
					amount,
					payment_date
				FROM
					payment
				WHERE
					payment_date BETWEEN '2007-02-07' AND '2007-02-15';

## PostgreSQL LIKE ##
1. `LIKE` and `ILIKE` operators:
	1. Used to query data using pattern matching

### Introduction to PostgreSQL LIKE Operator ###
1. Scenario: Finding a customer whose name is not known exactly but it is known to start with `Jen`
	1. One solution: Fetch all customers and check if first name starts with `Jen`
		1. Time-consuming if customer table has large number of rows
	2. Another solution: Using `LIKE` operator
	
			SELECT
				first_name,
				last_name
			FROM
				customer
			WHERE
				first_name LIKE 'Jen%';
				
		1. `Jen%` is called a pattern
		2. Pattern matching: Query returns rows whose values in the first_name column begin with `Jen` and be followed by any sequence of characters
			1. A pattern is formed by combining literal values with wildcard characters and using `LIKE` or `NOT LIKE` operator to find matches.
		3. PostgreSQL provides 2 wildcards:
			1. `%` - matches any sequence of zero or more characters
			2. `_` - matches any single character
2. Syntax:
	1. `LIKE` operator:
	
			value LIKE pattern
			
		1. Returns `true` if `value` matches `pattern`
	2. `NOT LIKE` operator:
	
			value NOT LIKE pattern
			
		1. Returns `ture` if `value` does not match `pattern`
	3. If `pattern` does not contain any wildcard characters, `LIKE` behaves like `=` operator

### PostgreSQL LIKE Operator - Pattern Matching Examples ###
1. Examples of `LIKE` operator

#### Simple PostgreSQL LIKE Examples ####
1. Following example:

		SELECT
			'foo' LIKE 'foo', -- true
			'foo' LIKE 'f%', -- true
			'foo' LIKE '_o_', -- true
			'bar' LIKE 'b_'; -- false
			
2. Wildcards can be used at the beginning and/or end of the pattern
	1. Example: Return customers whose first name contains `er` substring
	
			SELECT
				first_name,
				last_name
			FROM
				customer
			WHERE
				first_name LIKE '%er%'
			ORDER BY
				first_name;
				
3. Combining `%` with `_`:

		SELECT
			first_name,
			last_name
		FROM
			customer
		WHERE
			first_name LIKE '_her%'
		ORDER BY
			first_name;
			
	1. Matches any string that begins with any single characer (`_`) and followed by the literal `her` and is ended with any number of characters
		1. Example outputs: `Cheryl`, `Sherri`, `Sherry`, and `Therasa`

#### PostgreSQL NOT LIKE Examples ####
1. Using `NOT LIKE` operator to find customers whose first names do not begin with `Jen`:

		SELECT
			first_name,
			last_name
		FROM
			customer
		WHERE
			first_name NOT LIKE 'Jen%'
		ORDER BY
			first_name;

### PostgreSQL Extensions of LIKE Operator ###
1. `ILIKE` operator: Matches value case-insensitively
2. Example:

		SELECT
			first_name,
			last_name
		FROM
			customer
		WHERE
			first_name ILIKE 'BAR%';

	1. `BAR%` matches any string that begins with `BAR`, `Bar`, `bar`, etc.
		1. `LIKE` will not return any row
3. Operators provided by PostgreSQL that act like `LIKE`, `NOT LIKE`, `ILIKE` and `NOT ILIKE`:
	1. `~~` - `LIKE`
	2. `~~*` - `ILIKE`
	3. `!~~` - `NOT LIKE`
	4. `!~~*` - `NOT ILIKE`
	
## PostgreSQL IS NULL ##
1. `IS NULL` **(M)** - used to check if value is `NULL` or not.

### Introduction to NULL and IS NULL Operator ###
1. `NULL` **means missing information** / **not applicable**
	1. `NULL` is not a value
		1. Hence, it cannot be used to compare with any other value like numbers or strings
2. Comparison of `NULL` with a value will result in `NULL` - unknown result
3. `NULL` is not equal to `NULL`

		NULL = NULL -- Returns NULL
		
4. Let us assume that we have `contacts` table that stores first_name, last_name, email, and phone_number of contacts
	1. At the time of recording, we may not know the phone number
		1. This is dealt with by defining `phone` collumn as nullable and insert `NULL` into `phone` column when we save the contact info
		
				CREATE TABLE contacts (
					id INT GENERATED BY DEFAULT AS IDENTITY,
					first_name VARCHAR(50) NOT NULL,
					last_name VARCHAR(50) NOT NULL,
					email VARCHAR(255) NOT NULL,
					phone VARCHAR(15),
					PRIMARY KEY (id)
				);
				
			1. If error, PostgreSQL version may not support [identity column](https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-identity-column/) column.
		2. Inserting contacts:
		
				INSERT INTO contacts (first_name, last_name, email, phone)
				VALUES ('John', 'Doe', 'john.doe@exampl.com', NULL),
					('Lily', 'Bush', 'lily.bush@example.com', '(408-234-2764)');
					
			1. To find contact who does not have phone number:
			
					SELECT
						id,
						first_name,
						last_name,
						email,
						phone
					FROM
						contacts
					WHERE
						phone = NULL;
						
				1. No row is returned
					1. `phone = NULL` always returns false
						1. Because `NULL` is not a value and it is not equal to itself
			2. Solution: We need to use `IS NULL` **(M)** instead
			
					value IS NULL
					
			3. To get contact who does not have a phone number:
			
					SELECT
						id,
						first_name,
						last_name,
						email,
						phone
					FROM
						contacts
					WHERE
						phone IS NULL;

### PostgreSQL IS NOT NULL Operator ###
1. To check if value is not `NULL`. Use `IS NOT NULL` **(M)** operator:
	1. expression returns `true` if value is not `NULL`
	2. expression returns `false` if value is `NULL`
	
2. Return contacts which have phone number:

		SELECT
			id,
			first_name,
			last_name,
			email,
			phone
		FROM
			contacts
		WHERE
			phone IS NOT NULL;

## PostgreSQL Joins ##
1. Various kinds of PostgreSQL joins
	1. Inner join
	2. Left join
	3. Right join
	4. Full outer join
2. Join: used to combine columns from one (self-join) or more tables based on values of common columns between related tables
	1. Common columns: typically primary key columns of first table and foreign key columns of second table
	2. Types of join:
		1. **inner join**
		2. **left join**
		3. **right join**
		4. **full outer join**
		5. **cross join**
		6. **natural join**

### Setting up Sample Tables ###
1. Example: Two tables called `basket_a` and `backet_b` that store fruts:

		CREATE TABLE basket_a (
			a INT PRIMARY KEY,
			fruit_a VARCHAR (100) NOT NULL
		);
		
		CREATE TABLE basket_b (
			b INT PRIMARY KEY,
			fruit_b VARCHAR (100) NOT NULL
		);
		
		INSERT INTO basket_a (a, fruit_a)
		VALUES
			(1, 'Apple'),
			(2, 'Orange'),
			(3, 'Banana'),
			(4, 'Cucumber');
			
		INSERT INTO basket_b (b, fruit_b)
		VALUES
			(1, 'Orange'),
			(2, 'Apple'),
			(3, 'Watermelon'),
			(4, 'Pear');
			
	1. Tables have common fruits: `appled`, and `orange`

### PostgreSQL Inner Join ###
1. Following statement joins first table `basket_a` with second table `basket_b` by matching values in `fruit_a` and `fruit_b` columns:

		SELECT
			a,
			fruit_a,
			b,
			fruit_b
		FROM
			basket_a
		INNER JOIN basket_b
			ON fruit_a = fruit_b;
			
	1. Inner join examines each row in first table (`basket_a`)
	2. It compares the value in `fruit_a` column with value in `fruit_b` column of each row in second table (`basket_b`)
	3. If values are equal, it constructs a new row that contains columns from both tables
	4. It adds the new row to the result set

### PostgreSQL Left Join ###
1. Left join is used to join `basket_a` table with `basket_b` table
	1. First table is called the left table (in this context)
	2. Second table is called the right table (in this context)
2. Example:

		SELECT
			a,
			fruit_a,
			b,
			fruit_b
		FROM
			basket_a
		LEFT JOIN basket_b
			ON fruit_a = fruit_b;
			
3. Steps:
	1. It starts selecting data from left table
	2. It compares values in `fruit_a` column with values in `fruit_b` column in `basket_b` table
	3. If values are equal, a new row is created that contains columns from both tables
	4. It adds the new row to the result set
	5. If values do not equal, a new row is created that contains columns from both tables
	6. It fills the columns of the right table (`basket_b`) with `NULL`
4. To select rows from the left table that do not have matching rows in the right table. Use left join with `WHERE` clause

		SELECT
			a,
			fruit_a,
			b,
			fruit_b
		FROM
			basket_b
		LEFT JOIN basket_b
			ON fruit_a = fruit_b
		WHERE b IS NULL;
		
	1. Only rows that do not have matching rows in the right table are selected
5. `LEFT JOIN` is the same as `LEFT OUTER JOIN`

### PostgreSQL Right Join ###
1. Right join is a reversed version of left join
2. Steps:
	1. It starts selecting data from right table
	2. It compares each value in `fruit_b` column of every row in the right table with each value in `fruit_a` column of every row in the left table
	3. If values are equal, a new row is created that contains columns from both tables
	4. If values are not equal, a new row is created that contains columns from both tables
	5. In the case of no match, the columns in the left table are filled with `NULL`
3. Example:

		SELECT
			a,
			fruit_a,
			b,
			fruit_b
		FROM
			basket_a
		RIGHT JOIN basket_b
			ON fruit_a = fruit_b;
			
4. To get rows from the right table that do not have matching rows from the left table:

		SELECT
			a,
			fruit_a,
			b,
			fruit_b
		FROM
			basket_a
		RIGHT JOIN basket_b
			ON fruit_a = fruit_b
		WHERE
			a IS NULL;
			
5. `RIGHT JOIN` and `RIGHT OUTER JOIN` are the same

### PostgreSQL Full Outer Join ###
1. The full outer join returns a result set that contains all rows from both left and right tables with matching rows from both sides if available. If there are not matching rows, the corresponding columns of both tables will be filled with `NULL`
2. Example:

		SELECT
			a,
			fruit_a,
			b,
			fruit_b
		FROM
			basket_a
		FULL OUTER JOIN basket_b
			ON fruit_a = fruit_b;
			
3. To return rows that do not have matching rows in the other

		SELECT
			a,
			fruit_a,
			b,
			fruit_b
		FROM
			basket_a
		FULL OUTER JOIN basket_b
			ON fruit_a = fruit_b
		WHERE
			a IS NULL OR b IS NULL;
			
4. PostgreSQL Joins:

	[PostgreSQL-Joins.png](PostgreSQL-Joins.png)

## PostgreSQL Table Aliases ##
1. Aliases and their practical applications

### Introduction to the PostgreSQL Table Aliases ###
1. Table aliases: Temporarily assigned new names to tables during the execution of a query
2. Syntax:

		table_name AS alias_name;
		
	1. `table_name` is assigned an alias as `alias_name`
		1. `AS` keyword is optional
		
				table_name alias_name;

### Practical Applications of Table Aliases ###
#### Using Table Aliases for the Long Table Name to Make Queries More Readable ####
1. Scenario: If we want to qualify a column name with a long table name, we can use a table alias:

		a_very_long_table_name.column_name
		
	1. We can asign an alias:
	
			a_very_long_table_name AS alias
			
	2. Then use the alias instead of the long table name:
	
			alias.column_name

#### Using Table Aliases in Join Clauses ####
1. If we have the same column names in the tables we are joining, we need to use a fully qualified name to differentiate between the columns as follows:

		table_name.column_name
		
	1. If the table name is too long, we can use an alias instead in `FROM` and `INNER JOIN` clauses
	
			SELECT
				c.customer_id,
				first_name,
				amount,
				payment_date
			FROM
				customer c
			INNER JOIN payment p
				ON p.customer_id = c.customer_id
			ORDER BY
				payment_date DESC;

#### Using Table Aliases in Self-Join ####
1. [self-join](https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-self-join/) needs table aliases
	1. Referencing the same table multiple times within a query results in error (there is no distinction)
	2. Referencing `employee` table twice in the same query using table aliases:
	
			SELECT
				e.first_name employee,
				m.first_name manager
			FROM
				employee e
			INNER JOIN employee m
				ON m.employee_id = e.manager_id
			ORDER BY manager;
			
		1. We are refering to `employee` table twice in the above query

## PostgreSQL INNER JOIN ##
1. Selecting data from multiple tables using PostgreSQL `INNER JOIN` clause

### Introduction to PostgreSQL INNER JOIN Clause ###
1. In RDBMS, data is typically distributed in more than one table
	1. To select complete data, we often need to query data from multiple tables
2. `INNER JOIN` clause is used to combine data from multiple tables
3. Example: Consider tables A and B
	1. pka column in A matches fka column in B
	2. To select data from both tables, we use `INNER JOIN` clause in the `SELECT` statement
	
			SELECT
				pka,
				c1,
				pkb,
				c2
			FROM
				A
			INNER JOIN B
				ON pka = fka;
				
4. Steps to following to join `A` with table `B`:
	1. Specify columns from both tables that we want to select data in `SELECT` clause
	2. Specify main table (table `A`) in the `FROM` clause
	3. Specify second table (table `B`) in the `INNER JOIN` clause and provide a join condition after `ON` keyword
5. How `INNER JOIN` works:
	1. For each row in table `A`, inner join compares the values in `pka` column with values in `fka` column in every row in table `B`:
		1. If values are equal, inner join constructs a new row that contains all columns of both tables and adds it to result set
		2. If values are not equal, inner join ignores them and moves on to the next row
6. Most of the time, tables that we want to join will have columns with same name (`id`, `customer_id`, ...)
	1. To resolve ambiguity, we need to qualify columns fully using the following syntax:
	
			table_name.column_name
			
		1. We can use table aliases to assign joined tables short names to make query more readable

#### PostgreSQL INNER JOIN Examples ####
1. Assume the following tables:

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
			
		payment
			* payment_id
			customer_id
			staff_id
			rental_id
			amount
			payment_date
			
	1. One to many relationship exists between `customer` and `payment` tables
		1. Whenever a customer makes a payment, a new row is inserted into `payment` table
			1. Each customer may have 0 or more payments
			2. Each paymet belongs to one and only one customer
		2. `customer_id` column establishes the relationship between the two tables
	2. To select data from both tables:
	
			SELECT
				customer.customer_id,
				first_name,
				last_name,
				email,
				amount,
				payment_date
			FROM
				customer
			INNER JOIN payment
				ON payment.customer_id = customer.customer_id
			ORDER BY payment_date;
			
		1. Using table aliases:
		
				SELECT
					c.customer_id,
					first_name,
					last_name,
					email,
					amount,
					payment_date
				FROM
					customer c
				INNER JOIN payment p
					ON p.customer_id = c.customer_id
				WHERE
					c.customer_id = 2;
					
2. We can use `USING` syntax instead since both tables have the same `customer_id` column

		SELECT
			customer_id,
			first_name,
			last_name,
			amount,
			payment_date
		FROM
			customer
		INNER JOIN payment USING(customer_id)
		ORDER BY payment_date;
		
#### Using PostgreSQL INNER JOIN to Join the Three Tables ####
1. Relationship between three tables: `staff`, `payment`, and `customer`
	1. Each staff handles 0 or more payments
	2. Each payment is processed by one and only one staff
	3. Each customer made zero or more payments.
	4. Each payment is made by one customer
	
			staff
				* staff_id
				first_name
				last_name
				address_id
				email
				store_id
				active
				username
				password
				last_update
				picture
				
2. How to join three tables?
	1. Place second `INNER JOIN` clause after the first `INNER JOIN` clause:
	
			SELECT
				c.customer_id,
				c.first_name customer_first_name,
				c.last_name customer_last_name,
				s.first_name staff_first_name,
				s.last_name staff_last_name,
				amount,
				payment_date
			FROM
				customer c
			INNER JOIN payment p
				ON p.customer_id = c.customer_id
			INNER JOIN staff s
				ON s.staff_id = p.staff_id
			ORDER BY payment_date;
			
## PostgreSQL LEFT JOIN ##
1. How to use `LEFT JOIN` clause to select data from multiple tables.

### Introduction to PostgreSQL LEFT JOIN Clause ###
1. Assume we have two tables: `A` and `B`
2. Each row in `A` can have zero or many corresponding rows in table `B`
3. Each row in `B` has one and only one corresponding row in table `A`
4. To select data from table `A` that may or may not have corresponding rows in table `B`, we use `LEFT JOIN` clause
5. Syntax:

		SELECT
			pka,
			c1,
			pkb,
			c2
		FROM
			A
		LEFT JOIN B
			ON pka = fka;
			
	1. Steps:
		1. Specify columns in both tables from which we want to select data in `SELECT` clause
		2. Specify left table (table `A`) in `FROM` clause
		3. Specify right table (table `B`) in `LEFT JOIN` clause and join the condition after `ON` keyword
6. `LEFT JOIN` clause starts selecting data from left table
7. For each row in left table, it compares value in `pka` column with value of each row in `fka` column in the right table
8. If the values are equal, left join clause constructs a new row that contains columns that appear in `SELECT` clause
9. Adds the row in the result set
10. If values are not equal, left join clause constructs a new row that contains columns that appear in `SELECT` clause
11. It fills columns that come from the right table with `NULL`

### PostgreSQL LEFT JOIN Examples ###
1. Example: `film` and `inventory` tables from sample database

		film
			*film_id
			title
			description
			release_year
			language_id
			rental_duration
			rental_rate
			length
			replacement_cost
			rating
			last_update
			special_features
			fulltext
			
		inventory
			* inventory_id
			film_id
			store_id
			last_update
			
	1. Each row in `film` table may have zero or many rows in `inventory` table
	2. Each row in `inventory` table has one and only one row in `film` table
	3. `film_id` column establishes link between `film` and `inventory` tables
2. Statement using `LEFT JOIN` clause to join `film` table with `inventory` table

		SELECT
			film.film_id,
			title,
			inventory_id
		FROM
			film
		LEFT JOIN inventory
			ON film.film_id = inventory.film_id
		ORDER BY title;
		
	1. If a row from `film` table does not have a matching row in `inventory` table, value of `inventory_id` column of the row is `NULL`
	2. Using `WHERE` clause to find films that are not in inventory:
	
			SELECT
				film.film_id
				film.title
				inventory_id
			FROM
				film
			LEFT JOIN inventory
				ON inventory.film_id = film.film_id
			WHERE inventory.film_id IS NULL
			ORDER BY title;
			
	3. Using table aliases:
	
			SELECT
				f.film_id,
				title,
				inventory_id
			FROM
				film f
			LEFT JOIN inventory i
				ON i.film_id = f.film_id
			WHERE i.film_id IS NULL
			ORDER BY title;
			
	4. If both tables have same column name used on `ON` clause, we can use `USING` syntax:
	
			SELECT
				f.film_id,
				title,
				inventory_id
			FROM
				film f
			LEFT JOIN inventory i USING (film_id)
			WHERE i.film_id IS NULL
			ORDER BY title;
		
		1. Used to select rows from one table that do not have matching rows in another table
		
## PostgreSQL RIGHT JOIN ##
1. How to use PostgreSQL `RIGHT JOIN` to select data from two tables

### Setting up Sample Tables ###
1. Two tables: `films` and `film_reviews`:

		DROP TABLE IF EXISTS films;
		DROP TABLE IF EXISTS film_reviews;
		
		CREATE TABLE films (
			film_id SERIAL PRIMARY KEY,
			title varchar(255) NOT NULL
		);
		
		INSERT INTO films(title)
		VALUES ('Joker'),
			('Avengers: Endgame'),
			('Parasite');
			
		CREATE TABLE film_reviews (
			review_id SERIAL PRIMARY KEY,
			film_id INT,
			review VARCHAR(255) NOT NULL
		);
		
		INSERT INTO film_reviews(film_id, review)
		VALUES (1, 'Excellent'),
			(1, 'Awesome'),
			(2, 'Cool'),
			(NULL, 'Beautiful');
			
	1. A film can have zero or many reviews and a review belongs to zero or one film
		1. `film_id` column in `films` references the `film_id` column in the `film_reviews` table
2. Contents of the `films` and `film_reviews` tables:

		SELECT * FROM films;
		
		SELECT * FROM film_reviews;

### Introduction to PostgreSQL RIGHT JOIN Clause ###
1. Use right join to select data from `films` and `film_reviews` tables:

		SELECT
			review,
			title
		FROM
			films
		RIGHT JOIN film_reviews
			ON films.film_id = film_reviews.film_id;
			
	1. `films` is the left table and `film_reviews` is the right table
	2. `RIGHT JOIN` clause starts selecting data from the right table `film_reviews`.
	3. For each row from the right table (`film_reviews`), it checks if the value in the `film_id` column of the `films` table equals the value in the `film_id` column of every row from the left table (`film_reviews`)
	4. If they are equal, `RIGHT JOIN` constructs a new row that contains columns from both tables specified in the `SELECT` clause and includes the new row in the result set
	5. If they are not equal, `RIGHT JOIN` constructs a new row that contains columns from both tables and includes the new row in the result set. It fills the columns from the left table `films` with `NULL`
		1. The review with id 4 doesn't match any film, so `title` columns is filled with `NULL`

### PostgreSQL RIGHT JOIN with USING Syntax ###
1. Since the joined column has the same name (`film_id`), we can use the `ÙSING` syntax in the join predicate:

		SELECT review, title
		FROM films
		RIGHT JOIN film_reviews USING (film_id);

### PostgreSQL RIGHT JOIN with WHERE Clause ###
1. Find rows in the right table that does not have any corresponding rows in the left table:

		SELECT
			review,
			title
		FROM
			films
		RIGHT JOIN film_reviews USING (film_id)
		WHERE title IS NULL;

## PostgreSQL Self-Join ##
1. We can use PostgreSQL self-join technique to compare rows within the same table

### Introduction to PostgreSQL Self-Join ###
1. Self-join is a regular join that joins table to itself
2. Use-cases:
	1. To query hierarchical data (?)
	2. To compare rows within the same table
3. How to use self-join?
	1. Specify same table twice with different table aliases and provide join predicate after the `ON` keyword
	2. Using inner-join:
	
			SELECT select_list
			FROM table_name t1
			INNER JOIN table_name t2 ON join_predicate;
			
	3. Using `LEFT JOIN` or `RIGHT JOIN`:
	
			SELECT select_list
			FROM table_name t1
			LEFT JOIN table_name t2 ON join_predicate;

### PostgreSQL Self-Join Examples ###
#### Querying Hierarchical Data Example ####
1. Example: Org structure:

		Windy Hays
			Hassan Conner
				Salley Lester
				Kelsie Hays
				Tory Goff
			Ava Christensen
				Sau Norman
				Anna Reeves
				
	1. `employee` table creation:
	
			CREATE TABLE employee (
				employee_id INT PRIMARY KEY,
				first_name VARCHAR(255) NOT NULL,
				last_name VARCHAR(255) NOT NULL,
				manager_id INT,
				FOREIGN KEY (manager_id)
				REFERENCES employee (employee_id)
				ON DELETE CASCADE
			);
			
			INSERT INTO employee (
				employee_id,
				first_name,
				last_name,
				manager_id
			)
			VALUES
				(1, 'Windy', 'Hays', NULL),
				(2, 'Ava', 'Christensen', 1),
				(3, 'Hassan', 'Conner', 1),
				(4, 'Anna', 'Reeves', 2),
				(5, 'Sau', 'Norman', 2),
				(6, 'Kelsie', 'Hays', 3),
				(7, 'Tory', 'Goff', 3),
				(8, 'Salley', 'Lester', 3);
				
		1. In the `employee` table, `manager_id` column references the `employee_id` column
			1. Value in `manager_id` columns shows the manager to whom the employee directly reports
			2. If value in `manager_id` column is null, employee does not report to anyone
				1. He/she is a top manager
		2. Query to find who reports to whom
		
				SELECT
					e.first_name || ' ' || e.last_name employee,
					m.first_name || ' ' || m.last_name manager
				FROM
					employee AS e
				INNER JOIN employee AS m
					ON e.manager_id = m.employee_id
				ORDER BY manager;
				
			1. Query references `employee` table twice
				1. One as employee
				2. Another as manager
			2. `e` and `m` aliases are used
			3. Join predicate finds employee/manager pair by matching values in `employee_id` and `manager_id` columns
			4. **Top manager does not appear in the output**
				1. Solution: Use `LEFT JOIN` instead of `INNER JOIN`
				
						SELECT
							e.first_name || ' ' || e.last_name AS employee,
							m.first_name || ' ' || m.last_name AS manager
						FROM
							employee AS e
						LEFT JOIN employee AS m
							ON e.manager_id = m.employee_id
						ORDER BY manager;

#### Comparing the Rows with the Same Table ####
1. Consider `film` table from `dvdrental` database
2. Query: Find all pair of films that have the same length

		SELECT
			f1.title,
			f2.title,
			f1.length
		FROM
			film f1
		INNER JOIN film f2
			ON f1.film_id <> f2.film_id AND
			   f1.length = f2.length;
			   
	1. `f1.film_id <> f2.film_id` matches two different films

#### Summary ####

## PostgreSQL FULL OUTER JOIN ##
1. How to use PostgreSQL `FULL OUTER JOIN` to query data from two or more tables

### Introduction to the PostgreSQL FULL OUTER JOIN ###
1. Consder two tables A and B and we want to perform full outer join of the two tables
2. The following illustrates the syntax of the `FULL OUTER JOIN`:

		SELECT * FROM A
		FULL [OUTER] JOIN B ON A.id = B.id;
		
	1. `OUTER` keyword is optional
3. **The full outer join combines the results of both left join and right join
	1. If rows in the joined table do no match, full outer join sets `NULL` values for every column of the table that doesn't have a matching row
	2. If a row matches a row in the second table, the result row will contain columns populated from columns from both tables

### PostgreSQL FULL OUTER JOIN Example ###
1. Creation of tables:

		DROP TABLE IF EXISTS departments;
		DROP TABLE IF EXISTS employees;
		
		CREATE TABLE departments (
			department_id serial PRIMARY KEY,
			department_name VARCHAR (255) NOT NULL
		);
		
		CREATE TABLE employees (
			employee_id serial PRIMARY KEY,
			employee_name VARCHAR (255),
			department_id INTEGER
		);
		
	1. Each department has zero or many employees
	2. Each employee belongs to zero or one department
2. Insert some sample data into the tables:

		INSERT INTO departments (department_name)
		VALUES
			('Sales'),
			('Marketing'),
			('HR'),
			('IT'),
			('Production');
			
		INSERT INTO employees (
			employee_name,
			department_id
		)
		VALUES
			('Bette Nicholson', 1),
			('Christian Gable', 1),
			('Joe Swank', 2),
			('Fred Costner', 3),
			('Sandra Kilmer', 4),
			('Julia Mcqueen', NULL);
			
	1. Query data from the tables:
	
			SELECT * FROM departments;
			SELECT * FROM employees;
			
3. Use `FULL OUTER JOIN` to query data from both `employees` and `departments` tables:

		SELECT
			employee_name,
			department_name
		FROM
			employees e
		FULL OUTER JOIN departments d
			ON d.department_id = e.department_id;
			
	1. The result set includes every employee who belongs to a department and every department which have an employee
	2. The result set also includes every employee who does not belong to a department
	3. The result set also includes every department who does not have an employee
4. Find departments that do not have any employees

		SELECT
			employee_name,
			department_name
		FROM
			employees e
		FULL OUTER JOIN departments d
			ON d.department_id = e.department_id
		WHERE
			employee_name IS NULL;

	1. `Production` department does not have any employees
5. Find employees who do not belong to any department:
	
		SELECT
			employee_name,
			department_name
		FROM
			employees e
		FULL OUTER JOIN departments d
			ON d.department_id = e.department_id
		WHERE
			department_name IS NULL;
			
	1. `Juila Mcqeen` does not belong to any department
	
## PostgreSQL Cross Join By Example ##
1. How to use PostgreSQL `CROSS JOIN` to produce a **cartesian product** of rows from joined tables

### Introduction to the PostgreSQL CROSS JOIN Clause ###
1. **Cross-join clause does not have a predicate**
2. Let us assume that we want ot perform a `CROSS JOIN` of two tables `T1` and `T2`
	1. If `T1` has `n` rows and `T2` has `m` rows, the result set will have `n x m` rows
3. Syntax of `CROSS JOIN`:

		SELECT select_list
		FROM T1
		CROSS JOIN T2;
		
	1. Equivalent statement:
	
			SELECT select_list
			FROM T1, T2;
			
	2. Equivalent statement using `INNER JOIN`
	
			SELECT select_list
			FROM T1
			INNER JOIN T2 ON true;
			
		1. condition always evaluates to true so all joins are valid

### PostgreSQL CROSS JOIN Example ###
1. Creation of T1 and T2 tables and insertion of sample data

		DROP TABLE IF EXISTS T1;
		
		CREATE TABLE T1 (label CHAR(1) PRIMARY KEY);
		
		DROP TABLE IF EXISTS T2;
		
		CREATE TABLE T2 (score INT PRIMARY KEY);
		
		INSERT INTO T1 (label)
		VALUES
			('A'),
			('B');
			
		INSERT INTO T2 (score)
		VALUES
			(1),
			(2),
			(3);
			
	1. Using `CROSS JOIN` to join the two tables:
	
			SELECT *
			FROM T1
			CROSS JOIN T2;
			
		1. Cross join illustration:
		
			![PostgreSQL-CROSS-JOIN-illustration.png](PostgreSQL-CROSS-JOIN-illustration.png)
			
## PostgreSQL NATURAL JOIN Explained By Examples ##
1. How to use PostgreSQL `NATURAL JOIN` to query data from two or more tables
2. **Natural join constructs an implicit join based on the same column names in joined tables**
3. Syntax:

		SELECT select_list
		FROM T1
		NATURAL [INNER, LEFT, OUTER] JOIN T2;
		
	1. Natural join can be:
		1. Inner join (default if we don't specify the type)
		2. Left join
		3. Right join
4. If `*` is used in select list, the result contains:
	1. All common columns
		1. Columns from both tables that have the same name
	2. Every column from both tables, which is not a common column

### PostgreSQL NATURAL JOIN Examples ###
1. Two tables can be created: `categories`, `products`

		DROP TABLE IF EXISTS categories;
		CREATE TABLE categories (
			category_id SERIAL PRIMARY KEY,
			category_name VARCHAR (255) NOT NULL
		);
		
		DROP TABLE IF EXISTS products;
		CREATE TABLE products (
			product_id SERIAL PRIMARY KEY,
			product_name VARCHAR (255) NOT NULL,
			category_id INT NOT NULL,
			FOREIGN KEY (category_id) REFERENCES categories (category_id)
		);
		
	1. Each category has zero or many products
	2. Each product belongs to one and only one category
	3. `category_id` column in `products` table is the foreign key that references to the primary key of `categories` table
		1. Hence, `categorid_id` is the common column that we will use to perform natural join
2. Inserting values:

		INSERT INTO categories (category_name)
		VALUES
			('Smart Phone'),
			('Laptop'),
			('Tablet');
			
		INSERT INTO products (product_name, category_id)
		VALUES
			('iphone', 1),
			('Samsung Galaxy', 1),
			('HP Elite', 2),
			('Lenovo Thinkpad', 2),
			('iPad', 3),
			('Kindle Fire', 3);
			
3. Using `NATURAL JOIN` clause to join `products` and `categories` table:

		SELECT *
		FROM products
		NATURAL JOIN categories;
		
	1. The statement is equivalent to:
	
			SELECT *
			FROM products
			INNER JOIN categories USING (category_id);
			
4. Convenience: We do not need to specify the join clause (implicit join clause on common column(s))
	1. **Avoid `NATURAL JOIN` whenever possible because it sometimes may cause an unexpected result**
		1. Example: Consider the following tables
		
				city
					* city_id
					city
					country_id
					last_update
					
				country
					* country_id
					country
					last_update
					
			1. The following `NATURAL JOIN` can be used because both tables have `country_id`
			
					SELECT *
					FROM city
					NATURAL JOIN country;
					
				1. **Query returns empty result set**
					1. Reason: `last_update` exists in both tables and this is also used implicitly (and both may have different values)
					
## PostgreSQL GROUP BY ##
1. How to divide rows into groups using `GROUP BY` clause

### Introduction to PostgreSQL GROUP BY Clause ###
1. `GROUP BY` divides rows returned from `SELECT` statement into groups
2. For each group, we can **apply an aggregate function**
	1. `SUM()` to calculate sum of items
	2. `COUNT()` to get the number of items in the groups
3. Basic syntax:

		SELECT
			column_1,
			column_2,
			...,
			aggregate_function(column_3)
		FROM
			table_name
		GROUP BY
			column_1,
			column_2,
			...;
			
	1. **First select columns that we want to group and column that we want to apply an aggregate function**
		1. Columns to group: `column_1`, `column_2`
		2. Column we want to apply an aggregate function on: `column_3`
	2. **Second list the columns we want to group in the** `GROUP BY` **clause**
4. The statement clause **divides rows by the values of columns specified in the** `GROUP BY` **clause and calculates a value for each group**
5. Other clauses of `SELECT` statement with `GROUP BY` clause can be used (?)
6. Order of execution of of a query:

		FROM
		|
		v
		WHERE
		|
		v
		GROUP BY
		|
		v
		HAVING
		|
		v
		SELECT
		|
		v
		DISTINCT
		|
		v
		ORDER BY
		|
		v
		LIMIT

### PostgreSQL GROUP BY Clause Examples ###
1. Consider `payment` table in the sample database

		payment
			* payment_id
			customer_id
			staff_id
			rental_id
			amount
			payment_date

#### Using PostgreSQL GROUP BY Without an Aggregate Function Example ####
1. We can use `GROUP BY` without applying an aggregate function
	1. Example: Query `payment` table and group result by customer id
	
			SELECT
				customer_id
			FROM
				payment
			GROUP BY
				customer_id;
				
		1. **It works like the** `DISTINCT` **clause and removes duplicate rows from the result set**

#### Using PostgreSQL GROUP BY With SUM() Function Example ####
1. `GROUP BY` clause is useful when it is used in conjunction with an aggregate function
	1. Example: Select the total amount that each customer has paid (Divide the rows into groups grouped by customer id)
		1. For each group, calculate the total amount using the `SUM()` function
		
				SELECT
					customer_id,
					SUM (amount)
				FROM
					payment
				GROUP BY
					customer_id;
					
			1. `GROUP BY` sorts result set by customer id and adds up the amount that belongs to the same customer
				1. Whenever the `customer_id` changes, it adds the row to the returned result set
		2. Using `ORDER BY` clause with `GROUP BY` clause to sort the groups:
		
				SELECT
					customer_id,
					SUM (amount)
				FROM
					payment
				GROUP BY
					customer_id
				ORDER BY
					SUM (amount) DESC;

#### Using PostgreSQL GROUP BY Clause With the JOIN CLAUSE ####
1. Using `GROUP BY` clause with `INNER JOIN` clause to get the total amount paid by each customer
2. The query joins `payment` table with the `customer` table and group customers by their names:

		SELECT
			first_name || ' ' || last_name full_name,
			SUM (amount) amount
		FROM
			payment
		INNER JOIN customer USING (customer_id)
		GROUP BY
			full_name
		ORDER BY amount DESC;

#### Using PostgreSQL GROUP BY With COUNT() Function Example ####
1. To find the number of payment transactions that each staff has processed, group the rows in the `payment` table by the values in the `staff_id` column and use the `COUNT()` function to get the number of transactions:

		SELECT
			staff_id,
			COUNT (payment_id)
		FROM
			payment
		GROUP BY
			staff_id;
			
	1. `GROUP BY` divides the rows in the payment into groups and groups them by value in `staff_id` column
	2. For each group, it returns the number of rows by using `COUNT()` function

#### Using PostgreSQL GROUP BY With Multiple Columns ####
1. Using multiple columns in the `GROUP BY` clause:

		SELECT
			customer_id,
			staff_id,
			SUM (amount)
		FROM
			payment
		GROUP BY
			staff_id,
			customer_id
		ORDER BY
			customer_id;
			
	1. `GROUP BY` clause divides rows in the `payment` table by the values in `customer_id` and `staff_id` columns
	2. For each group of `(customer_id, staff_id)`, the `SUM()` calculates the total amount

#### Using PostgreSQL GROUP BY Clause With a Date Column ####
1. `payment_date` is a timestamp column
2. Use `DATE()` function to group payment by dates
	1. `DATE()` function converts timestamps to dates
	
## PostgreSQL HAVING ##
1. How to use PostgreSQL HAVING clause to specify a search condition for a group or an aggregate

### Introduction to PostgreSQL HAVING Clause ###
1. `HAVING` clause specifies a search condition for group or aggregate
	1. Often used by `GROUP BY` clause **to filter groups or aggregates based on a specified condition**
2. Syntax:

		SELECT
			column1,
			aggregate_function (column2)
		FROM
			table_name
		GROUP BY
			column1
		HAVING
			condition;
			
	1. `HAVING` clause specifies a condition to filter the groups
	2. We can also add other clauses of `SELECT` such as:
		1. `JOIN`
		2. `LIMIT`
		3. `FETCH`
		4. ...
	3. `HAVING` **clause is evaluated by the** `SELECT` clause
		1. Column aliases cannot be used
			1. They are not available in the `HAVING` clause

### HAVING vs. WHERE ###
1. `WHERE` is used to filter rows based on on a specific condition
2. `HAVING` is used **to filter groups or rows** according to a specified condition

### PostgreSQL HAVING Clause Examples ###
1. Consider `payment` table in sample database

#### Using PostgreSQL HAVING Clase with SUM Function Example ####
1. Use `GROUP BY` with `SUM()` function to find the total amount of each customer:

		SELECT
			customer_id,
			SUM (amount)
		FROM
			payment
		GROUP BY
			customer_id;
	
2. Use `HAVING` class to select only customers who have been spending more than `200`:

		SELECT
			customer_id,
			SUM (amount)
		FROM
			payment
		GROUP BY
			customer_id
		HAVING
			SUM (amount) > 200;

#### PostgreSQL HAVING Clause With COUNT Example ####
1. Consider `customer` table from the sample database
2. Get the number of customers per store:

		SELECT
			store_id,
			COUNT (customer_id)
		FROM
			customer
		GROUP BY
			store_id;
			
3. Select a store that has more than 300 customers:

		SELECT
			store_id,
			COUNT (customer_id)
		FROM
			payment
		GROUP BY
			store_id
		HAVING
			COUNT (customer_id) > 300;
			
## PostgreSQL UNION ##
1. How to use PostgreSQL UNION operator to combine result sets of multiple queries into a single result set

### Introduction to PostgreSQL UNION Operator ###
1. `UNION` operator combines result sets of two of more `SELECT` statements into a single result set
2. Syntax of `UNION` operator:

		SELECT select_list_1
		FROM table_expression_1
		UNION
		SELECT select_list_2
		FROM table_expression_2
		
	1. To combine result sets of two queries using `UNION` operator, queries must conform to the following rules:
		1. **Number and order of columns in select list of both queries must be same**
		2. **Data types must be compatible**
3. `UNION` operator removes all duplicate rows from combined data set
	1. Use `UNION ALL` to retain duplicate rows

### PostgreSQL UNION With ORDER BY Clause ###
1. `UNION` operator may place the rows from result set of first query before, after, or between the rows from the result set of second query
2. To sort rows in the final result set, use `ORDER BY` in the second query
3. Use-cases: `UNION` operator is used to combine data from similar tables which are not perfectly normalized
	1. In data warehouse or
	2. In business intelligence systems

### Setting Up Sample Tables ###
1. Creation of two tables: `top_rated_films`, and `most_popular_films`

		DROP TABLE IF EXISTS top_rated_films;
		CREATE TABLE top_rated_films (
			title VARCHAR NOT NULL,
			release_year SMALLINT
		);
		
		DROP TABLE IF EXISTS most_popular_films;
		CREATE TABLE most_popular_films (
			title VARCHAR NOT NULL,
			release_year SMALLINT
		);
		
		INSERT INTO
			top_rated_films (title, release_year)
		VALUES
			('The Shawshank Redemption', 1994),
			('The Godfather', 1972),
			('12 Angry Men', 1957);
			
		INSERT INTO
			most_popular_films (title, release_year)
		VALUES
			('An American Pickle', 2020),
			('The Godfather', 1972),
			('Greyhound', 2020);
			
2. All data from `top_rated_films`:

		SELECT * FROM top_rated_films;
		
3. All data from `most_popular_films`:

		SELECT * FROM most_popular_films;

### PostgreSQL UNION Examples ###
#### Simple PostgreSQL UNION Example ####
1. Using `UNION` operator to combine data from both tables:

		SELECT * FROM top_rated_films
		UNION
		SELECT * FROM most_popular_films;
		
	1. Duplicate row is removed

#### PostgreSQL UNION ALL Example ####
1. Using `UNION ALL` to include duplicates

		SELECT * FROM top_rated_films
		UNION ALL
		SELECT * FROM most_popular_films;

#### PostgreSQL UNION ALL With ORDER BY Clause Example ####
1. Sort the resutl returned by `UNION` operator using `ORDER BY` clause:

		SELECT * FROM top_rated_films
		UNION ALL
		SELECT * FROM most_popular_films
		ORDER BY title;
		
	1. If we place `ORDER BY` at the end of each query, the combined result set will not be sorted as we expected
		1. `UNION` operator just combines result sets from each query and soes not quarantee the order of rows in the final result set

## PostgreSQL INTERSECT Operator ##
1. How to use the PostgreSQL `INTERSECT` operator to combine result sets of two or more queries

### Introduction to PostgreSQL INTERSECT Operator ###
1. `INTERSECT` is similar to `UNION` and `EXCEPT` operators
	1. It combines result sets of two or more `SELECT` statements into a single result set
	2. **It returns any rows available in both result sets**
2. Syntax:

		SELECT select_list
		FROM A
		INTERSECT
		SELECT select_list
		FROM B;
		
	1. To use `INTERSET` operator, the columns that appear in `SELECT` statements must follow the following rules:
		1. **Number of columns are their order in** `SELECT` **must be the same**
		2. **Data types of the columns must be compatible**

### PostgreSQL INTERSECT With ORDER BY Clause ###
1. Place the `ORDER BY` at the final query in the query list:

		SELECT select_list
		FROM A
		INTERSET
		SELECT select_list
		FROM B
		ORDER BY sort_expression;
		
### PostgreSQL INTERSECT Operator Examples ###
1. Using `top_rated_films` and `most_popular_films` tables
2. Get popular films which are also top rated:

		SELECT *
		FROM top_rated_films
		INTERSECT
		SELECT *
		FROM most_popular_films;
		
	1. The result set returns films that appear in both tables.
	
## PostgreSQL EXCEPT ##
1. PostgreSQL `EXCEPT` operator
	1. Returns rows in the first query that do not appear in the output of the second query

### Introduction to the PostgreSQL EXCEPT Operator ###
1. `EXCEPT` operator returns rows by comparing result sets of two or more queries
	1. It returns distinct rows from first (left) query that are not in the output of the second (right) query
2. Syntax:

		SELECT select_list
		FROM A
		EXCEPT
		SELECT select_list
		FROM B;
		
	1. Rules to follow:
		1. Number of columns and their orders must be the same in the two queries
		2. Data types of the respective columns must be compatible

### PostgreSQL EXCEPT Operator Examples ###
1. Let us use the `top_rated_films` and `most_popular_films` tables
2. Find top-rated films that are not popular:

		SELECT * FROM top_rated_films
		EXCEPT
		SELECT * FROM most_popular_films;
		
3. Sort result set:

		SELECT * FROM top_rated_films
		EXCEPT
		SELECT * FROM most_popular_films
		ORDER BY title;
		
	2. `ORDER BY` is placed at the end of the statement

## PostgreSQL GROUPING SETS ##
1. How to use `GROUPING SETS` clause to generate multiple grouping sets in a query

### Setup a Sample Table ###
1. Creation of `sales` table:

		DROP TABLE IF EXISTS sales;
		CREATE TABLE sales (
			brand VARCHAR NOT NULL,
			segment VARCHAR NOT NULL,
			quantity INT NOT NULL,
			PRIMARY KEY (brand, segment)
		);
		
		INSERT INTO sales (brand, segment, quantity)
		VALUES
			('ABC', 'Premium', 100),
			('ABC', 'Basic', 200),
			('XYZ', 'Premium', 100),
			('XYZ', 'Basic', 300);
			
	1. `sales` table stores the number of products sold by brand and segment

### Introduction to PostgreSQL GROUPING SETS ###
1. A grouping set is a set of columns by which you group by using `GROUP BY` clause
2. A grouping set is denoted by a comma-separated list of columns placed inside parantheses:

		(column1, column2, ...)
		
	1. The query that uses `GROUP BY` clause to return the number of products sold by brand and segment
	2. It defines a grouping set of the brand and segment which is denoted by `(brand, segment)`
	
			SELECT
				brand,
				segment,
				SUM (quantity)
			FROM
				sales
			GROUP BY
				brand,
				segment;
				
	3. Query to find the number of products sold by a brand
	
			SELECT
				brand,
				SUM (quantity)
			FROM
				sales
			GROUP BY
				brand;
				
	4. Query to find number of products sold by segment
	
			SELECT
				segment,
				SUM (quantity)
			FROM
				sales
			GROUP BY
				segment;
				
	5. Query to find number of products sold by all brands and segments
	
			SELECT
				SUM (quantity)
			FROM
				sales;
				
3. To get all the grouping sets by using a single query:
	1. We can use `UNION ALL` to combine all the quries
		1. `UNION ALL` needs all result sets to have same number of columns with compatible data types:
			1. Solution: Add `NULL` to the selection list of each:
			
					SELECT
						brand,
						segment,
						SUM (quantity)
					FROM
						sales
					GROUP BY
						brand,
						segment
						
					UNION ALL
					
					SELECT
						brand,
						NULL,
						SUM (quantity)
					FROM
						sales
					GROUP BY
						brand
						
					UNION ALL
					
					SELECT
						NULL,
						segment,
						SUM (quantity)
					FROM
						sales
					GROUP BY
						segment
						
					UNION ALL
					
					SELECT
						NULL,
						NULL,
						SUM (quantity)
					FROM
						sales;
						
				1. Query generates single result set with aggregates for all grouping sets
				2. The query has two main problems:
					1. First, it is quite lengthy
					2. Second, it has a performance issue because PostgreSQL has to scan the `sales` table separately for each query
						1. Solution: `GROUPING SETS` clause
							1. It is a subclause of `GROUP BY` clause
4. `GROUPING SETS` allows us to define multiple grouping sets in a single query
5. Syntax:

		SELECT
			c1,
			c2,
			aggregate_function(c3)
		FROM
			table_name
		GROUP BY
			GROUPING SETS (
				(c1, c2),
				(c1),
				(c2),
				()
			);
			
	1. We have 4 grouping sets `(c1, c2)`, `(c1)`, `(c2)`, and `()`
6. Applying the syntax to the example:

		SELECT
			brand,
			segment,
			SUM (quantity)
		FROM
			sales
		GROUP BY
			GROUPING SET (
				(brand, segment),
				(brand),
				(segment),
				()
			);
		
	1. Pros:
		1. Query is shorted and more readable
		2. PostgreSQL will optimize the number of times it scans `sales` table (avoids unnecessary multiple scans)

### Grouping Function ###
1. `GROUPING()` **(M)** function:
	1. It accepts an argument which can be a column name or an expression
	
			GROUPING( column_name | expression )
			
		1. `column_name` or `expression` must match with one specified in the `GROUP BY` clause
	2. The function returns:
		1. `0`: if **the argument is a member of the current grouping set**
		2. `1`: **otherwise**
2. Example:

		SELECT
			GROUPING (brand) grouping_brand,
			GROUPING (segment) grouping_segment,
			brand,
			segment,
			SUM (quantity)
		FROM
			sales
		GROUP BY
			GROUPING SETS (
				(brand),
				(segment),
				()
			)
		ORDER BY
			brand,
			segment;
			
	1. When the value in `grouping_brand` is `0`, the `sum` columns shows the subtotal of the `brand`
	2. When the value in `grouping_segment` is `0`, the `sum` column shows the subtotal of the `segment`
3. Using `GROUPING` in `HAVING` clause to find subtotal of each `brand`:

		SELECT
			GROUPING (brand) AS grouping_brand,
			GROUPING (segment) AS grouping_segment,
			brand,
			segment,
			SUM (quantity)
		FROM
			sales
		GROUP BY
			GROUPING SET (
				(brand),
				(segment),
				()
			)
		HAVING GROUPING (brand) = 0
		ORDER BY
			brand,
			segment;
			
## PostgreSQL ROLLUP ##
1. How to use PostgreSQL `ROLLUP` to generate multiple grouping sets

### Introduction to the PostgreSQL ROLLUP ###
1. `ROLLUP` **(M)** is a subclass of `GROUP BY` clause that offers shorthand for defining multiple `GROUPING SETS`
	1. `ROLLUP` does not generate all possible grouping sets based on the specified columns
		1. It makes a subset of those
		2. It assumes a hierarchy among input columns
			1. grouping sets are generated based on what makes sense considering the hierarchy
	2. Use-cases:
		1. To generate subtotals and grand totals (order or individual columns doesn't matter)
2. `CUBE` **(M)** vs `ROLLUP`
	1. `CUBE (c1, c2, c3)` generates:
	
			(c1, c2, c3)
			(c1, c2)
			(c2, c3)
			(c1, c3)
			(c1)
			(c2)
			(c3)
			()
			
	2. `ROLLUP (c1, c2, c3)` generates:
	
			(c1, c2, c3)
			(c1, c2)
			(c1)
			()
			
		1. `ROLLUP` assumes `c1 > c2 > c3` in this case
			1. Interpretation: `c1` must be part of the group for `c2` to be part of the group, `c2` must be part of the group for `c3` to be part of the group
		2. Use-case: To calculate aggregations of date by year, month, and date considering the hierarchy `year > month > date`
3. Syntax:

		SELECT
			c1,
			c2,
			c3,
			aggregate(c4)
		FROM
			table_name
		GROUP BY
			ROLLUP (c1, c2, c3);
			
	1. Partial roll ups:
	
			SELECT
				c1,
				c2,
				c3,
				aggregate(c4)
			FROM
				table_name
			GROUP BY
				ROLLUP (c2, c3);
				
		1. This generates the following groups:
		
				(c2, c3)
				(c2)
				()

### PostgreSQL ROLLUP Examples ###
1. Creation of tables:

		DROP TABLE IF EXISTS sales;
		CREATE TABLE sales (
			brand VARCHAR NOT NULL,
			segment VARCHAR NOT NULL,
			quantity INT NOT NULL,
			PRIMARY KEY (brand, segment)
		);
		
		INSERT INTO sales (brand, segment, quantity)
		VALUES
			('ABC', 'Premium', 100),
			('ABC', 'Basic', 200),
			('XYZ', 'Premium', 100),
			('XYZ', 'Basic', 300);
			
2. Find number of products sold by `brand` (subtotal) and by all `brands` and `segments` (total)

		SELECT
			brand,
			segment,
			SUM (quantity)
		FROM
			sales
		GROUP BY
			ROLLUP (brand, segment)
		ORDER BY
			brand,
			segment;
			
	1. Result shows:
		1. Third row: sales of `ABC` brand
		2. Sixth row: sales of `XYZ` brand
		3. Last row: grand total of all brands and segments
	2. The hierarchy is: `brand > segment`
	3. The result will be different if we swap the order
	
			SELECT
				segment,
				brand,
				SUM (quantity)
			FROM
				sales
			GROUP BY
				ROLLUP (segment, brand)
			ORDER BY
				segment,
				brand;
				
3. Partial roll up:

		SELECT
			segment,
			brand,
			SUM (quantity)
		FROM
			sales
		GROUP BY
			segment,
			ROLLUP (brand)
		ORDER BY
			segment,
			brand;
			
4. Find the number of rentals per day, month, and year using `ROLLUP`:
	1. Consider the following `rental` table:
	
			rental
				* rental_id
				rental_date
				inventory_id
				customer_id
				return_date
				staff_id
				last_update
				
		1. Query:
		
				SELECT
					EXTRACT (YEAR FROM rental_date) y,
					EXTRACT (MONTH FROM rental_date) m,
					EXTRACT (DAY FROM rental_date) d,
					COUNT (rental_id)
				FROM
					rental
				GROUP BY
					ROLLUP (
						EXTRACT(YEAR FROM rental_date),
						EXTRACT(MONTH FROM rental_date),
						EXTRACT(DAY FROM rental_date)
					);

## PostgreSQL CUBE ##
1. How to use PostgreSQL `CUBE` to generate multiple grouping sets

### Introduction to the PostgreSQL CUBE ###
1. `CUBE` is a subclause of `GROUP BY` clause
	1. It allows us to generate multiple grouping sets
		1. Grouping set: It is a set of columns to which we want to group
2. Syntax:

		SELECT
			c1,
			c2,
			c3,
			aggregate (c4)
		FROM
			table_name
		GROUP BY
			CUBE (c1, c2, c3);
			
	1. Specify `CUBE` subclause inside `GROUP BY` clause
	2. Select list, specify the columns (dimensions or dimension columns) which we want to analyze, and aggregation expressions
	3. Specify dimension columns within the parantheses of `CUBE` subclause
3. Query generates all possible grouping sets based on the dimension columns specified in `CUBE`
	1. It is a short way to define multiple grouping sets. It is equivalent to:
	
			CUBE (c1, c2, c3)
			
			GROUPING SETS (
				(c1, c2, c3),
				(c1, c2),
				(c2, c3),
				(c1, c3),
				(c1),
				(c2),
				(c3),
				()
			)
			
		1. If the number of columns specified in the `CUBE` is n, then you will have `2^n` combinations
4. Partial `CUBE`s is allowed to reduce the number of aggregates calculated:

		SELECT
			c1,
			c2,
			c3,
			aggregate (c4)
		FROM
			table_name
		GROUP BY
			c1,
			CUBE (c2, c3);

### PostgreSQL CUBE Examples ###
1. Let us use the `sales` table.
2. Following query uses `CUBE` subclause to generate multiple grouping sets:

		SELECT
			brand,
			segment,
			SUM (quantity)
		FROM
			sales
		GROUP BY
			CUBE (brand, segment)
		ORDER BY
			brand,
			segment;
			
3. Partial `CUBE`:

		SELECT
			brand,
			segment,
			SUM (quantity)
		FROM
			sales
		GROUP BY
			brand,
			CUBE (segment)
		ORDER BY
			brand,
			segment;
			
## PostgreSQL Subquery ##
1. How to use PostgreSQL subquery that allows us to construct complex queries

### Introduction to PostgreSQL Subquery ###
1. Find all films whose rental rate is higher than the average rental rate.
	1. Find the average rental rate using SELECT statement and average function (`AVG`)
	2. Use the result of the first query in the second `SELECT` statement to find the films that we want
2. Query to get average rental rate:

		SELECT
			AVG (rental_rate)
		FROM
			film;
			
3. Query to get films whose rental rate is higher than average rental rate (`2.98`)

		SELECT
			film_id,
			title,
			rental_rate
		FROM
			film
		WHERE
			rental_rate > 2.98;
			
4. The code is not elegent because it needs two steps
	1. Solution: Subquery
		1. Used to pass the result of one query to the second query in one single complex query
5. Subquery: A query nested inside another query
	1. `SELECT`
	2. `INSERT`
	3. `DELETE`
	4. `UPDATE`
6. Construction: We put the second query in brackets and use it in the `WHERE` clause:

		SELECT
			film_id,
			title,
			rental_rate
		FROM
			film
		WHERE
			rental_rate > (
				SELECT 
					AVG (rental_rate)
				FROM
					film
			);
			
	1. Query inside the brackets is called a **subquery** or **inner query**
	2. Query that contains a subquery is called **outer query**
7. Execution:
	1. Step 1: Executes the subquery
	2. Step 2: Gets the result and passes it to the outer query
	3. Step 3: Executes the outer query

### PostgreSQL Subquery with IN Operator ###
1. A subquery can return 0 or more rows.
2. Using `IN`
	1. Example: Get films that have the returned date between `2005-05-29` and `2005-05-30`:
	
			SELECT
				inventory.film_id
			FROM
				rental
			INNER JOIN inventory
				ON inventory.inventory_id = rental.inventory_id
			WHERE
				return_date BETWEEN '2005-05-29' AND '2005-05-30';
				
3. Returning multiple rows to use the query as a subquery in `WHERE` clause of a query:

		SELECT
			film_id,
			title
		FROM
			film
		WHERE
			film_id IN (
				SELECT
					inventory.film_id
				FROM
					rental
				INNER JOIN inventory
					ON inventory.inventory_id = rental.inventory_id
				WHERE
					return date BETWEEN '2005-05-29' AND '2005-05-30'
			);

### PostgreSQL Subquery with EXISTS Operator ###
1. Usage:
	
		EXISTS subquery
		
	1. A subquery can be an input of `EXISTS` operator
		1. If subquery returns **any row**, `EXISTS` operator returns `true`
		2. If subquery returns no rows, `EXISTS` operator returns `false`
		3. Since only number of rows is important and not the content, the following convention is used:
				
				EXISTS (SELECT 1 FROM tbl WHERE condition);
				
2. Example:

		SELECT
			first_name,
			last_name
		FROM
			customer
		WHERE
			EXISTS (
				SELECT
					1
				FROM
					payment
				WHERE
					payment.customer_id = customer.customer_id
			);
			
	1. The query works like an inner join on `customer_id` column
	2. It returns at most one row for each row in the `customer` table even though there are some corresponding rows in the `payment` table
	
## PostgreSQL ANY Operator ##
1. How to use PostgreSQL `ANY` **(M)** operator to **compare a scalar value with a set of values** returned by a subquery

### Introduction to PostgreSQL ANY Operator ###
1. `ANY` operator compares a value to a set of values returned by a subquery
2. Syntax:

		expression operator ANY (subquery)
		
	1. subquery must return exactly **one column**
	2. `ANY` operator must be preceded by one of the following comparison operators: `=`, `<=`, `>`, `<>`, `>=`, `<`
	3. `ANY` operator returns `true` if any value of the subquery meets the condition, otherwise it returns `false`
3. `SOME` **(M)** is a synonym for `ANY`

### PostgreSQL ANY Examples ###
1. Using the following tables:
		
		film_category
			* film_id
			* category_id
			last_update
		
		film
			* film_id
			title
			description
			release_year
			language_id
			rental_duration
			rental_rate
			length
			replacement_cost
			rating
			last_update
			special_features
			fulltext
			
2. Return the maximum length of a film grouped by film category

		SELECT
			MAX ( length )
		FROM
			film
		INNER JOIN film_category
			USING (film_id)
		GROUP BY
			category_id;
			
	1. The above query can be used as a subquery in the statement that finds films whose lengths are greater than or equal to maximum length of any film category
	
			SELECT 
				title
			FROM 
				film
			WHERE length >= ANY (
				SELECT
					MAX (length)
				FROM film
				INNER JOIN film_category
					USING (film_id)
				GROUP BY
					category_id
			);
			
		1. For each film category, subquery finds maximum length
		2. Outer query looks at all the values and determines which film's lengths are greater than or equal to any film category's maximum length
		3. If the subquery does not return any rows, the entire query returns an empty result set

### ANY vs. IN ###
1. ` = ANY` is equivalent to `IN` operator
2. Example: Get films whose category is either `Action` or `Drama`

		SELECT
			title,
			category_id
		FROM film
		INNER JOIN film_category
			USING (film_id)
		WHERE
			category_id = ANY (
				SELECT
					category_id
				FROM
					film_category
				WHERE
					name = 'Action' OR
					name = 'Drama'
			);
			
	1. Using `IN` operator:
	
			SELECT
				title,
				category_id
			FROM film
			INNER JOIN film_category
				USING (film_id)
			WHERE category_id IN (
				SELECT
					category_id
				FROM
					film_category
				WHERE
					name = 'Action' OR
					name = 'Drama'
			);
			
		1. `<> ANY` operator is different from `NOT IN`
		
				x <> ANY (a, b, c)
				
			1. The above is equivalent to:
			
					x <> a OR x <> b OR x <> c

## PostgreSQL ALL Operator ##
1. How to use the PostgreSQL ALL operator to compare a value with a list of values returned by a subquery
2. Syntax: 
	
		comparison_operator ALL (subquery)
		
	1. `ALL` operator must be preceded by a comparison operator such as `=`, `!=`, `>`, `>=`, `<`, or `<=`
	2. `ALL` operator must be followed by a subquery which also must be surrounded by parantheses
3. How does it work?
	1. Assuming subquery returns a non-empty list
		1. `value > ALL (subquery)` - returns true if value is greater than biggest value returned by the subquery
		2. `value >= ALL (subquery)` - returns true if value is greater than or equal to the biggest value returned by the subquery
		3. `value < ALL (subquery)` - returns true if value is less than the smallest value returned by the subquery
		4. `value <= ALL (subquery)` - returns true if value is less than or equal to the smallest value returned by the subquery
		5. `value = ALL (subquery)` - returns true if value is equal to every value returned by the subquery
		6. `value != ALL (subquery)` - returns true if value is equal to none of the values returned by the subquery
	2. If subquery returns no rows, `ALL` operator evaluates to `true`
3. Example:

		CREATE TABLE employees (
			id SERIAL PRIMARY KEY,
			first_name VARCHAR(255) NOT NULL,
			last_name VARCHAR(255) NOT NULL,
			salary DECIMAL(10, 2) NOT NULL
		);

		CREATE TABLE managers (
			id SERIAL PRIMARY KEY,
			first_name VARCHAR(255) NOT NULL,
			last_name VARCHAR(255) NOT NULL,
			salary DECIMAL(10, 2) NOT NULL
		);

		INSERT INTO employees (first_name, last_name, salary)
		VALUES
		('Bob', 'Williams', 75000.00),
		('Charlie', 'Davis', 55000.00),
		('David', 'Jones', 50000.00),
		('Emma', 'Brown', 48000.00),
		('Frank', 'Miller', 52000.00),
		('Grace', 'Wilson', 49000.00),
		('Harry', 'Taylor', 53000.00),
		('Ivy', 'Moore', 47000.00),
		('Jack', 'Anderson', 56000.00),
		('Kate', 'Hill',  44000.00),
		('Liam', 'Clark', 59000.00),
		('Mia', 'Parker', 42000.00);

		INSERT INTO managers (first_name, last_name, salary)
		VALUES
		('John', 'Doe',  60000.00),
		('Jane', 'Smith', 55000.00),
		('Alice', 'Johnson',  58000.00);

### Using the ALL Operator with the Greater than Operator (>) Example ###
1. Example:

		SELECT
			*
		FROM
			employees
		WHERE
			salary > ALL (
				SELECT
					salary
				FROM
					managers
			);

### Using the All Operator with the Less than Operator (<) ###
1. Example:

		SELECT
			*
		FROM
			employees
		WHERE
			salary < ALL (
				SELECT
					salary
				FROM
					managers
			);

### Summary ###
1. `ALL` is used to compare with all values returned by a subquery.

## PostgreSQL INSERT - (16 days) ##
1. Summary: Learn how to use `INSERT` statement to insert a new row into a table

### Introduction to PostgreSQL INSERT statement ###
1. Basic syntax:

		INSERT INTO table1(column1, column2, ...)
		VALUES (value1, value2, ...);

	1. `table1` - name of the table
		1. `column1`, `column2`, ... - comma separated columns
	2. `(value1, value2, ...)` - value list (should be in the same order)
2. `INSERT` returns command tag of the following form:

		INSERT oid count

	1. `OID` - Object identifier
		1. PostgreSQL used the `OID` internally as a [primary key](https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-primary-key/) for its system tables
			1. Typically, `INSERT` statement returns `OID` with a value of `0`
	2. `count` is number of rows that `INSERT` statement inserted successfully
	3. Example:

			INSERT 0 1

### RETURNING clause ###
1. Optional `RETURNING` **(M)** clause
	1. It returns information of inserted row
		1. `*` returns the entire inserted row
		
		```sql
		INSERT INTO table1 (column1, column2, ...)
		VALUES (value1, value2, ...)
		RETURNING *;
		```
		
		2. `id` returns the id of the inserted row
		
		```sql
		INSERT INTO table1 (column1, column2, ...)
		VALUES (value1, value2, ...)
		RETURNING id;
		```
		
		3. `AS` keyword is used to rename the returned output
		
		```sql
		INSERT INTO table1 (column1, column2, ...)
		VALUES (value1, value2, ...)
		RETURNING output_expression AS output_name;
		```
		
2. To insert multiple rows: [https://neon.tech/postgresql/postgresql-tutorial/postgresql-insert-multiple-rows](https://neon.tech/postgresql/postgresql-tutorial/postgresql-insert-multiple-rows)

```sql
INSERT INTO table_name (column_list)
VALUES
    (value_list_1),
	(value_list_2),
	(value_list_3),
	...
	(value_list_n);
```

### PostgreSQL INSERT statement examples ###
1. New table creation:

```sql
CREATE TABLE links (
  id SERIAL PRIMARY KEY,
  url VARCHAR(255) NOT NULL,
  name VARCHAR(255) NOT NULL,
  description VARCHAR(255),
  last_update DATE
);
```

#### Basic PostgreSQL INSERT statement example ####
1. Example:

```sql
INSERT INTO links (url, name)
VALUES ('https://neon.tech/postgresql', 'PostgreSQL Tutorial');
```

```sql
-- output
INSERT 0 1
```

2. To insert character data, we eclose it in single quotes `''`
3. `NOT NULL` - An error is thrown if value is not provided
	1. Otherwise, a default value is used
		1. `NULL` is used for `description` column
4. `SERIAL` - Automatically generates a sequential number for serial column

#### Inserting character string that contains a single quote ####
1. To insert a string containing `'`, we need to use additional `'` to escape it

```sql
INSERT INTO links (url, name)
VALUES ('http://www.oreilly.com', 'O''Reilly Media');
```

#### Inserting a date value ####
1. Use date in the format `'YYYY-MM-DD'` **(M)**

```sql
INSERT INTO links (url, name, last_update)
VALUES ('https://www.google.com', 'Google', '2013-06-01');
```

#### Getting the last inserted ID ####
1. Use `RETURNING` clause.
2. Example:

```sql
INSERT INTO links (url, name)
VALUES ('https://www.postgresql.org', 'PostgreSQL')
RETURNING id;
```

```sql
INSERT INTO links (url, name)
VALUES ('https://www.postgresql.org', 'PostgreSQL')
RETURNING id, url;
```

### Summary ###
1. `RETURNING` - to get inserted rows

## PostgreSQL INSERT Multiple Rows ##
### Inserting multiple rows into a table ###
1. Syntax:

```sql
INSERT INTO table_name (column_list)
VALUES
  (value_list_1),
  (value_list_2),
  (value_list_3),
  ...
  (value_list_n);
```

2. Syntax:
	1. Specify name of the table to insert data into
	2. List the required columns of the table in parantheses
	3. Supply a comma separated list of rows after `VALUES` keyword
3. To return multiple rows after inserting:

```sql
INSERT INTO table_name (column_list)
VALUES
  (value_list_1),
  (value_list_2),
  ...
  (value_list_n)
RETURNING * | output_expression;
```

4. Advantages of inserting multiple rows compared to one row at a time:
	1. Performance: Reduces the number of round-trips between an application and PostgreSQL server
	2. Atomicity: Entire `INSERT` statement is atomic (either all rows are inserted, or none are).
		1. Ensures data consistency

### Inserting multiple rows into a table examples ###
#### Setting up a sample table ####

```sql
CREATE TABLE contacts (
  id SERIAL PRIMARY KEY,
  first_name VARCHAR(50) NOT NULL,
  last_name VARCHAR(50) NOT NULL,
  email VARCHAR(384) NOT NULL UNIQUE,
);
```

#### Basic inserting multiple rows example ####
1. Example:

```sql
INSERT INTO contacts (first_name, last_name, email)
VALUES
  ('John', 'Doe', '[[email protected]](../cdn-cgi/l/email-protection.html)'),
  ('Jane', 'Smith', '[[email protected]](../cdn-cgi/m/email-protection.html)'),
  ('Bob', 'Johnson', '[[email protected]](../cdn-cgi/n/email-protection.html)');
  
SELECT * FROM contacts;
```

#### Inserting multiple rows and returning inserted rows ####
1. Example:

```sql
INSERT INTO contacts (first_name, last_name, email)
VALUES
  ('Alice', 'Johnson', '[[email protected]](../cdn-cgi/o/email-protection.html)'),
  ('Charlie', 'Brown', '[[email protected]](../cdn-cgi/p/email-protection.html)')
RETURNING *;
```

1. Example: Returning id list only

```sql
INSERT INTO contacts (first_name, last_name, email)
VALUES
  ('Eva', 'Williams', '[[email protected]](../cdn-cgi/q/email-protection.html)'),
  ('Michael', 'Miller', '[[email protected]](../cdn-cgi/r/email-protection.html)'),
  ('Sophie', 'Davis', '[[email protected]](../cdn-cgi/s/email-protection.html)')
RETURNING id;
```

### Summary ###

## PostgreSQL UPDATE ##
**Summary**: How to use `UPDATE` statement to update existing data in a table

### Introduction to the PostgreSQL UPDATE statement ###
1. `UPDATE` allows us to update data in one or more columns of one or more rows in a table
2. Syntax:

```sql
UPDATE table_name
SET column1 = value1,
SET column2 = value2,
    ...
WHERE condition;
```

2. Explanation:
	1. `table_name` - name of table to update data. Comes after `UPDATE` clause
	2. `SET` - column name is specified after the keyword
		1. The columns that do not appear in the `SET` clause retain their original values
	3. `WHERE` - determines which rows to update
		1. It is optional.
			1. If omitted, all rows are updated.
3. Return: `UPDATE count`
	1. `count` - number of rows updated (including rows whose values did not change)

#### Returning updated rows ####
1. `RETURNING` - returns updated rows

```sql
UPDATE table_name
SET column1 = value1,
SET column2 = value2,
    ...
WHERE condition
RETURNING * | output_expression AS output_name;
```

### PostgreSQL UPDATE examples ###
1. Some examples of `UPDATE` statement

#### Setting up a sample table ####
1. Table creation:

```sql
CREATE TABLE courses (
  course_id serial PRIMARY KEY,
  course_name VARCHAR(255) NOT NULL,
  price DECIMAL(10, 2) NOT NULL,
  description VARCHAR(500),
  published_date date
);

INSERT INTO courses (course_name, price, description, published_date)
VALUES
('PostgreSQL for Developers', 299.99, 'A complete PostgreSQL for Developers', '2020-07-13'),
('PostgreSQL Admininstration', 349.99, 'A PostgreSQL Guide for DBA', NULL),
('PostgreSQL High Performance', 549.99, NULL, NULL),
('PostgreSQL Bootcamp', 777.99, 'Learn PostgreSQL via Bootcamp', '2013-07-11'),
('Mastering PostgreSQL', 999.98, 'Mastering PostgreSQL in 21 Days', '2012-06-30');

SELECT * FROM courses;
```

### Basic PostgreSQL UPDATE example ###
1. To update course with id 3 by changing the `published_date` to `'2020-08-01`

```sql
UPDATE courses
SET published_date = '2020-08-01'
WHERE course_id = 3;
```

2. Return: `UPDATE 1`
3. The following statement retrieves course with id 3 to verify the update:

```sql
SELECT course_id, course_name, published_date
FROM courses
WHERE course_id = 3;
```

### Updating a row and returning the updated row ###
1. Statement to `UPDATE` `published_date` of course with id 2 to `'2020-07-01'` and return updated course:

```sql
UPDATE courses
SET published_date = '2020-07-01'
WHERE course_id = 2
RETURNING *;
```

### Updating a column with an expression ###
1. `UPDATE` price by increasing it by 5%:

```sql
UPDATE courses
SET price = price * 1.05;
```

2. Output: `UPDATE 5`
3. To retrieve all courses:

```sql
SELECT * FROM courses;
```

```sql
SELECT
  course_name,
  price
FROM
  courses;
```

### Summary ###

## PostgreSQL UPDATE JOIN ##
1. How to update data in a table based on values in another table

### Introduction to the PostgreSQL UPDATE join syntax ###
1. We use PostgreSQL `UPDATE` join
2. Syntax:

```sql
UPDATE table1
SET table1.c1 = new_value
FROM table2
WHERE table1.c2 = table2.c2;
```

3. `FROM` - joins `table1` with `table2`
	1. Must appear soon after the `SET` clause
4. `WHERE` - join condition
5. Logic:
	1. For each row of `table1`, `UPDATE` statement examines if a row in `table2` can be found with such that the `c2` value in `table1` row equals the `c2` value in `table2` row. If a matching row is found, `c1` value in the `table1` row is updated to the `new_value`.

### PostgreSQL UPDATE JOIN example ###
1. `product_segment` stores `Grand Luxury`, `Luxury`, or `Mass`
	1. It has `discount` column that stores the discount percentage based on a specific segment
		1. Grand Luxury: 5%
		2. Luxury: 6%
		3. Mass: 10%
		
```sql
CREATE TABLE product_segment (
  id SERIAL PRIMARY KEY,
  segment VARCHAR NOT NULL,
  discount NUMERIC(4, 2)
);

INSERT INTO
  product_segment (segment, discount)
VALUES
  ('Grand Luxury', 0.05),
  ('Luxury', 0.06),
  ('Mass', 0.1);
```

2. `product` - stores product data.
	1. `segment_id` - foreign key column (links `id` of `product_segment` table)
	
```sql
CREATE TABLE product (
  id SERIAL PRIMARY KEY,
  name VARCHAR NOT NULL,
  price NUMERIC(10, 2),
  net_price NUMBERIC(10, 2),
  segment_id INT NOT NULL,
  FOREIGN KEY(segment_id) REFERENCES product_segment(id)
);

INSERT INTO
  product (name, price, segment_id)
VALUES
  ('diam', 804.89, 1),
  ('vestibulum aliquet', 228.55, 3),
  ('lacinia erat', 366.45, 2),
  ('scelerisque quam turpis', 145.33, 3),
  ('justo lacinia', 551.77, 2),
  ('ultrices mattis odio', 261.58, 3),
  ('hendrerit', 519.62, 2),
  ('in hac habitasse', 843.31, 1),
  ('orci eget orci', 254.18, 3),
  ('pellentesque', 427.78, 2),
  ('sit amet nunc', 936.29, 1),
  ('sed vestibulum', 910.34, 1),
  ('turpis eget', 208.33, 3),
  ('cursus vestibulum', 985.45, 1),
  ('orci nullam', 841.26, 1),
  ('est quam pharetra', 896.38, 1),
  ('posuere', 575.74, 2),
  ('ligula', 530.64, 2),
  ('convallis', 892.43, 1),
  ('nulla elit ac', 161.71, 3);
```

3. Problem: Calculate the net price of every product based on the discount of the product segment.

```sql
UPDATE product
SET net_price = price * (1 - discount)
FROM product_segment
WHERE product.segment_id = product_segment.id;
```

4. Making query shorter using table aliases:

```sql
UPDATE
  product p
SET 
  net_price = price * (1 - discount)
FROM 
  product_segment s
WHERE
  p.segment_id = s.id;
RETURNING *;
```

### Summary ###
1. `UPDATE` join is used to update data in a table based on values in another table

## PostgreSQL DELETE ##
1. Summary: How to use `DELETE` statement to delete data from a table.

### Introduction to PostgreSQL DELETE statement ###
1. `DELETE` allows us to delete one or more rows in a table
2. Basic syntax:

```sql
DELETE FROM table_name
WHERE condition;
```

	1. Specify name (`table_name`) of the table from which we want to delete data after `DELETE FROM`
	2. `WHERE` - used to specify condition to determine the rows to delete
		1. If ommitted, all rows will be deleted.
	3. Returns the number of rows deleted
3. `RETURNING` - to return the deleted rows to the client

```sql
DELETE FROM table_name
WHERE condition
RETURNING (select_list | *)
```

	1. `*` - all columns of deleted rows
4. Delete Join - to delete data based on data in another table
5. `ON DELETE CASCADE` - **(M)**

### PostgreSQL DELETE statement examples ###
#### Setting up a sample table ####
1. `todos` creation and insertion of data:

```sql
CREATE TABLE todos (
  id SERIAL PRIMARY KEY,
  title VARCHAR(255) NOT NULL,
  completed BOOLEAN NOT NULL DEFAULT false
);

INSERT INTO todos (title, completed)
VALUES
  ('Learn basic SQL syntax', true),
  ('Practice writing SELECT queries', false),
  ('Study PostgreSQL data types', true),
  ('Create and modify tables', false),
  ('Explore advanced SQL concepts', true),
  ('Understand indexes and optimization', false),
  ('Backup and restore databases', true),
  ('Implement transactions', false),
  ('Master PostgreSQL security features', true),
  ('Build a sample application with PostgreSQL', false);
  
SELECT * FROM todos;
```

#### Using PostgreSQL DELETE to delete one row from the table ####
#### Using PostgreSQL DELETE to delete a row and return the deleted row ####
#### Using PostgreSQL DELETE to delete multiple rows from the table ####
#### Using PostgreSQL DELETE to delete all rows from the table ####
### Summary ###

## PostgreSQL DELETE JOIN ##
## PostgreSQL UPSERT using INSERT ON CONFLICT Statement ##
## PostgreSQL MERGE Statement ##

## PostgreSQL Transaction ##

## Import CSV File Into PostgreSQL Table ##
## Export PostgreSQL Table to CSV File ##

## PostgreSQL Data Types ##
## PostgreSQL CREATE TABLE ##
## PostgreSQL SELECT INTO ##
## PostgreSQL CREATE TABLE AS ##
## Using PostgreSQL SERIAL to Construct Auto-Increment Column ##
## PostgreSQL Sequences ##
## PostgreSQL Identity Column ##
## PostgreSQL Generated Columns ##
## PostgreSQL ALTER TABLE ##
## PostgreSQL Rename Table: A Step-by-Step Guide ##
## PostgreSQL ADD COLUMN: Add One or More Columns to a Table ##
## PostgreSQL DROP COLUMN: Remove One or More Columns of a Table ##
## PostgreSQL Change Column Type ##
## PostgreSQL RENAME COLUMN: Renaming a Column ##
## PostgreSQL DROP TABLE ##
## PostgreSQL TRUNCATE TABLE ##
## PostgreSQL Temporary Table ##
## PostgreSQL Copy Table: A Step-by-Step Guide with Practical Examples ##

## PostgreSQL Primary Key ##
## PostgreSQL Foreign Key ##
## PostgreSQL DELETE Cascade ##
## PostgreSQL CHECK Constraints ##
## PostgreSQL UNIQUE Constraint ##
## PostgreSQL Not-Null Constraint ##
## PostgreSQL DEFAULT Value ##

## PostgreSQL Boolean Data Type with Practical Examples ##
## PostgreSQL Character Types: CHAR, VARCHAR, and TEXT ##
## PostgreSQL NUMERIC Type ##
## PostgreSQL DOUBLE PRECISION Data Type ##
## PostgreSQL REAL Data Type ##
## PostgreSQL Integer Data Types ##
## PostgreSQL DATE Data Type ##
## PostgreSQL Timestamp Data Types ##
## PostgreSQL Interval Data Type ##
## PostgreSQL TIME Data Type ##
## PostgreSQL UUID Data Type ##
## PostgreSQL Array ##
## PostgreSQL hstore ##
## PostgreSQL JSON ##
## A Look at PostgreSQL User-defined Data Types ##
## PostgreSQL enum ##
## PostgreSQL XML Data Type ##
## PostgreSQL BYTEA Data Type ##
## PostgreSQL Composite Types ##

## How to Compare Two Tables in PostgreSQL ##
## How to Generate a Random Number in a Range ##
## How to Delete Duplicate Rows in PostgreSQL ##

## PostgreSQL CASE ##
## PostgreSQL COALESCE ##
## PostgreSQL ISNULL ##
## PostgreSQL NULLIF ##
## PostgreSQL CAST: Convert a value of One Type to Another ##
## PostgreSQL EXPLAIN ##
## PostgreSQL DISTINCT ON ##
## PostgreSQL vs MySQL ##

## PostgreSQL generate_series() Function ##

## PostgreSQL PL/pgSQL - (7 days) ##
## Introduction to PostgreSQL PL/pgSQL ##
## Dollar-Quoted String Constants ##
## PL/pgSQL Block Structure ##
## PL/pgSQL Variables ##
## PL/pgSQL Select Into ##
## PL/pgSQL Row Types ##
## PL/pgSQL Record Types ##
## PL/pgSQL Constants ##
## PL/pgSQL Errors and Messages ##
## PL/pgSQL Assert Statement ##
## PL/pgSQL IF Statement ##
## PL/pgSQL CASE Statement ##
## PL/pgSQL Loop Statements ##
## PL/pgSQL While Loop ##
## PL/pgSQL For Loop ##
## PL/pgSQL Exit Statement ##
## PL/pgSQL Continue Statement ##
## PostgreSQL Exception ##
## PostgreSQL Create Function Statement ##
## PL/pgSQL Function Parameter Modes: IN, OUT, INOUT ##
## PL/pgSQL Function Overhoading ##
## How to Develop a PL/pgSQL Function That Returns a Table ##
## PL/pgSQL Returns SetOf ##
## PostgreSQL Drop Function ##
## PostgreSQL CREATE PROCEDURE ##
## PostgreSQL DROP PROCEDURE Statement ##
## PostgreSQL Stored Procedure with INOUT Parameters ##
## PL/pgSQL Cursor ##

## PostgreSQL Triggers - (4 days) ##
## Introduction to PostgreSQL Trigger ##
## PostgreSQL CREATE TRIGGER Statement ##
## PostgreSQL DROP TRIGGER Statement ##
## PostgreSQL ALTER TRIGGER Statement ##
## PostgreSQL BEFORE INSERT Trigger ##
## PostgreSQL AFTER INSERT Trigger ##
## PostgreSQL BEFORE UPDATE Trigger ##
## PostgreSQL AFTER UPDATE Trigger ##
## PostgreSQL BEFORE DELETE Trigger ##
## PostgreSQL AFTER DELETE Trigger ##
## PostgreSQL INSTEAD OF Triggers ##
## PostgreSQL BEFORE TRUNCATE Trigger ##
## Disable Triggers ##
## Enable Triggers ##
## How to List All Triggers in PostgreSQL ##
## PostgreSQL Event Trigger ##
## Constructing a PostgreSQL Trigger with a When Condition ##

## PostgreSQL Views - (2 days) ##
## PostgreSQL CREATE VIEW ##
## PostgreSQL Drop View ##
## Create PostgreSQL Updatable Views ##
## PostgreSQL WITH CHECK OPTION ##
## PostgreSQL ALTER VIEW Statement ##
## PostgreSQL Materialized Views ##
## PostgreSQL Recursive View ##
## PostgreSQL List Views ##

## PostgreSQL Indexes - (3 days) ##
## PostgreSQL CREATE INDEX Statement ##
## PostgreSQL UNIQUE Index ##
## PostgreSQL Index on Expression ##
## PostgreSQL Partial Index ##
## PostgreSQL Multicolumn Indexes ##
## PostgreSQL REINDEX ##
## PostgreSQL DROP INDEX ##
## PostgreSQL List Indexes ##
## PostgreSQL Index Types ##
## PostgreSQL Full Text Search ##
## PostgreSQL JSON Index ##


## PostgreSQL Administraion - (10 days) ##
## PostgreSQL CREATE DATABASE ##
## PostgreSQL ALTER DATABASE ##
## PostgreSQL DROP DATABASE ##
## PostgreSQL Rename Database ##
## PostgreSQL Copy Database Made Easy ##
## How to Get Sizes of Database Objects in PostgreSQL ##
## How to Change the Owner of a PostgreSQL Database ##
## PostgreSQL Schema ##
## PostgreSQL CREATE SCHEMA ##
## PostgreSQL ALTER SCHEMA ##
## PostgreSQL DROP SCHEMA Statement ##
## PostgreSQL CREATE ROLE Statement ##
## PostgreSQL GRANT ##
## PostgreSQL REVOKE Statement ##
## PostgreSQL Role Membership ##
## PostgreSQL SET ROLE Statement ##
## PostgreSQL CURRENT_USER ##
## PostgreSQL ALTER ROLE Statement ##
## PostgreSQL DROP ROLE Statement ##
## PostgreSQL List Users ##
## How to Define Superuser in PostgreSQL ##
## PostgreSQL Row-Level Security ##
## Reset Forgotten Password For postgres User ##
## How to Change the Password of a PostgreSQL User ##
## PostgreSQL CREATE TABLESPACE ##
## PostgreSQL ALTER TABLESPACE ##
## PostgreSQL DROP TABLESPACE Statement ##
## PostgreSQL Backup ##
## PostgreSQL Restore Database ##
## PostgreSQL Show Databases ##
## PostgreSQL Show Tables ##
## PostgreSQL Describe Table ##
## 17 Practical psql Commands You Don't Want to Miss ##
## How to Uninstall PostgreSQL for Ubuntu ##
## PostgreSQL Password File .pgpass ##
## PostgreSQL Uptime ##
## How to Check PostgreSQL Version ##
## How to Restart PostgreSQL on Ubuntu ##
## How to Restart PostgreSQL on Windows ##
## PostgreSQL pg_terminate_backend() Function ##

## PostgreSQL Functions ##
## PostgreSQL Aggregate Functions ##
## PostgreSQL AVG Function ##
## PostgreSQL COUNT Function ##
## PostgreSQL MAX Function ##
## PostgreSQL MIN() Function ##
## PostgreSQL SUM Function ##
## PostgreSQL ARRAY_AGG Function ##
## PostgreSQL BOOL_AND() Function ##
## PostgreSQL STRING_AGG Function ##
## PostgreSQL BOOL_OR() Function ##
## PostgreSQL Date Functions ##
## PostgreSQL CURRENT_DATE Function ##
## PostgreSQL CURRENT_TIME Function ##
## PostgreSQL CURRENT_TIMESTAMP Function ##
## PostgreSQL CLOCK_TIMESTAMP() Function ##
## PostgreSQL STATEMENT_TIMESTAMP() Function ##
## PostgreSQL NOW() Function ##
## PostgreSQL LOCALTIME Function ##
## PostgreSQL LOCALTIMESTAMP Function ##
## PostgreSQL DATE_PART() Function ##
## PostgreSQL EXTRACT() Function ##
## PostgreSQL TO_DATE() Function ##
## PostgreSQL TO_TIMESTAMP Function ##
## PostgreSQL MAKE_DATE() Function ##
## PostgreSQL MAKE_TIME() Function ##
## PostgreSQL AGE() Function ##
## PostgreSQL JUSTIFY_DAYS() Function ##
## PostgreSQL JUSTIFY_HOURS() Function ##
## PostgreSQL JUSTIFY_INTERVAL() Function ##
## PostgreSQL MAKE_INTERVAL() Function ##
## PostgreSQL AT TIME ZONE Operator ##
## PostgreSQL DATE_TRUNC() Function ##
## PostgreSQL ISFINITE() Function ##
## PostgreSQL TIMEOFDAY() Function ##
## PostgreSQL PG_SLEEP() Function ##
## PostgreSQL String Functions ##
## PostgreSQL ASCII() Function ##
## PostgreSQL CHR() Function ##
## PostgreSQL INITCAP() Function ##
## PostgreSQL POSITION() Function ##
## PostgreSQL SUBSTRING() Function ##
## PostgreSQL SPLIT_PART() Function ##
## PostgreSQL REPLACE() Function ##
## PostgreSQL REGEXP_REPLACE() Function ##
## PostgreSQL REGEXP_MATCHES() Function ##
## PostgreSQL REVERSE() Function ##
## PostgreSQL REPEAT() Function ##
## PostgreSQL LENGTH() Function ##
## PostgreSQL TRIM() Function ##
## PostgreSQL LTRIM() Function ##
## PostgreSQL LOWER() Function ##
## PostgreSQL UPPER() Function ##
## PostgreSQL RTRIM() Function ##
## PostgreSQL FORMAT() Function ##
## PostgreSQL MD5() Function ##
## PostgreSQL LEFT() Function ##
## PostgreSQL RIGHT() Function ##
## PostgreSQL LPAD() Function ##
## PostgreSQL RPAD() Function ##
## PostgreSQL CONCAT() Function ##
## PostgreSQL CONCAT_WS() Function ##
## PostgreSQL TRANSLATE() Function ##
## PostgreSQL TO_CHAR() Function ##
## PostgreSQL TO_NUMBER() Function ##
## PostgreSQL Math Functions ##
## PostgreSQL ABS() Function ##
## PostgreSQL CEIL() Function ##
## PostgreSQL CBRT() Function ##
## PostgreSQL DEGREES() Function ##
## PostgreSQL DIV() Function ##
## PostgreSQL EXP() Function ##
## PostgreSQL FLOOR() Function ##
## PostgreSQL MOD() Function ##
## PostgreSQL LN() Function ##
## PostgreSQL LOG() Function ##
## PostgreSQL POWER() Function ##
## PostgreSQL RANDOM() Function ##
## PostgreSQL RADIANS() Function ##
## PostgreSQL ROUND() Function ##
## PostgreSQL PI() Function ##
## PostgreSQL SIGN() Function ##
## PostgreSQL SCALE() Function ##
## PostgreSQL SQRT() Function ##
## PostgreSQL TRUNC() Function ##
## PostgreSQL TRIM_SCALE() Function ##
## PostgreSQL WIDTH_BUCKET() Function ##
## PostgreSQL Window Function ##
## PostgreSQL CUME_DIST ##
## PostgreSQL DENSE_RANK ##
## PostgreSQL FIRST_VALUE ##
## PostgreSQL LAG ##
## PostgreSQL LAST_VALUE ##
## PostgreSQL LEAD ##
## PostgreSQL NTILE ##
## PostgreSQL NTH_VALUE ##
## PostgreSQL PERCENT_RANK ##
## PostgreSQL RANK ##
## PostgreSQL ROW_NUMBER ##

## PostgreSQL JSON Functions ##

---
## Section 2: Filtering Data ##

## Section 3: Joining Multiple Tables ##

## Section 4: Grouping Data ##

## Section 5: Set Operations ##

## Section 6: Grouping Sets, Cube, and Rollup ##

## Section 7: Subquery ##

## Section 8: Common Table Extensions ##

## Section 9: Modifying Data ##

## Section 10: Transactions ##

## Section 11: Import & Export Data ##

## Section 12: Managing Tables ##

## Section 13: Understanding PostgreSQL Constraints ##

## Section 14: PostgreSQL Data Types in Depth ##

## Section 15: Conditional Expressions & Operations ##

## Section 16: PostgreSQL Utilities ##

## Section 17: PostgreSQL Recipes ##

## Advanced PostgreSQL Tutorial ##
### PostgreSQL PL/pgSQL ###
### PostgreSQL Triggers ###
### PostgreSQL Views ###
### PostgreSQL Indexes ###
### PostgreSQL Administration ###