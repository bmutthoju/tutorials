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
1. `DELETE` one row with the id 1 from `todos` table:

```
DELETE FROM todos
WHERE id = 1;
```

```
DELETE 1
```

2. If a row with `ìd` 100, which does not exist, is tried to be `DELETE`d, 

#### Using PostgreSQL DELETE to delete a row and return the deleted row ####
1. Statement to `DELETE` the row with `id` 2, and return the deleted row:

```
DELETE FROM todos
WHERE id = 2
RETURNING *;
```

#### Using PostgreSQL DELETE to delete multiple rows from the table ####
1. `DELETE` all rows from the `todos` table with the value `true` in the completed column and return the rows:

```
DELETE FROM todos
WHERE completed = true
RETURNING *;
```

#### Using PostgreSQL DELETE to delete all rows from the table ####
1. `DELETE` all rows in the table:

```
DELETE FROM todos;
```

### Summary ###

## PostgreSQL DELETE JOIN ##
1. `DELETE` statement for delete join operations

### Introduction to PostgreSQL DELETE statement with USING clause ###
1. PostgreSQL doesn't support [DELETE JOIN statement like in MySQL](https://www.mysqltutorial.org/mysql-basics/mysql-delete-join/).
2. It offers `USING` clause in `DELETE` statement, which is similar to `DELETE JOIN`
3. Syntax:

```
DELETE FROM table1
USING table2
WHERE condition
RETURNING returning_columns;
```

	1. `table1` - Name of the table you want to delete from
	2. `table2` - Name of the table to join with the main table after `USING` keyword
	3. `condition` - used to join the tables
	
4. Example:

```
DELETE from t1
USING t2
WHERE t1.id = t2.id
```

### PostgreSQL DELETE JOIN examples ###
#### Setting up sample tables ####
1. `member` and `denylist` tables:

```
CREATE TABLE member (
    id SERIAL PRIMARY KEY,
	first_name VARCHAR(50) NOT NULL,
	last_name VARCHAR(50) NOT NULL,
	phone VARCHAR(15) NOT NULL
);

CREATE TABLE denylist (
    phone VARCHAR(15) PRIMARY KEY
);

INSERT INTO member (first_name, last_name, phone)
VALUES ('John', 'Doe', '(408)-523-9874'),
       ('Jane','Doe','(408)-511-9876'),
	   ('Lily','Bush','(408)-124-9221');
	   
INSERT INTO denylist (phone)
VALUES ('(408)-523-9874'),
	   ('(408)-511-9876');
	   
SELECT * FROM member;

SELECT * FROM denylist;
```

#### Basic PostgreSQL delete join example ####
1. `DELETE` rows in `member`s table if the phone number exists in `denylist` table:

```
DELETE FROM member
USING denylist
WHERE member.phone = denylist.phone
RETURNING *;

SELECT * FROM member;
```

#### Delete join using a subquery example ####
1. `USING` is not part of SQL standard.
	1. It may not be available in other DB systems
		1. Alternative: Subquery
2. Above example using subquery:

```
DELETE FROM member
WHERE phone IN (
    SELECT 
	    phone
	FROM 
	    denylist
)
RETURNING *;

SELECT * FROM member;
```

### Summary ###

## PostgreSQL UPSERT using INSERT ON CONFLICT Statement ##
1. To insert a new row into a table if the row does not exist, or update an existing row if it already exists

### Introduction to the PostgreSQL UPSERT Statement ###
1. Upsert is a combination of update and insert
	1. To update an existing row, or insert a new row if it doesn't exist
2. There is no `UPSERT` in PostgreSQL but it supports `INSERT ... ON CONFLICT` statement
	1. [MERGE](https://neon.tech/postgresql/postgresql-tutorial/postgresql-merge) statement if >= PostgreSQL 15
		1. It is equivalent to `UPSERT` statement
3. Syntax:

```sql
INSERT INTO table_name (column1, column2, ...)
VALUES (value1, value2, ...)
ON CONFLICT (conflict_column)
DO NOTHING | DO UPDATE SET column1 = value1, column2 = value2, ...;
```

	1. `ON CONFLICT (conflict_column)`: Clause specifies conflict target
		1. Unique constraint or unique index that may cause a conflict
	2. `DO NOTHING`: Instructs PostgreSQL to do nothing when a conflict occurs
	3. `DO UPDATE`: Performs an update if a conflict occurs
	
4. How does it work?
	1. `ON CONFLICT` clause identifies the conflict target which is usually a unique constraint (or a unique index).
		1. If the data that you insert violates the constraint, a conflict occurs
	2. `DO UPDATE` clause instructs PostgreSQL to update existing rows or do nothing rather than aborting the entire operation when a conflict occurs
	3. `SET` clause defines the columns and values to update.
		1. You can use new values or reference values you attempted to insert using `EXCLUDED` keyword

### PostgreSQL UPSERT examples ###
1. Example:

```sql
CREATE TABLE inventory (
  id INT PRIMARY KEY,
  name VARCHAR(255) NOT NULL,
  price DECIMAL(10,2) NOT NULL,
  quantity INT NOT NULL
);

INSERT INTO inventory (id, name, price, quantity)
VALUES
  (1, 'A', 15.99, 100),
  (2, 'B', 25.49, 50),
  (3, 'C', 19.95, 75)
RETURNING *;
```

2. Requirement: Received an updated list of products with new prices, and you need to update inventory accordingly
	1. **Updating existing products**: If a product already exists in `inventory` table, you want to update its price and quantity with the new information
	2. **Insert new products**: If a product is not in the `inventory` table, you want to insert it into the table

#### Basic PostgreSQL INSERT ... ON CONFLICT statement example ####
1. Solution:

```
INSERT INTO (id, name, price, quantity)
VALUES
  (1, 'A', 16.99, 120)
ON CONFLICT (id)
DO UPSERT SET
  price = EXCLUDED.price,
  quantity = EXCLUDED.quantity;
```

#### Inserting data example ####
1. `INSERT ... ON CONFLICT` to insert a new row into the `inventory` table

```sql
INSERT INTO inventory (id, name, price, quantity)
VALUES (4, 'D', 29.99, 20)
ON CONFLICT (id)
DO UPDATE SET
  price = EXCLUDED.price,
  quantity = EXCLUDED.quantity;
```

2. To verify:

```sql
SELECT * FROM inventory
ORDER BY id;
```

### Summary ###

## PostgreSQL MERGE Statement ##
1. Used to conditionally insert, update, and delete rows of a table

### Introduction to the PostgreSQL MERGE statement ###
1. It is like a smart helper that can look at your data and decide whether to add new records, update existing ones, or even delete records, all in a single command

### Basic Concepts ###
1. Target table: Table you want to modify
2. Source table: Table containing your new or updated data
3. Match condition: Rule that determines if records match between your tables

### Basic MERGE Syntax ###
1. Syntax:

```sql
MERGE INTO target_table
USING source_table
ON match_condition
WHEN MATCHED AND condition THEN
  UPDATE SET column1 = value1, column2 = value2
WHEN MATCHED AND NOT condition THEN
  DELETE
WHEN NOT MATCHED THEN
  INSERT (column1, column2) VALUES (value1, value2)
RETURNING merge_action(), target_table.*;
```

	1. Conditional actions on `target_table` based on rows from `source_table`
		1. Update rows: `ON match_condition` (if a match is found), and `condition` is true, updates `column1` and `column2` in `target_table`
		2. Delete rows: If a match is found, but `condition` is false, it deletes the matching rows in `target_table`
		3. Insert rows: If no match is found, it inserts new rows into `target_table` using values from `source_table`

### Key Features in PostgreSQL 17 ###
1. `RETURNING` clause offers the following advantages:
	1. **Action Tracking:** The `merge_action()` function tells you exactly what happened to each row
	2. **Complete Row Access:** You can return both old and new values for affected rows (?)
	3. **Immediate Feedback:** No need for separate queries to verify the results

### Setting Up Our Example ###

```
-- Main product table
CREATE TABLE products (
  product_id SERIAL PRIMARY KEY,
  name TEXT unique,
  price DECIMAL (10, 2),
  stock INTEGER,
  status TEXT,
  last_updated TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Insert some initial data
INSERT INTO products (name, price, stock, status) VALUES
  ('Laptop', 999.99, 50, 'active'),
  ('Keyboard', 79.99, 100, 'active'),
  ('Mouse', 29.99, 200, 'active');
  
-- Creation of table for our updates
CREATE TABLE product_updates (
  name TEXT,
  price DECIMAL (10, 2),
  stock INTEGER,
  status TEXT
);

-- Insert mixed update data (new products, updates, and discontinuations)
INSERT INTO product_updates VALUES
  ('Laptop', 1099.99, 75, 'active'),     -- Update: price and stock change
  ('Monitor', 299.99, 30, 'active'),     -- Insert: new product
  ('Keyboard', NULL, 0, 'discontinued'), -- Delete: mark as discontinued
  ('Headphones', 89.99, 50, 'active');       -- Insert: another new product
```

### Using MERGE with RETURNING ###
1. To handle all three operations (`INSERT`, `UPDATE`, `DELETE`) while providing detailed feedback through the `RETURNING` clause.

```
MERGE INTO products p
USING product_updates u
ON p.name = u.name
WHEN MATCHED AND u.status = 'discontinued' THEN
  DELETE
WHEN MATCHED AND u.status = 'active' THEN
  UPDATE SET
    price = COALESCE(u.price, p.price),
	stock = u.stock,
	status = u.status,
	last_updated = CURRENT_TIMESTAMP
WHEN NOT MATCHED AND u.status = 'active' THEN
  INSERT (name, price, stock, status)
  VALUES (u.name, u.price, u.stock, u.status)
RETURNING
  merge_action() as action,
  p.product_id,
  p.name,
  p.price,
  p.stock,
  p.status,
  p.last_updated;
```

### Understanding the Output ###
1. `UPDATE` - Laptop's price and stock were updated
2. `DELETE` - Keyboard is deleted from the products table
3. `INSERT` - New monitor and headphones products were added
4. Check:

```
SELECT * FROM products
ORDER BY product_id;
```

### Advanced Usage with Conditions ###

```
MERGE INTO products p
USING (
  SELECT
    name,
	price,
	stock,
	status,
	CASE
	  WHEN price IS NULL AND status = 'discontinued' THEN 'DELETE'
	  WHEN stock = 0 THEN 'OUT_OF_STOCK'
	  ELSE status
	END as action_type
) u
ON p.name = u.name
WHEN MATCHED AND u.action_type = 'DELETE' THEN
  DELETE
WHEN MATCHED AND u.action_type = 'OUT_OF_STOCK' THEN
  UPDATE SET
    status = 'inactive',
	stock = 0,
	last_updated = CURRENT_TIMESTAMP
WHEN MATCHED THEN
  UPDATE SET
    price = COALESCE(u.price, p.price),
	stock = u.stock,
	status = u.status,
	last_updated = CURRENT_TIMESTAMP
WHEN NOT MATCHED AND u.action_type != 'DELETE' THEN
  INSERT (name, price, stock, status)
  VALUES (u.name, u.price, u.stock, u.status)
RETURNING
  merge_action() as action,
  p.*,
  u.action_type;
```

### Best Practices ###
1. Handle Source Data Carefully
	1. Validate input data before the `MERGE`
	2. Use subqueries to transform or clean data 
	3. Consider using CTEs for complex data preparation
2. Leverage RETURNING for Validation
	1. Include the `merge_action()` for operation tracking
	2. Consider returning both old and new values for logging purposes and validation

### Common Pitfalls to Avoid ###
1. Ambiguous Matches: Ensure your `ON` clause generates unique matches
2. NULL Handling: Use `COALESCE` or `IS NOT DISTINCT FROM` for `NULL` values (?)
3. Missing Conditions: Always handle all possible cases in your `WHEN` clauses

#### What is `IS NOT DISTINCT FROM`? ####

In SQL, the `IS NOT DISTINCT FROM` operator is a **null-safe equality check**. Unlike a simple `=` comparison, this always returns **TRUE or FALSE**, never **UNKNOWN**, even when comparing `NULL` values.

---

### 🔍 Behavior Highlights (per the SQL standard and PostgreSQL docs)

* **Non-null inputs**:
  Behaves just like `=`.

  * `5 IS NOT DISTINCT FROM 5` → **TRUE**
  * `5 IS NOT DISTINCT FROM 3` → **FALSE**

* **Both NULLs**:
  Treated as equal → **TRUE**

  * `NULL IS NOT DISTINCT FROM NULL` → **TRUE**

* **One NULL, one non-NULL**:
  Treated as not equal → **FALSE**

  * `5 IS NOT DISTINCT FROM NULL` → **FALSE**
  * `NULL IS NOT DISTINCT FROM 5` → **FALSE** ([wiki.postgresql.org][1], [Wikipedia][2], [Database Administrators Stack Exchange][3], [Stack Overflow][4])

---

### 🧩 Truth Table Summary

| A    | B    |     `A = B`    | `A IS NOT DISTINCT FROM B` |
| :--- | :--- | :------------: | :------------------------: |
| 5    | 5    |      TRUE      |            TRUE            |
| 5    | 3    |      FALSE     |            FALSE           |
| 5    | NULL | UNKNOWN (NULL) |            FALSE           |
| NULL | NULL | UNKNOWN (NULL) |            TRUE            |

`A = B` gives **UNKNOWN** when any operand is `NULL`, but `IS NOT DISTINCT FROM` transforms that into a definitive TRUE or FALSE ([modern-sql.com][5], [PostgreSQL][6]).

---

### 🚀 Why It's Useful

1. **NULL-safe comparisons**
   You can use it in `WHERE` or `JOIN` clauses without worrying about `NULL` values messing up your logic:

   ```sql
   WHERE col1 IS NOT DISTINCT FROM col2
   ```

2. **Cleaner alternative to verbose logic**
   Instead of writing:

   ```sql
   WHERE (col1 = col2 OR (col1 IS NULL AND col2 IS NULL))
   ```

   you can simply write:

   ```sql
   WHERE col1 IS NOT DISTINCT FROM col2
   ```

3. **Standard SQL behavior**
   It's part of SQL:1999 and SQL:2003 standards (feature T152) ([Stack Overflow][4], [Wikipedia][2]), supported in PostgreSQL and other major DBMS (e.g., SQL Server 2022, Oracle, Snowflake, MySQL `<=>`) ([Snowflake][7]).

---

### ✅ Quick Equivalence

* `A IS NOT DISTINCT FROM B` =
  `(A = B) OR (A IS NULL AND B IS NULL)`
* `A IS DISTINCT FROM B` =
  `NOT (A IS NOT DISTINCT FROM B)`

---

### 💡 Final Takeaway

Use `IS NOT DISTINCT FROM` when you want **true/false certainty**, even when comparing fields that might contain `NULL`. It's more concise, easier to read, and negates the unpredictability of three-valued logic when handling `NULL` values.

Let me know if you’d like examples in your specific database!

[1]: https://wiki.postgresql.org/wiki/Is_distinct_from?utm_source=chatgpt.com "Is distinct from - PostgreSQL wiki"
[2]: https://en.wikipedia.org/wiki/Null_%28SQL%29?utm_source=chatgpt.com "Null (SQL)"
[3]: https://dba.stackexchange.com/questions/217324/is-not-distinct-from-vs-row-wise-equality-with?utm_source=chatgpt.com "IS NOT DISTINCT FROM vs row-wise equality with"
[4]: https://stackoverflow.com/questions/10416789/how-to-rewrite-is-distinct-from-and-is-not-distinct-from-in-sql-server-20008r2?utm_source=chatgpt.com "How to rewrite IS DISTINCT FROM and IS NOT DISTINCT FROM in ..."
[5]: https://modern-sql.com/feature/is-distinct-from?utm_source=chatgpt.com "NULL -Aware Comparison: is [not] distinct from - Modern SQL"
[6]: https://www.postgresql.org/docs/current/functions-comparison.html?utm_source=chatgpt.com "17: 9.2. Comparison Functions and Operators - PostgreSQL"
[7]: https://docs.snowflake.com/en/sql-reference/functions/is-distinct-from?utm_source=chatgpt.com "IS [ NOT ] DISTINCT FROM - Snowflake Documentation"

### Conclusion ###
1. `MERGE` and `RETURNING` gives the ability to perform multiple operations in a single statement, and also gives immediate feedback.

### Frequently Asked Questions (FAQ) ###
#### What is the purpose of the `MERGE` statement in PostgreSQL? ####
1. Allows us to conditionally `INSERT`, `UPDATE`, and `DELETE` rows in a target table based on the presence of matching records in a source table.
	1. Consolidates multiple operations into a single, efficient command

#### When was the `MERGE` statement introduced in PostgreSQL? ####
1. PostgreSQL 15

#### How does the `MERGE` statement determine which oepration to perform? ####
1. `ON` condition matches rows between the source and target tables.
	1. Based on whether a match is found (`MATCHED`) or not (`NOT MATCHED`), and any additional conditions, it executes the corresponding `INSERT`, `UPDATE`, `DELETE`, or `DO NOTHING` actions

#### Can I use the `MERGE` statement with views in PostgreSQL? ####
1. From PostgreSQL 17, `MERGE` can be used with updatable views
	1. However, the views must be consistent
2. Trigger-updatable views need `INSTEAD OF` triggers for all actions
3. Auto-updatable views cannot have any triggers
4. Mixing types of views or using rule-updatable views is not allowed

#### What privileges are required to execute a `MERGE` statement? ####
1. `SELECT` privilege on the source table or query.
2. `INSERT` privilege on target table for insert actions.
3. `UPDATE` privilege on target table for update actions.
4. `DELETE` privilege on target table for delete actions.

#### Is the `MERGE` statement atomic in PostgreSQL? ####
1. Yes.
	1. All specified actions are performed as a single unit
	2. If an error occurs during execution, the entire operation is rolled back, ensuring data integrity

#### Can I use the `RETURNING` clause with the `MERGE` statement? ####
1. Yes. Starting from PostgreSQL 17
	1. Allows us to retrieve information about rows affected by the `MERGE` operation - shows the specific operation performed (`INSERT`, `UPDATE`, or `DELETE`) on each row

#### How does the `MERGE` statement handle concurrent data modifications? ####
1. `MERGE` ensures data consistency during concurrent operations by acquiring the necessary locks on target table
	1. It prevents other transactions from modifying the same rows simultaneously (avoids conflicts)

#### Are there any performance considerations when using the `MERGE` statement? ####
1. `ON` condition must be well-optimized - index the columns involved
	1. Proper indexing can significantly enhance performance

#### Can I perform different actions based on additional conditions within the `MERGE` statement? ####
1. `MERGE` allows multiple `WHEN` clauses with additional conditions
	1. Enables us to specify different actions (`INSERT`, `UPDATE`, `DELETE`, or `DO NOTHING`) based on various criteria
		1. Gives fine-grained control

## PostgreSQL Transaction ##
1. Summary: Learn how to handle `BEGIN`, `COMMIT` and `ROLLBACK` statements

### What is a database transaction? ###
1. Transaction: A single unit of work that consists of one or more operations
2. Example: A bank transfer from one account to another
	1. A complete transaction must ensure a balance between the sender and receiver accounts
		1. If a sender account transfers X amount, the receiver receives exactly X amount (neither more nor less)
3. PostgreSQL transaction is:
	1. Atomic
		1. Guarantees that the transaction is completed in all-or-nothing manner.
	2. Consistent
		1. Ensures that changes to data written to the database are valid and adhere to predefined rules.
	3. Isolated
		1. Determines how the integrity of a transaction is visible to other transactions.
	4. Durable
		1. Ensures that transactions that have been committed are permanently stored in the database.

### Setting up a sample table ###
1. `accounts`

```sql
DROP TABLE IF EXISTS accounts;

CREATE TABLE accounts (
    id INT GENERATED BY DEFAULT AS IDENTITY,
	name VARCHAR(100) NOT NULL,
	balance DEC(15, 2) NOT NULL CHECK (balance >= 0),
	PRIMARY KEY (id)
);
```

### Begin a transaction ###
1. When we execute a statement, PostgreSQL implicitly wraps it in a transaction.
	1. Example:
	
	```
	INSERT INTO accounts (name, balance)
	VALUES ('Bob', 10000);
	```
	
2. To start a transaction explicitly, execute either of the following statements:

```
BEGIN TRANSACTION;
```

```
BEGIN WORK;
```

```
BEGIN;
```

3. Example: The following statements start a new transaction and insert a new account into the `accounts` table:

```
BEGIN;

INSERT INTO accounts (name, balance)
VALUES ('Alice', 10000);
```

4. From the **current session**, we can see the change by retrieving data from the `accounts` table:

```sql
SELECT
    id, 
	name,
	balance
FROM 
    accounts;
```

	1. We will not see the change if we connect to PostgreSQL server in a new session and execute the following query:
	
	```sql
	SELECT
	    id,
		name,
		balance
	FROM
	    accounts;
	```

### Commit a transaction ###
1. To permanently apply a change to the db, commit the transaction by using the `COMMIT WORK` statement;

```
COMMIT WORK;
```

```
COMMIT TRANSACTION;
```

```
COMMIT;
```

2. Other sessions can view the change by retrieving data from the `accounts` table

```sql
SELECT
    id,
	name,
	balance
FROM
    accounts;
```

3. After executing the `COMMIT` statement, PostgreSQL guarantees that the change will be durable if a crash happens.

```sql
-- start a transaction
BEGIN;

-- insert a new row into the accounts table
INSERT INTO accounts (name, balance)
VALUES ('Alice', 10000);

-- commit the change (or roll it back later)
COMMIT;
```

### Roll back a transaction ###
1. If we want to undo the changes in the DB, we use `ROLLBACK` statement.

```
ROLLBACK;
```

```
ROLLBACK TRANSACTION;
```

```
ROLLBACK WORK;
```

2. `ROLLBACK` undos the changes that you made within the transaction
	1. Example: The following example rolls back changes made to the account 1
	
	```sql
	-- start transaction
	BEGIN;
	
	UPDATE accounts
	SET balance = balance - 1000
	WHERE id = 1;
	
	-- rollback the changes
	ROLLBACK;
	```
	
	2. If you retrieve data from the accounts table, you won't see the changes
	
	```sql
	SELECT * FROM accounts;
	```
	
3. In practice, transactions are used in stored procedures, or application code.

### Summary ###
1. Use `BEGIN` to explicitly start a transaction
2. Use `COMMIT` to explicitly apply the changes permanently to the database
3. Use the `ROLLBACK` statement to undo the changes made to the database during the transaction

## Import CSV File Into PostgreSQL Table ##
1. Summary: Various ways to import CSV file into a PosgreSQL table
2. Example: New table named `persons` with following columns:

```
id: the person id
first_name: first name
last_name: last name
dob: date of birth
email: the email address
```

```sql
CREATE TABLE persons (
    id SERIAL,
	first_name VARCHAR(50),
	last_name VARCHAR(50),
	dob DATE,
	email VARCHAR(255),
	PRIMARY KEY (id)
);
```

3. CSV data file with the following format:

```csv
First Name,Last Name,Date of Birth,Email
John,Doe,1990-01-05,doe@postgresqltutorial.com
Lily,Bush,1995-02-05,lily.bush@postgresqltutorial.com
```

	1. The path of the CSV file: `C:\sampledb\persons.csv`

### Import a CSV file into a table using COPY statement ###
1. To import, we use `COPY` statement:

```sql
COPY persons (first_name, last_name, dob, email)
FROM 'C:\sampledb\persons.csv'
DELIMITER ','
CSV HEADER;
```

```
COPY 2
```

2. Explanation:
	1. Specify table name after `COPY`
	2. Specify column names after the table name
		1. The order of the columns must be the same as the ones in the CSV file
		2. If CSV file contains all columns of the table, we don't need to specify them explicitly
			1. Example:
			
			```sql
			COPY sample_table_name
			FROM 'C:\sampledb\sample_data.csv'
			DELIMITER ','
			CSV HEADER;
			```
	3. Put CSV path after `FROM`
	4. CSV needs `DELIMITER` and `CSV` clauses
		1. `HEADER` - indicates that the CSV file contains a header
			1. When `COPY` command imports data, it ignores the header of the file.

### Import a CSV file into a table using pgAdmin ###
1. To import a CSV file from the computer into a table on PostgreSQL database server, use pgAdmin.
2. To truncate `persons` table:

```sql
TRUNCATE TABLE persons
RESTART IDENTITY;
```

3. Right click `persons` table and select **Import/Export...**
4. Switch to import
5. Browse to the import file
6. Select the format as CSV
7. Check **Header**
8. Select the delimiter as `,`
9. Click **columns** tab
	1. Uncheck `id` column
10. Click **OK** button

## Export PostgreSQL Table to CSV File ##
1. Summary: Various techniques to export data from PostgreSQL tables to CSV files.
2. Retrieve data from `persons` table:

```sql
SELECT * FROM persons;
```

### Export data from a table to CSV using the COPY statement ###
1. `COPY` statement allows us to export data from a table to a CSV file.
2. Example:

```sql
COPY persons 
TO 'C:\temp\persons_db.csv'
DELIMITER ','
CSV HEADER;
```

	1. `COPY` exports all data from all columns of `persons` table to `persons_db.csv` file
	
3. To export data from some columns of a table to a CSV file
	1. Specify column names together with table name after `COPY`
4. Example:

```sql
COPY persons (first_name, last_name, email)
TO 'C:\temp\persons_partial_db.csv'
DELIMITER ','
CSV HEADER;
```

5. To remove header, remove `HEADER` flag

```sql
COPY persons (email)
TO 'C:\Program Files\PostgreSQL\17\data\persons_email_db.csv'
DELIMITER ','
CSV;
```

	1. The CSV file is written in the server and not the local machine
	
### Export data from a table to a CSV file using the \copy command ###
1. For remote PostgreSQL server, use `\copy`
	1. `\copy` runs `COPY` behind the scenes
		1. Instead of the server, PSQL writes the CSV file and transfers data from the server to your local file system
2. `\copy` needs to have sufficient privileges to local machine & not PostgreSQL superuser privileges.
3. Example:

```sql
\copy (SELECT * FROM persons) to 'C:\Program Files\PostgreSQL\17\data\persons_client.csv' with csv
```

## PostgreSQL Data Types ##
1. Summary: PostgreSQL data types - Boolean, Character, Numeric, Temporal, Array, JSON, UUID, and Special types.

### PostgreSQL Data Types Overview of PostgreSQL data types ###
1. Types supported
	1. Boolean
	2. Character types: `char`, `varchar`, `text`.
	3. Numeric types: Integers and floating point numbers
	4. Temporal types such as `date`, `time`, `timestamp`, `interval`.
	5. UUID: For storing Universally Unique Identifiers
	6. Array: For storing array strings, numbers, etc.
	7. JSON: Stores JSON data
	8. hstore: stores key-value pair
	9. Special types such as network address and geometric data

### Boolean ###
1. Boolean - It can hold one of three possible values
	1. Use `boolean` or `bool` to declare **(M)**
2. When we insert data into Boolean column, PostgreSQL converts it to a Boolean value
	1. `1`, `yes`, `y`, `t`, `true` are converted to `true`
	2. `0`, `no`, `f`, `false` are converted to `false`
3. When we select data from the Boolan column, PostgreSQL converts the values back.
	1. `t` to `true`
	2. `f` to `false`
	3. `space` to `null`

### Character ###
1. Three character data types: `CHAR(n)`, `VARCHAR(n)`, and `TEXT` **(M)**
	1. `CHAR(n)`: Fixed-length character with space padded.
		1. If you inserted a string that is shorter than the length of the column, PostgreSQL pads spaces.
		2. If you insert a string that is longer than the length of the column, PostgreSQL will issue an error.
	2. `VARCHAR(n)`: Variable length character string.
		1. It allows us to store up to `n` characters.
		2. If you inserted a string that is shorter than the length of the column, PostgreSQL doenot pad spaces.
	3. `TEXT`: Variable length character string.
		1. Text data is a character string with unlimited length (theoretically)

### Numeric ###
1. Two distinct type of numbers:
	1. Integers
	2. Floating-point numbers

#### Integer ####
1. Three kinds of integers in PostgreSQL:
	1. `SMALLINT` **(M)**: It is a 2-byte signed integer that has a range from -32,768 to 32,767
	2. `INT` **(M)**: It is a 4-byte signed integer that has a range from -2^31 to 2^31 - 1.
	3. `SERIAL` **(M)**: It is similar to integer, but PostgreSQL will automatically generate and populate values into the column.
		1. It is similar to `AUTO_INCREMENT` column in MySQL or `AUTOINCREMENT` column in SQLite.

#### Floating-point number ####
1. Three main types of floating-point numbers:
	1. `float(n)` **(M)**: floating-point number whose precision, is at least, n, up to a maxium of 8 bytes.
	2. `real`, or `float8` **(M)**: It is a 4-byte floating-point number
	3. `numeric` or `numeric(p, s)` **(M)**: Real number with p digits with s number after the decimal point (it is the exact number).

### Temporal Data Types ###
1. To store date and/or time data.
2. There are five main temporal data types:
	1. `DATE` **(M)**: Stores dates only
	2. `TIME` **(M)**: Stores time of the day values.
	3. `TIMESTAMP` **(M)**: Stores both date and time values.
	4. `TIMESTAMPZ` **(M)**: Timezone-aware timestamp data type. Timestamp with the timezone.
		1. An extension to SQL standard's temporal date types.
	5. `INTERVAL` **(M)**: Stores periods.

### Arrays ###
1. PostgreSQL allows storing array of strings, array of integers, ... in array columns
	1. Application: Storing days of the week, months of the year, etc.

### JSON ###
1. PostgreSQL provides two JSON data types: `JSON`, and `JSONB` for storing JSON data.
	1. `JSON`: It stores plain JSON data that requires reparsing for each processing. (?)
		1. Every time you query or manipulate the data (e.g., extract a key or run a filter), PostgreSQL must re-parse the JSON string to understand its structure.
			So:
				1. It's slower for querying or indexing.
				2. It uses more CPU during reads because of the repeated parsing.
				3. It’s faster for raw insertion (no upfront parsing).
	2. `JSONB`: Stores `JSON` data in a binary format which is faster to process but slower to insert.
		1. It also supports indexing (for performance)

### UUID ###
1. `UUID`: Allows us to store universal identifiers defined by [RFC 4122](https://tools.ietf.org/html/rfc4122)
	1. The values guarantee a better uniqueness than `SERIAL`
	2. They can be used to hide sensitive data exposed to the public such as values of `id` in URL.

### Special data types ###
1. They are related to geometry and network.
	1. `box`: a rectangular box
	2. `line`: a set of points
	3. `point`: a geometric pair of numbers
	4. `lseg`: a line segment
	5. `polygon`: a closed geometric
	6. `inet` **(M)**: an IP4 address
	7. `macaddr` **(M)**: a MAC address

## PostgreSQL CREATE TABLE ##
1. Summary: PostgreSQL CREATE TABLE statement

### Introduction to PostgreSQL CREATE TABLE statement ###
1. New table creation:

```sql
CREATE TABLE [IF NOT EXISTS] table_name (
  column1 datatype(length) column_constraint,
  column2 datatype(length) column_constraint,
  ...
  table_constraints
);
```

	1. The table name must be unique in a schema
		1. We will get an error if we try table creation with the same name in the schema.
	2. Schema: A named collection of database objects (tables, ...)
		1. `public` is the default schema (if we don't use a name for table creation)
	3. `IF NOT EXISTS`: Table is created only if it does not exist.
		1. If used, PostgreSQL only issues a notice isntead of an error.
	4. Table columns must be separated by `,`s
		1. Each column definition consists of:
			1. Column name
			2. Data type
			3. Size
			4. Constraint
				1. It specifies a rule that is applied to the data within a column to ensure data integrity.
				2. Examples:
					1. `PRIMARY KEY`
					2. `FOREIGN KEY`
					3. `NOT NULL`
						1. Ensures that the value in the column cannot be `NULL`
					4. `UNIQUE`
					5. `CHECK`
					6. `DEFAULT`
				3. It specifies table constraint:
					1. `PRIMARY KEY`
					2. `FOREIGN KEY`
					3. `UNIQUE`
					4. `CHECK`

#### Constraints ####
1. Columns constraints:
	1. `NOT NULL`: Ensures that the values in a column cannot be `NULL`
	2. `UNIQUE`: Ensures the values in a column are unique across the rows within the same table
	3. `PRIMARY KEY`: It uniquely identifies rows in a table.
		1. A table can have one and only one primary key.
		2. It allows us to define the primary key of the table.
	4. `CHECK`: Ensures that the data must satisfy a boolean expression.
		1. Example: Value in the price column must be zero or positive.
	5. `FOREIGN KEY`: Ensures that the values in a column or a group of columns from a table exist in a column or group of columns in another table.
		1. A table can have many foreign keys.
2. Table constraints:
	1. Similar to column constraints, but we can include more than one column in the table constraint.

### PostgreSQL CREATE TABLE example ###
1. Example: `accounts` table in `dvdrental` database.
	1. Columns:
		1. `user_id`: primary key
		2. `username`: unique and not null
		3. `password`: not null
		4. `email`: unique and not null
		5. `created_at`: not null
		6. `last_login`: null
	2. Statement:
	
	```sql
	CREATE TABLE accounts (
	  user_id SERIAL PRIMARY KEY,
	  username VARCHAR (50) UNIQUE NOT NULL,
	  password VARCHAR (50) NOT NULL,
	  email VARCHAR (255) UNIQUE NOT NULL,
	  created_at TIMESTAMP NOT NULL,
	  last_login TIMESTAMP
	);
	```
	
		1. To view the table: In `PLSQL`, run `\d accounts` **(M)**

### Summary ###
1. `IF NOT EXISTS` to generate a table only if it does not exist.

## PostgreSQL SELECT INTO ##
1. Summary: `SELECT INTO` is used for creation of a new table from the result set of a query
	1. [PL/pgSQL SELECT INTO statement](https://neon.com/postgresql/postgresql-plpgsql/pl-pgsql-select-into) - to select data into variables.

### Introduction to PostgreSQL SELECT INTO statement ###
1. `SELECT INTO` statement is used for the creation of new table and insert data returned from a query into the table.
	1. The new table will have columns with the same names as the columns of the result set of the query.
	2. It does not return result to the client (unlike the `SELECT` statement).
2. Basic syntax:

```sql
SELECT
  select_list
INTO [ TEMPORARY | TEMP ] [ TABLE ] new_table_name
FROM
  table_name
WHERE
  search_condition;
```

	1. `INTO`: For the creation of a new table.
	2. `TEMP`, `TEMPORARY`: Allows the creation of a temporary table.
	3. `TABLE`: Optional to enhance the clarity of the statement.
	4. `WHERE`: To specify teh condition that determines which rows from the original table should be filled into the new table.
		1. We can use other clauses:
			1. `INNER JOIN`
			2. `LEFT JOIN`
			3. `GROUP BY`
			4. `HAVING`
	5. `SELECT INTO` clause cannot be used in PL/pgSQL.
		1. `INTO` is interpreted differently.
		2. Use `CREATE TABLE AS` instead.

### PostgreSQL SELECT INTO examples ###
1. Using `film` table: [sample database](https://neon.com/postgresql/postgresql-getting-started/postgresql-sample-database)

#### Basic PostgreSQL SELECT INTO statement example ####
1. `SELECT INTO`: For a table called `film_r` - films with rating `R` and rental duration 5 days from the `film` table.

```sql
SELECT
  film_id,
  title,
  rental_rate
INTO
  film_r
FROM
  film
WHERE
  rating = 'R'
AND rental_duration = 5
ORDER BY
  title;
```

	1. To verify: `SELECT * FROM film_r;`

#### Using the SELECT INTO statement to generate a new temporary table ####
1. Temporary table named `short_film` that contains films whose lengths are under 60 minutes.

```sql
SELECT
  film_id,
  title,
  length
INTO TEMPORARY TABLE short_film
FROM
  film
WHERE
  length < 60
ORDER BY
  title;  
```

	1. To verify:
	
	```sql
	SELECT * FROM short_film
	ORDER BY length DESC;
	```

### Summary ###
1. `SELECT INTO`: For creation of table form the result set of a query.

## PostgreSQL CREATE TABLE AS ##
1. Summary: How to use `CREATE TABLE AS` for creation of new table from result set of a query.

### Introduction to the PostgreSQL CREATE TABLE statement ###
1. `CREATE TABLE AS`: A new table is created and filled with data returned by a query.
2. Syntax:

```sql
CREATE TABLE new_table_name
AS query;
```

	1. Specify table name after `CREATE TABLE` clause.
	2. Provide a query whose result set is added to the new table after the `AS` keyword.
3. `TEMPORARY` or `TEMP` keyword can be used for temporary tables

```sql
CREATE TEMP TABLE new_table_name
AS query;
```

4. The `UNLOGGED` keyword allows the new table to be created as an unlogged table.

```sql
CREATE UNLOGGED TABLE new_table_name
AS query;
```

### PostgreSQL CREATE TABLE AS statement examples ###
1. Using `film` and `film_category` tables.
2. Example: Creation of new table that contains the films whose category is 1.

```sql
CREATE TABLE action_film
AS
SELECT
  film_id,
  title,
  release_year,
  length,
  rating
FROM 
  film
INNER JOIN film_category USING (film_id)
WHERE
  category_id = 1;
```

3. To verify table creation:

```sql
SELECT * FROM action_films
ORDER BY title;
```

4. Check the structure of the `action_film`

```psql
\d action_film
```

5. The names and data types of `action_film` table are derived from the columns of the `SELECT` clause.
6. If the `SELECT` clause contains expressions, we can override the column names:

```sql
CREATE TABLE IF NOT EXISTS film_rating (rating, film_count)
AS
SELECT
  rating,
  COUNT (film_id)
FROM
  film
GROUP BY
  rating;
```

	1. Check the structure of the table: `\c film_rating`
	
7. `CREATE TABLE AS` is similar to `SELECT INTO`, but former is preferred, because it is not confused with other uses of `SELECT INTO` syntax in PL/pgSQL.
	1. The former also provides superset of functionality offered by the latter.

### Summary ###
1. `CREATE TABLE AS` is used for creation of a table from the result of a query.

## Using PostgreSQL SERIAL to Construct Auto-Increment Column ##
1. Summary: `SERIAL` pseudo-type
	1. To use `SERIAL` pseudo-type to define auto-increment columns in table.

### Introduction to the PostgreSQL SERIAL pseudo-type ###
1. `sequence` - a special kind of database object that generates a sequence of integers
	1. It is often used as a primary key column in a table.
2. A `sequence` can be created through `SERIAL` pseudo-type

```sql
CREATE TABLE table_name (
  id SERIAL
);
```

	1. PostgreSQL performs the following:
		1. First: Generates a sequence object and set the next value generated by the sequence as the default value for the column.
		2. Second: Add a `NOT NULL` constraint to the `id` column because a sequence always generates an integer (a non-null value).
		3. Third: Assign the owner of the sequence to the `id` column
			1. If column or table is dropped, the sequence object is also deleted.
	2. The statement is equivalent to:
	
	```sql
	CREATE SEQUENCE table_name_id_seq;
	
	CREATE TABLE table_name (
	  id INTEGER NOT NULL DEFAULT nextval('table_name_id_seq')
	);
	
	ALTER SEQUENCE table_name_id_seq
	OWNED BY table_name.id;
	```
	
3. PostgreSQL provides three serial pseudo-types: `SMALLSERIAL`, `SERIAL`, and `BIGSERIAL`
	1. `SMALLSERIAL`: 2 bytes
	2. `SERIAL`: 4 bytes
	3. `BIGSERIAL`: 8 bytes

### PostgreSQL SERIAL Example ###
#### Basic PostgreSQL SERIAL example ####
1. `SERIAL` does not implicitly generate an index on the column ore make the column the primary key.
	1. Solution: Use `PRIMARY KEY` constraint for the `SERIAL` column.
	
	```sql
	CREATE TABLE fruits (
	  id SERIAL PRIMARY KEY,
	  name VARCHAR NOT NULL
	);
	```
	
2. To assign a default value when inserting a row into the table, ignore the column name or use the `DEFAULT` keyword in the `INSERT` statement.

```sql
INSERT INTO fruits (name)
VALUES ('Orange');
```

```sql
INSERT INTO fruits (id, name)
VALUES (DEFAULT, 'Apple');
```

3. Get all the records:

```
SELECT * FROM fruits;
```

#### Getting the sequence name ####
1. To get the sequence name of a `SERIAL` column in a table, use the `pg_get_serial_sequence()` **(M)**

```sql
pg_get_serial_sequence('table_name', 'column_name');
```

```sql
SELECT pg_get_serial_sequence('fruits', 'id');
```

2. To get the recent value generated by the sequence:

```sql
SELECT currval(pg_get_serial_sequence('fruits', 'id'));
```

#### Retrieving the generated value ####
1. To get the value generated by the sequence when you insert a new row into the table, use `RETURNING id` caluse in the `INSERT` statement.

```sql
INSERT INTO fruits (name)
VALUES ('Banana')
RETURNING id;
```

2. Sequence generator operation is not transaction-safe
	1. If two concurrent database-connections attempt to get the next value from a sequence, each client will get a different value.
	2. If one client rolls back the transaction, the sequence number of that client will be unused.
		1. Causes a gap in the sequence.

#### Adding a serial column to an existing table ####
1. `baskets` table without a primary key column:

```sql
CREATE TABLE baskets (
  name VARCHAR (255) NOT NULL
);
```

2. Add a `SERIAL` column to the `baskets` table.

```sql
ALTER TABLE baskets
ADD COLUMN id SERIAL PRIMARY KEY;
```

3. Describe the table:

```psql
\d baskets
```

### Summary ###
1. `SERIAL`: For auto-increment column for a table.

## PostgreSQL Sequences ##
1. Summary: PostgreSQL sequences and how to use a sequence object to generate sequence numbers

### Introduction to PostgreSQL sequences ###
1. A sequence is a database object that allows us to generate a sequence of unique integers.
2. It is generally used to generate a unique identifier for a primary key in a table.
3. It can be used to generate unique numbers across tables.
4. Use `CREATE SEQUENCE` statement.

### PostgreSQL CREATE SEQUENCE statement ###
1. Syntax:

```sql
CREATE SEQUENCE [ IF NOT EXISTS ] sequence_name
  [ AS { SMALLINT | INT | BIGINT } ]
  [ INCREMENT [ BY ] increment ]
  [ MINVALUE minvalue | NO MINVALUE ]
  [ MAXVALUE maxvalue | NO MAXVALUE ]
  [ START [ WITH ] start ]
  [ CACHE cache ]
  [ [ NO ] CYCLE ]
  [ OWNED BY { table_name.column_name | NONE } ]
```

#### sequence_name ####
1. Name of the sequence.
2. [ IF NOT EXISTS ] conditionally generates a sequence only if it does not exist.
3. The sequence name must be distinct from any other sequences, tables, indexes, views, or foreign key tables in the same schema.

### [ AS { SMALLINT | INT | BIGINT } ] ###
1. Specify the data type of the sequence.
2. Valid data types:
	1. `SMALLINT`
	2. `INT`
	3. `BIGINT` - default type if you skip
3. It is the data type of the sequence which determines the sequence's minimum and maximum values.

### [ INCREMENET [ BY ] increment ] ###
1. `increment` specifies which value to add to the current sequence value.
2. A positive number will make an ascending sequence whereas a negative number will form a descending sequence.
3. Default increment value is 1.

### [ MINVALUE minvalue | NO MINVALUE ] [ MAXVALUE maxvalue | NO MAXVALUE ] ###
1. Defines the minimum value and maximum value of the sequence.
2. `NO MINVALUE` or `NO MAXVALUE` - sequence will use the default value.
	1. For ascending sequence, the default maximum value is the maximum value of the data type of the sequence and the default min value is 1.
	2. For descending sequence, the default maximum value is -1 and the default minimum value is the minimum value of the data type of the sequence.

### [ START [ WITH ] start ###
1. `START` - specifies the starting value of the sequence.
	1. The default starting value is `minvalue` for ascending sequence and `maxvalue` for descending ones.

### cache ###
1. `CACHE` determines how many sequence numbers are preallocated and stored in memory for faster access.
	1. One value can be generated at a time.
2. By default, sequence generates one value at a time
	1. `no cache`

### CYCLE | NO CYCLE ###
1. `CYCLE`: Allows us to restart the value if limit is reached.
	1. The next number will be the minimum value for ascending sequence and maximum value for the descending sequence.
2. `NO CYCLE`: If limit is reached, attempting to get the next value results in error.
	1. It is the default.

### OWNED BY table_name.column_name ###
1. `OWNED BY`: Allows us to associate table column with sequence so that when you drop the column or table, the associated sequence is also dropped.
2. `SERIAL`: PostgreSQL automatically generates a sequence associated with the column.

### PostgreSQL CREATE SEQUENCE examples ###
#### Constructing an ascending sequence example ####
1. New ascending sequence starting from 100 with an increment of 5:

```sql
CREATE SEQUENCE my_sequence
START WITH 100
INCREMENT BY 5;
```

	1. To get next value from the sequence, we use `nextval('my_sequence')` (increments automatically for every call)
	
	```sql
	SELECT nextval('my_sequence');
	```

#### Constructing a descending sequence example ####
1. Descending sequence from 3 to 1 with a cycle option:

```sql
CREATE SEQUENCE three
START WITH 3
MAXVALUE 3
MINVALUE 1
INCREMENT BY -1
CYCLE;
```

	1. Execute the following statement multiple times to see the numbers cycling:
	
	```sql
	SELECT nextval('three');
	```

#### Constructing a sequence associated with a table column ####
1. New table `order_details`:

```sql
CREATE TABLE order_details (
  order_id SERIAL,
  item_id INT NOT NULL,
  item_next VARCHAR NOT NULL,
  price DEC(10, 2) NOT NULL,
  PRIMARY KEY (order_id, 
);
```

2. New sequence associated with the `item_id` column of `order_details` table:

```sql
CREATE SEQUENCE order_item_id
START 10
MINVALUE 10
INCREMENT 10
OWNED BY order_details.order_id;
```

3. Insert three order items into `order_details` table:

```sql
INSERT INTO
  order_details (order_id, item_id, item_text, price)
VALUES
  (100, nextval('order_item_id'), 'DVD Player', 100),
  (100, nextval('order_item_id'), 'Android TV', 550),
  (100, nextval('order_item_id'), 'Speaker', 250);
```

4. Query data:

```sql
SELECT
  order_id,
  item_id,
  item_text,
  price
FROM
  order_details;
```

### Listing all sequences in a database ###
1. Use the following query:

```sql
SELECT
  relname sequence_name
FROM
  pg_class
WHERE
  relkind = 'S';
```

### Deleting sequences ###
1. If a sequence is associated with a table column, it will be automatically dropped once the table column is removed or the table is dropped.
2. Removing a sequence manually:

```sql
DROP SEQUENCE [ IF EXISTS ] sequence_name [, ...]
[ CASCADE | RESTRICT ];
```

	1. `sequence_name` - name of the sequence to be dropped
	2. `[, ...]` - to drop multiple sequences at once
	3. `CASCADE` - To drop objects that depend on the sequence recursively (objects that depend on dependent objects, etc.)

#### PostgreSQL DROP SEQUENCE statement examples ####
1. If we drop the table `order_details`, the sequence `order_item_id`, associated with the `order_id` column of `order_details` table, will be dropped automatically.

```sql
DROP TABLE order_details;
```

## PostgreSQL Identity Column ##
1. Summary: `GENERATED AS IDENTITY` **(M)** constraint used to generate identity column for a table.

### Introduction to PostgreSQL identity column ###
1. PostgreSQL introduced `GENERATED AS IDENTITY`
	1. It allows us to automatically assign a unique number to a column.
2. It is the SQL standard-confirming variant of `SERIAL` column.
3. Syntax:

```sql
column_name type
GENERATED { ALWAYS | BY DEFAULT }
AS IDENTITY[ ( sequence_option ) ]
```

	1. type can be `SMALLINT`, `INT`, or `BIGINT`
	2. `GENERATED ALWAYS`: To always generate value for the identity column.
		1. If we try to insert (or update) values into the `GENERATED ALWAYS AS IDENTITY` column, PostgreSQL will issue an error.
	3. `GENERATED BY DEFAULT`: To generate a value for the identity column.
		1. If we supply a value for insert or update, PostgreSQL will use the value to insert into the identity column instead of using the system-generated value.
4. PostgreSQL allows a table to have more than one identity column.
	1. `GENERATED AS IDENTITY` also uses `SEQUENCE` object internally.

### PostgreSQL identity column examples ###
#### GENERATED ALWAYS example ####
1. New table: `color` with `color_id` as identity column.

```sql
CREATE TABLE color
  color_id INT GENERATED ALWAYS AS IDENTITY,
  color_name VARCHAR NOT NULL,
);
```

2. Insert a new row into the `color` table:

```sql
INSERT INTO color (color_name)
VALUES ('Red');
```

```sql
INSERT INTO color (color_id, color_name)
VALUES (DEFAULT, 'Blue');
```

3. Verify:

```sql
SELECT * FROM color;
```

4. Insert a row by supplying values for both `color_id` and `color_name` columns:

```sql
INSERT INTO color (color_id, color_name)
VALUES (2, 'Green');
```

```
ERROR:  cannot insert a non-DEFAULT value into column "color_id"
Column "color_id" is an identity column defined as GENERATED ALWAYS. 

SQL state: 428C9
Detail: Column "color_id" is an identity column defined as GENERATED ALWAYS.
Hint: Use OVERRIDING SYSTEM VALUE to override.
```

5. Use `OVERRIDING SYSTEM VALUE` **(M)** to fix the issue.

```sql
INSERT INTO color (color_id, color_name)
OVERRIDING SYSTEM VALUE
VALUES (3, 'Green');
```

#### GENERATED BY DEFAULT AS IDENTITY example ####
1. Drop `color` and re-generate it. Use `GENERATED BY DEFAULT AS IDENTITY` instead:

```sql
DROP TABLE color;

CREATE TABLE color (
  color_id INT GENERATED BY DEFAULT AS IDENTITY,
  color_name VARCHAR NOT NULL
);
```

2. Insert a row into the `color` table:

```sql
INSERT INTO color (color_id, color_name)
VALUES (2, 'Yellow');
```

#### Sequence options example ####
1. `GENERATED AS IDENTITY` constraint uses `SEQUENCE` object
	1. We can specify sequence options for system-generated values.
2. Example: Specify starting value and increment:

```sql
CREATE TABLE color (
  color_id GENERATED ALWAYS AS IDENTITY (START WITH 10 INCREMENT BY 10),
  color_name VARCHAR NOT NULL
);
```

3. Insert a new row:

```sql
INSERT INTO color (color_name)
VALUES ('Orange');
```

4. Verify:

```sql
SELECT * FROM color;
```

5. Insert another row:

```sql
INSERT INTO color (color_name)
VALUES ('Purple');
```

6. Verify:

```sql
SELECT * FROM color;
```

### Adding an identity column to an existing table ###
1. Using `ALTER TABLE` statement:

```sql
ALTER TABLE table_name
ALTER COLUMN column_name
ADD GENERATED { ALWAYS | BY DEFAULT } AS IDENTITY { (sequence_option) }
```

2. Example:

```sql
CREATE TABLE shape (
  shape_id INT NOT NULL,
  shape_name VARCHAR NOT NULL
);
```

3. Change `shape_id` column to identity column:

```sql
ALTER TABLE shape
ALTER COLUMN shape_id
ADD GENERATED ALWAYS AS IDENTITY;
```

	1. `shape_id` must have `NOT NULL` constraint for it to work.
		1. Otherwise, you will get an error.
		
		```sql
		ERROR:  column "shape_id" of relation "shape" must be declared NOT NULL before identity can be added
		SQL state: 55000
		```
		
4. Describe the `shape` table:

```
\d shape
```

### Changing an identity column ###
1. To change the characteristics of existing identity column:

```sql
ALTER TABLE table_name
ALTER COLUMN column_name
{ SET GENERATED { ALWAYS | BY DEFAULT } |
  SET sequence_option | RESTART [ [ WITH ] ] restart ] }
```

2. Example:

```sql
ALTER TABLE shape
ALTER COLUMN shape_id
SET GENERATE AS DEFAULT;
```

3. Describe the table:

```
\d shape
```

### Removing the GENERATED AS IDENTITY constraint ###
1. Removed `GENERATED AS IDENTITY`:

```sql
ALTER TABLE shape
ALTER COLUMN shape_id
DROP IDENTITY IF EXISTS;
```

## PostgreSQL Generated Columns ##
1. Summary: Learn about PostgreSQL generated columns whose values are automatically calculated from other columns.

### Introduction to PostgreSQL Generated Columns ###
1. A generated column is a special type of column whose values are automatically calculated based on expression or values from other columns.
2. Similar to: Computed column in SQL Server, and virtual column in Oracle.
3. Two kinds of generated columns:
	1. Stored: Stored generated column is calculated when it is inserted or updated and occupies storage space.
		1. It is similar to materialized view.
			1. But PostgreSQL automatically updates data for stored generated columns, unlike materialized view.
				1. **PostgreSQL currently implements only stored generated columns**
	2. Virtual: Virtual generated column is computed when it is read and does not occupy storage space.
		1. It is like a view.

#### Defining generated columns ####
1. We typically define generated column when defining a table:

```sql
CREATE TABLE table_name (
  ...,
  column_name type GENERATED ALWAYS AS (expression) STORED | VIRTUAL,
  ...
);
```

	1. `column_name`: Name of generated column.
	2. `type`: data type for the column.
	3. `expression`: Expression that returns values for the calculated column.
	4. `STORED`: Indicates that the data of the generated column is physically stored in the table.
	5. `VIRTUAL`: Indicates that the data of the generated column is computed when queried, not stored physically.
2. To add a generated column to a table:

```sql
ALTER TABLE table_name
ADD column_name type GENERATED ALWAYS AS (expression) STORED;
```

3. An `expression` must meet the following requirements:
	1. It can use only immutable functions and cannot involve subqueries or reference anything behond the current row.
		1. Example: It cannot use `CURRENT_TIMESTAMP` function.
	2. It cannot reference another generated column or a system column, except `tableoid`.
	3. It cannot have a default value or an identity definition.
	4. It cannot be part of a partition key.

### PostgreSQL Generated Column examples ###
#### Concatenated columns ####
1. Table `contacts`:

```sql
CREATE TABLE contacts (
  id SERIAL PRIMARY KEY,
  first_name VARCHAR (50) NOT NULL,
  last_name VARCHAR (50) NOT NULL,
  full_name VARCHAR (101) GENERATED ALWAYS AS (first_name || ' ' || last_name) STORED,
  email VARCHAR (300) UNIQUE
);
```

2. Example: values of `full_name` column will be automatically updated from the values in `first_name` and `last_name` columns.

```sql
INSERT INTO contacts (first_name, last_name)
VALUES
  ('John', 'Doe', 'john.doe@example.com'),
  ('Jane', 'Doe', 'jane.doe@example.com')
RETURNING *;
```

#### Calculating net prices ####
1. Table `products` that stores the product information:

```sql
CREATE TABLE products (
  id SERIAL PRIMARY KEY,
  name VARCHAR (100) NOT NULL,
  list_price DECIMAL (10, 2) NOT NULL,
  tax DECIMAL (5, 2) DEFAULT 0,
  discount DECIMAL (5, 2) DEFAULT 0,
  net_price DECIMAL (10, 2) GENERATED ALWAYS AS ((list_price + (list_price * tax / 100)) - (list_price * discount / 100)) STORED
);
```

2. Insert rows:

```sql
INSERT INTO products (name, list_price, tax, discount)
VALUES
  ('A', 100.00, 10.00, 5.00),
  ('B', 50.00, 8.00, 0.00),
  ('C', 120.00, 12.50, 10.00)
RETURNING *;
```

### Summary ###

## PostgreSQL ALTER TABLE ##
1. Summary: To use PostgreSQL `ALTER TABLE` to modify the structure of a table.

### Introduction to PostgreSQL ALTER TABLE statement ###
1. `ALTER TABLe`: Used to change the structure of an existing table.
2. Syntax:

```sql
ALTER TABLE table_name action;
```

	1. Actions:
		1. Add a column
		2. Drop a column
		3. Change the data type of a column
		4. Rename a column
		5. Set a default value for the column
		6. Add a constraint to a column
		7. Rename a table
3. To add a new column to a table: `ALTER TABLE ADD COLUMN`

```sql
ALTER TABLE table_name
ADD COLUMN column_name datatype column_constraint;
```

4. To drop column from a table: `ALTER TABLE DROP COLUMN`

```sql
ALTER TABLE table_name
DROP COLUMN column_name;
```

5. To rename a column: `[ALTER TABLE RENAME COLUMN](postgresql-rename-column) TO`

```sql
ALTER TABLE table_name
RENAME COLUMN column_name
TO new_column_name;
```

6. To change default value of a column: `ALTER TABLE table_name ALTER COLUMN SET DEFAULT` or `DROP DEFAULT` **(M)**

```sql
ALTER TABLE table_name
ALTER COLUMN column_name
[SET DEFAULT value | DROP DEFAULT];
```

5. To change `NOT NULL` constraint: `ALTER TABLE ALTER COLUMN`

```sql
ALTER TABLE table_name
ALTER COLUMN column_name
[SET NOT NULL | DROP NOT NULL];
```

6. To add `CHECK` constraint: `ALTER TABLE ADD CHECK`

```sql
ALTER TABLE table_name
ADD CHECK expression;
```

7. To add a constraint: `ALTER TABLE ADD CONSTRAINT`

```sql
ALTER TABLE table_name
ADD CONSTRAINT constraint_name constraint_definition;
```

8. To rename a table: `ALTER TABLE RENAME TO`

```sql
ALTER TABLE table_name
RENAME TO new_table_name;
```

### PostgreSQL ALTER TABLE examples ###
1. New table: `links`

```sql
DROP TABLE IF EXISTS links;

CREATE TABLE links (
  link_id SERIAL PRIMARY KEY,
  title VARCHAR (512) NOT NULL,
  url VARCHAR (1024) NOT NULL
);
```

2. To add a new column named `active`:

```sql
ALTER TABLE links
ADD COLUMN active BOOLEAN;
```

3. To remove active column:

```sql
ALTER TABLE links
DROP COLUMN active;
```

4. To change the `title` column to `link_title`:

```sql
ALTER TABLE links
RENAME COLUMN title TO link_title;
```

5. To add new column `target`:

```sql
ALTER TABLE links
ADD COLUMN target VARCHAR (10);
```

6. Set `_blank` as default value for `target` column:

```sql
ALTER TABLE links
ALTER COLUMN target
SET DEFAULT '_blank';
```

	1. To test:
	
	```sql
	INSERT INTO links (link_title, url)
	VALUES ('PostgreSQL Tutorial', 'https://neon.com/postgresql/');
	
	SELECT * FROM links;
	```
	
7. Adding a `CHECK` condition to `target` column so that `target` column accepts only the following values: `_self`, `_blank`, `_parent`, and `_top`:

```sql
ALTER TABLE links
ADD CHECK (target IN ('_self', '_blank', '_parent', '_top'));
```

	1. If we try to insert a new row that violates the `CHECK` constriant, PostgreSQL will issue an error:
	
	```
	ERROR:  new row for relation "links" violates check constraint "links_target_check"
	DETAIL:  Failing row contains (2, PostgreSQL, http://www.postgresql.org/, whatever).DETAIL:  Failing row contains (2, PostgreSQL, http://www.postgresql.org/, whatever).
	```
	
8. Adding `UNIQUE` constraint to `url` column:

```sql 
ALTER TABLE links
ADD CONSTRAINT unique_url UNIQUE (url);
```

```sql
ALTER TABLE table_name
ADD CONSTRAINT constraint_name constraint_definition;
```

9. To change the `links` table to `urls`:

```sql
ALTER TABLE links
RENAME TO urls;
```

## PostgreSQL Rename Table: A Step-by-Step Guide ##
Summary: Renaming a table using `ALTER TABLE RENAME TO`

### Introduction to PostgreSQL RENAME TABLE statement ###
1. Syntax:

```sql
ALTER TABLE table_name
RENAME TO new_table_name;
```

2. To avoid error if the table does not exist, use `IF EXISTS`

```sql
ALTER TABLE IF EXISTS table_name
RENAME TO new_table_name;
```

3. It is not possible to rename multiple tables using a single `ALTER TABLE` statement.

### PostgreSQL rename table examples ###
#### Basic PostgreSQL rename table statement example ####
1. New table:

```sql
CREATE TABLE vendors (
  id SERIAL PRIMARY KEY,
  name VARCHAR NOT NULL
);
```

2. Change the name of the table:

```sql
ALTER TABLE vendors
RENAME TO suppliers;
```

	1. The name of the table changes but the sequence name (`vendors_id_seq`) remains intact

#### Renaming a table that has dependent objects ####
1. Tables: `customers` and `groups`:

```sql
CREATE TABLE customer_groups (
  id SERIAL PRIMARY KEY,
  name VARCHAR NOT NULL
);

CREATE TABLE customers (
  id SERIAL PRIMARY KEY,
  name VARCHAR (255) NOT NULL,
  group_id INT NOT NULL,
  FOREIGN KEY (group_id) REFERENCES customer_group (id)
    ON DELETE CASCADE
	ON UPDATE CASCADE
);
```

2. View based on `customers` and `customer_groups` table:

```sql
CREATE VIEW customer_data
AS SELECT
  c.id,
  c.name,
  g.name customer_group
FROM
  customers c
INNER JOIN customer_groups g ON g.id = c.group_id;
```

3. When we rename a table, PostgreSQL automatically udpates its dependent objects:
	1. Foreign key constraints
	2. Views
	3. Indexes
4. Rename `customer_groups` table to `groups`

```sql
ALTER TABLE customer_groups
RENAME TO groups;
```

	1. Verify the foreign key constraint
	2. Verify view:
	
	```psql
	\d+ customer_data
	```
	
		1. `customer_groups` is updated to `groups` in the `SELECT` statement.

### Summary ###

## PostgreSQL ADD COLUMN: Add One or More Columns to a Table ##
1. Summary: `ADD COLUMN` to add one or more columns to an existing table.

### Introduction to the PostgreSQL ADD COLUMN statement ###
1. Syntax:

```sql
ALTER TABLE table_name
ADD COLUMN new_column_name data_type constraint;
```

	1. PostgreSQL appends the column at the end of the table.
		1. It has not option to specify the position of the new column in the table.
2. To add multiple columns:

```sql
ALTER TABLE table_name
ADD COLUMN column_name1 data_type constraint,
ADD COLUMN column_name2 data_type constriant,
ADD COLUMN column_name3 data_type constraint,
...
ADD COLUMN column_namen data_type constraint;
```

### PostgreSQL ADD COLUMN statement examples ###
#### Adding a new column to a table ####
1. The following statement used for creation of `customers` with two columns: `id` and `customer_name`:

```sql
DROP TABLE IF EXISTS customers CASCADE;

CREATE TABLE customers (
  id SERIAL PRIMARY KEY,
  customer_name VARCHAR (255) NOT NULL
);
```

#### Adding multiple columns to a table ####
1. Add `phone` column to `customers` table using `ALTER TABLE...ADD COLUMN` statement:

```sql
ALTER TABLE customers
ADD COLUMN phone VARCHAR (255);
```

#### Adding a column with a NOT NULL constraint to a table that already has data ####
1. Insert data into `customers` table:

```sql
INSERT INTO
  customers (customer_name)
VALUES
  ('Apple'),
  ('Samsung'),
  ('Sony')
RETURNING *;
```

1. Attempt to add `contact_name` column to the `customers` table:

```sql
ALTER TABLE customers
ADD COLUMN contact_name VARCHAR (255) NOT NULL;
```

	1. `ERROR:  column "contact_name" of relation "customers" contains null values`
		1. The column has `NOT NULL` constraint.
		2. When PostgreSQL tried to add the column, it received `NULL` - a violation of the `NOT NULL` constraint.
2. To address the issue:
	1. Add `contact_name` column without `NOT NULL` constraint.
	
	```sql
	ALTER TABLE customers
	ADD COLUMN contact_name VARCHAR (255);
	```
	
	2. Update the values in the `contact_name` column:
	
	```sql
	UPDATE customers
	SET contact_name = 'John Doe'
	WHERE id = 1;
	
	UPDATE customers
	SET contact_name = 'Mary Doe'
	WHERE id = 2;
	
	UPDATE customers
	SET contact_name = 'Lily Bush'
	WHERE id = 3;
	```
	
	3. Modify the `customer_name` column to add `NOT NULL` constraint:
	
	```sql
	ALTER TABLE customers
	ALTER COLUMN
	SET NOT NULL;
	```

### Summary ###

## PostgreSQL DROP COLUMN: Remove One or More Columns of a Table ##
1. Summary: Using `DROP COLUMN` clause in the `ALTER TABLE` statement to remove one or more columns from a table.

### Introduction to PostgreSQL DROP COLUMN clause ###
1. Use `DROP COLUMN` clause in `ALTER TABLE` statement:

```sql
ALTER TABLE table_name
DROP COLUMN column_name;
```

	1. PostgreSQL will automatically remove all **indexes** and **constraints** associated with the dropped column.
	2. If the column is used in other database objects such as **views**, **triggers**, and **stored procedures**, we cannot drop the column.
		1. Solution: Use `CASCADE` - drops the column and all its dependent objects
		
		```sql
		ALTER TABLE table_name
		DROP COLUMN column_name CASCADE;
		```
		
			1. To remove column only if it exists:
			
			```sql
			ALTER TABLE table_name
			DROP COLUMN IF EXISTS column_name;
			```
			
			2. To drop multiple columns:
			
			```sql
			ALTER TABLE table_name
			DROP COLUMN column_name1,
			DROP COLUMN column_name2,
			...;
			```
			
			3. PostgreSQL allows tables with no columns, but it is not according to standard SQL.

### PostgreSQL DROP COLUMN examples ###
1. Three tables: `books`, `categories`, `publishers`
	1. Each book has only one publisher.
	2. Each publisher can publish many books.
	3. Each book is assigned to a category and each category can have many books.
2. Statements:

```sql
CREATE TABLE publishers (
  publisher_id SERIAL PRIMARY KEY,
  name VARCHAR (255) NOT NULL
);

CREATE TABLE categories (
  category_id SERIAL PRIMARY KEY,
  name VARCHAR (255) NOT NULL
);

CREATE TABLE books (
  book_id SERIAL PRIMARY KEY,
  title VARCHAR (255) NOT NULL,
  isbn VARCHAR (255) NOT NULL,
  published_date DATE NOT NULL,
  description VARCHAR,
  category_id INT NOT NULL,
  publisher_id INT NOT NULL,
  FOREIGN KEY (publisher_id)
    REFERENCES publishers (publisher_id),
  FOREIGN KEY (category_id)
    REFERENCES categories (category_id)
);
```

3. Views:

```sql
CREATE VIEW book_info
AS SELECT
  book_id,
  title,
  isbn,
  published_date,
  name
FROM
  books b
INNER JOIN publishers
  USING (publisher_id)
ORDER BY title;
```

##### Difference between Views and Meterialized Views #####

In PostgreSQL, **views** and **materialized views** are both ways to save a query definition for later use, but they behave quite differently in how they store and refresh data.

Here’s a side-by-side comparison:

| Feature               | **View**                                                                                          | **Materialized View**                                                                      |
| --------------------- | ------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| **Storage**           | Stores only the SQL query, **no actual data** is stored.                                          | Stores the result set of the query **physically on disk**.                                 |
| **Data Freshness**    | Always returns **up-to-date** data because it runs the underlying query every time you access it. | Shows a **snapshot** of the data from the last refresh.                                    |
| **Performance**       | Slower for complex queries, since the query is executed each time you query the view.             | Faster for repeated access to complex queries, since results are precomputed.              |
| **Refresh Mechanism** | Not applicable — data is always fetched live.                                                     | Must be manually refreshed (`REFRESH MATERIALIZED VIEW ...`) to update the stored results. |
| **Indexes**           | You cannot directly index a view (you can index the underlying tables).                           | You can create indexes on a materialized view to speed up lookups.                         |
| **Use Case**          | When data must always be current, even if queries are slow.                                       | When you want **faster access** to expensive query results that don’t change often.        |

**Example:**

```sql
-- Create a normal view
CREATE VIEW active_users AS
SELECT * FROM users WHERE is_active = true;

-- Create a materialized view
CREATE MATERIALIZED VIEW active_users_mv AS
SELECT * FROM users WHERE is_active = true;
```

* Querying `active_users` will re-run the SELECT each time.
* Querying `active_users_mv` will use the precomputed results from when it was last refreshed:

```sql
REFRESH MATERIALIZED VIEW active_users_mv;
```

**Quick analogy:**

* **View** = a live TV broadcast — you always see the latest but it takes processing power to generate it.
* **Materialized View** = a recorded video — faster to play back, but outdated until you re-record it.

If you want, I can show you **how to keep a materialized view automatically updated in PostgreSQL** so it behaves more like a live view but with speed benefits.

#### Drop a column example ####
1. Dropping `category_id` column:

```sql
ALTER TABLE books
DROP COLUMN IF EXISTS category_id;
```

	1. View the structure: `\d books` 
		1. The statement removes `category_id` column and the foreign constraint associated with it.

#### Drop a column that is referenced by a constraint ####
1. Attempt to remove the `publisher_id` column from `books` table:

```sql
ALTER TABLE books
DROP COLUMN publisher_id;
```

	1. Error:
	
	```
	ERROR:  cannot drop table books column publisher_id because other objects depend on it
	DETAIL:  view book_info depends on table books column publisher_id
	HINT:  Use DROP ... CASCADE to drop the dependent objects too.
	```
	
	2. Solution: Use `CASCADE`
	
	```sql
	ALTER TABLE books
	DROP COLUMN publisher_id CASCADE;
	```
	
		1. The view `book_info` also gets removed.

#### Drop multiple columns example ####
1. Remove `isbn` and `description` columns.

```sql
ALTER TABLE books
  DROP COLUMN isbn,
  DROP COLUMN description;
```

	1. Describe: `\d books`

### Summary ###

## PostgreSQL Change Column Type ##
Summary: How to change the data type of a column by using `ALTER TABLE ... ALTER COLUMN`

### PostgreSQL change column type statement ###
1. Use `ALTER TABLE` statement:

```sql
ALTER TABLE table_name
ALTER COLUMN column_name
[SET DATA] TYPE new_data_type;
```

	1. First, specify name of the table in `ALTER TABLE` statement.
	2. Second, specify name of the column you want to change the date type after the `ALTER COLUMN` clause.
	3. Third, specify the new data type for the column after `TYPE` keyword
		1. `SET DATA TYPE` and `TYPE` are equivalent.
2. To change data types of multiple columns:

```sql
ALTER TABLE table_name
ALTER COLUMN column_name1 [SET DATA] TYPE new_data_type,
ALTER COLUMN column_name2 [SET DATA] TYPE new_data_type,
...;
```

3. We can convert the values of a column to the new ones while changing its data type with `USING`:

```sql
ALTER TABLE table_name
ALTER COLUMN column_name
[SET DATA] TYPE new_data_type USING expression;
```

	1. `expression`: To convert old values to new values.
		1. If `USING` is omitted, PostgreSQL will cast the value to new ones implicitly.
		2. `expression` with `USING` clause is recommended.
		3. It can be simple: `column_name::new_data_type` (`price::numeric`).
		4. It can be complex: A custom function.

### PostgreSQL change column type examples ###
#### Setting up a sample table ####
1. New table `assets` and insert rows into the table:

```sql
CREATE TABLE assets (
  id SERIAL PRIMARY KEY,
  name TEXT NOT NULL,
  asset_no VARCHAR NOT NULL,
  description TEXT,
  location TEXT,
  acquired_date DATE NOT NULL
);

INSERT INTO assets (name, asset_no, location, acquired_date)
VALUES ('Server', '10001', 'Server room', '2017-01-01'),
       ('UPS', '10002', 'Server room', '2017-01-01')
RETURNING *;
```

#### Changing one column example ####
1. Change the data type of the `name` column to `VARCHAR`:

```sql
ALTER TABLE assets
ALTER COLUMN name
SET DATA TYPE VARCHAR (255);
```

	1. Output: `ALTER TABLE`
		1. Indicates success.
		
#### Changing multiple columns example ####
1. Change data types of `description` and `location` columns from `TEXT` to `VARCHAR`:

```sql
ALTER TABLE assets
ALTER COLUMN description SET DATA TYPE VARCHAR (255),
ALTER COLUMN location SET DATA TYPE VARCHAR (255);
```

#### Changing a column from VARCHAR to INT example ####
1. Change `asset_no` column to `INT`

```sql
ALTER TABLE assets
ALTER COLUMN asset_no TYPE INT;
```

	1. Error with hint:
	
	```
	ERROR:  column "asset_no" cannot be cast automatically to type integer
	HINT:  You might need to specify "USING asset_no::integer".
	```
	
```sql
ALTER TABLE assets
ALTER COLUMN asset_no
SET DATA TYPE INT USING asset_no::integer;
```

### Summary ###

## PostgreSQL RENAME COLUMN: Renaming a Column ##
1. Summary: `RENAME COLUMN` clause in `ALTER TABLE` to rename one or more columns.

### Introduction to PostgreSQL RENAME COLUMN clause ###
1. Syntax:

```sql
ALTER TABLE table_name
RENAME COLUMN column_name TO new_column_name;
```

2. `COLUMN` is optional

```sql
ALTER TABLE table_name
RENAME column_name TO new_column_name;
```

3. PostgreSQL does not support `IF EXISTS` option for `RENAME` clause.
4. We need to execute `ALTER TABLE` multiple times to alter multiple columns.

```sql
ALTER TABLE table_name
RENAME column_name1 TO new_column_name1;

ALTER TABLE table_name
RENAME column_name2 TO new_column_name2;
```

5. If we rename a column referenced by other database objects (views, foreign key constraints, triggers, and stored procedures), PostgreSQL will automatically change the column name in the dependent objects.

### PostgreSQL RENAME COLUMN examples ###
#### Setting up sample tables ####
1. New tables: `customers` and `customer_groups`

```sql
CREATE TABLE customer_groups (
  id SERIAL PRIMARY KEY,
  name VARCHAR NOT NULL
);

CREATE TABLE customers (
  id SERIAL PRIMARY KEY,
  name VARCHAR NOT NULL,
  phone VARCHAR NOT NULL,
  email VARCHAR,
  group_id INT,
  FOREIGN KEY (group_id) REFERENCES customer_groups (id)
);
```

#### Renaming one column example ####
1. Rename `email` column of `customers` table to `contact_email`:

```sql
ALTER TABLE customers
RENAME COLUMN email TO contact_email;
```

2. New view named `customer_data` based on `customers` and `customer_groups`:

```
CREATE VIEW customer_data AS
SELECT 
  c.id,
  c.name,
  g.name customer_group
FROM
  customers c
  INNER JOIN customer_groups g
  ON g.id = c.group_id;
```

#### Renaming a column that has dependent objects example ####
1. Change `name` column of `customer_groups` table to `group_name`:

```sql
ALTER TABLE customer_groups
RENAME COLUMN name TO group_name;
```

	1. `name` is used in `customer_data` view
		1. Check whether change in `name` column was cascaded to the `customer_data` view:
		
		```psql
		\d+ customer_data
		```

	2. Output:
	
	```
	postgres=# \d+ customer_data
                                 View "public.customer_data"
    Column     |       Type        | Collation | Nullable | De
	fault | Storage  | Description
	----------------+-------------------+-----------+----------+---
	------+----------+-------------
	 id             | integer           |           |          |
		  | plain    |
	 name           | character varying |           |          |
		  | extended |
	 customer_group | character varying |           |          |
		  | extended |
	View definition:
	 SELECT c.id,
		c.name,
		g.group_name AS customer_group
	   FROM customers c
		 JOIN customer_groups g ON g.id = c.group_id;
	```

#### Using multiple RENAME COLUMN statements to rename multiple columns example ####
1. Statements to rename two columns `name` and `phone` of `customers` table to `customer_name` and `contact_phone`:

```
ALTER TABLE customers
RENAME COLUMN name TO customer_name;

ALTER TABLE customers
RENAME COLUMN phone TO contact_phone;
```

### Summary ###

## PostgreSQL DROP TABLE ##
1. Summary: `DROP TABLE` statement to remove one or more tables from the database

### Introduction to PostgreSQL DROP TABLE statement ###
1. Use `DROP TABLE` statement as follows:

```sql
DROP TABLE [IF EXISTS] table_name
[CASCADE | RESTRICT];
```

	1. `IF EXISTS` to remove the table only if it exists.
		1. Otherwise, if the table does not exist, PostgreSQL throws an error.
	2. If the table is used in other database objects (views, triggers, functions, and stored procedures), you cannot remove it.
		1. Solution:
			1. `CASCADE`: Removes the table and its dependent objects
			2. `RESTRICT` **(M)**: Rejects the removal if there is any object depending on the table.
				1. It is the default option if you don't specify anything.
2. To remove multiple tables simultaneously, place tables separated by commas after `DROP TABLE` keywords:

```sql
DROP TABLE [IF EXISTS]
  table_name1,
  table_name2,
  ...
[CASCADE | RESTRICT];
```

	1. Roles required (any):
		1. Superuser (`postgres`)
		2. Schema owner
		3. Table owner

### PostgreSQL DROP TABLE examples ###
#### Drop a table that does not exist ####
1. Remove table `author` in the database:

```sql
DROP TABLE author;
```

2. Safe remove:

```sql
DROP TABLE IF EXISTS author;
```

#### Drop a table that has dependent objects ####
1. New tables: `authors` and `pages`. The `pages` table has a foreign key that references the `authors` table.

```sql
CREATE TABLE authors (
  author_id INT PRIMARY KEY,
  firstname VARCHAR (50) NOT NULL,
  lastname VARCHAR (50) NOT NULL
);

CREATE TABLE pages (
  page_id SERIAL PRIMARY KEY,
  title VARCHAR (255) NOT NULL,
  contents TEXT,
  author_id INT NOT NULL,
  FOREIGN KEY (author_id) REFERENCES authors (author_id)
);
```

2. Drop the `authors` table:

```sql
DROP TABLE IF EXISTS authors;
```

	1. Error:
	
	```
	ERROR:  cannot drop table authors because other objects depend on it
	DETAIL:  constraint pages_author_id_fkey on table pages depends on table authors
	HINT:  Use DROP ... CASCADE to drop the dependent objects too.
	```
	
		1. Solution: Remove dependent objects first before dropping the `author` table or use `CASCADE` option:
		
		```sql
		DROP TABLE IF EXISTS authors CASCADE;
		```
		
			1. It deletes `authors` table and the constraint in the `pages` table.
				1. It will just issue a notice:
				
				```
				NOTICE:  drop cascades to constraint pages_author_id_fkey on table pages
				DROP TABLE
				```

#### Drop multiple tables ####
1. Two tables:

```sql
CREATE TABLE tvshows (
  tvshow_id INT GENERATED ALWAYS AS IDENTITY,
  title VARCHAR,
  release_year SMALLINT,
  PRIMARY KEY (tvshow_id)
);

CREATE TABLE animes (
  anime_id INT GENERATED ALWAYS AS IDENTITY,
  title VARCHAR,
  release_year SMALLINT,
  PRIMARY KEY (anime_id)
);
```

2. Drop both tables using single `DROP TABLE` statement to drop `tvshows` and `animes` tables.

```sql
DROP TABLE tvshows, animes;
```

#### Summary ####
1. `DROP TABLE`: To drop one or more tables.
2. `CASCADE`: To drop a table and all of its dependent objects.

## PostgreSQL TRUNCATE TABLE ##
1. Summary: `TRUNCATE TABLE` - to delete all data from large tables.

### Introduction to PostgreSQL TRUNCATE TABLE statement ###
1. `DELETE` statement is not efficient if table has numerous data.
	1. Alternative: `TRUNCATE TABLE`
		1. It deletes data from a table very fast.
		
		```sql
		TRUNCATE TABLE table_name;
		```

#### Remove all data from multiple tables ####
1. Separate table names with `,`.

```sql
TRUNCATE TABLE
  table_name1,
  table_name2,
  ...;
```

#### Remove all data from a table that has foreign key references ####
1. If a table we want to delete has foreign key references from other tables.
	1. `TRUNCATE TABLe` doesn't delete a table that has foreign key references by default.
		1. Solution: `CASCADE`
		
		```sql
		TRUNCATE TABLE table_name CASCADE;
		```

### PostgreSQL TRUNCATE TABLE statement examples ###
#### Basic PostgreSQL TRUNCATE TABLE statement example ####
1. New table: `products`:

```sql
CREATE TABLE products (
  id SERIAL PRIMARY KEY,
  name VARCHAR (255) NOT NULL,
  price DECIMAL (10, 2) NOT NULL DEFAULT 0
);
```

2. Insert some rows:

```sql
INSERT INTO products (name, price)
VALUES
  ('A', 19.99),
  ('B', 29.99),
  ('C', 39.99),
  ('D', 49.99)
RETURNING *;
```

3. Delete all data from `products` table using `TRUNCATE TABLE`:

```sql
TRUNCATE TABLE products;
```

#### Using PostgreSQL TRUNCATE TABLE statement to delete all data from multiple tables ####
1. New table: `customers`

```sql
CREATE TABLE customers (
  id SERIAL PRIMARY KEY,
  name VARCHAR (255) NOT NULL,
  phone VARCHAR (255) NOT NULL
);

INSERT INTO customers (name, phone)
VALUES
  ('John Doe', '123-456-7890'),
  ('Jane Smith', '987-654-3210'),
  ('Robert Johnson', '555-123-4567'),
RETURNING *;
```

2. New table: `vendors`

```sql
CREATE TABLE vendors (
  id SERIAL PRIMARY KEY,
  name VARCHAR (255) NOT NULL,
  phone VARCHAR (255) NOT NULL
);

INSERT INTO vendors (name, phone)
VALUES
  ('ABC Electronics', '555-123-4567'),
  ('XYZ Supplies', '999-888-7777'),
  ('Tech Solutions Inc.', '111-222-3333')
RETURNING *;
```

3. Delete data from `customers` and `vendors` tables:

```sql
TRUNCATE TABLE customers, vendors;
```

#### Using PostgreSQL TRUNCATE TABLE statement to delete data from a table referenced by a foreign key ####
1. Creation of `orders` and `order_details`:

```sql
CREATE TABLE orders(
  order_id SERIAL PRIMARY KEY,
  customer_name VARCHAR(255) NOT NULL,
  ordered_date DATE NOT NULL,
  status VARCHAR(20) NOT NULL
);
CREATE TABLE order_items (
  order_id INT NOT NULL,
  item_id INT NOT NULL,
  product_name VARCHAR(255) NOT NULL,
  quantity INT NOT NULL,
  FOREIGN KEY (order_id)
     REFERENCES orders(order_id) ON DELETE CASCADE ON UPDATE CASCADE,
  PRIMARY KEY (order_id, item_id)
);
INSERT INTO orders (customer_name, ordered_date, status)
VALUES
  ('John Doe', '2024-01-25', 'Processing'),
  ('Jane Smith', '2024-01-26', 'Shipped'),
  ('Bob Johnson', '2024-01-27', 'Delivered');
INSERT INTO order_items (order_id, item_id, product_name, quantity)
VALUES
  (1, 1, 'A', 2),
  (1, 2, 'B', 1),
  (2, 1, 'C', 3),
  (3, 1, 'D', 5),
  (3, 2, 'E', 2);
```

2. Attempt to truncate data from `orders` table:

```sql
TRUNCATE TABLE orders;
```

```
DETAIL:  Table "order_items" references "orders".
HINT:  Truncate table "order_items" at the same time, or use TRUNCATE ... CASCADE.
```

	1. `orders` table is referenced by `order_items` table.
		1. Solution: Use `CASCADE`
		
		```sql
		TRUNCATE TABLE orders CASCADE;
		```
		
		```
		NOTICE:  truncate cascades to table "order_items"
		TRUNCATE TABLE
		```

### Restarting sequence ###
1. To reset values of identity column, besides removing data:

```sql
TRUNCATE TABLE table_name
RESTART IDENTITY;
```

2. Example:

```sql
TRUNCATE TABLE products
RESTART IDENTITY;
```

	1. `CONTINUE IDENTITY` is the default option of `TRUNCATE TABLE`
		1. It does not restart the value in sequence associated with the column in a table.

### TRUNCATE TABLE statement and ON DELETE trigger ###
1. `TRUNCATE TABLE` does not fire any `ON DELETE` triggers associated with the table.
	1. Solution: Define `BEFORE TRUNCATE` and `AFTER TRUNCATE` triggers for the table.

### TRUNCATE TABLE statement and transactions ###
1. `TRUNCATE TABLE` is transaction-safe:
	1. It can be placed within a transaction.

### Why TRUNCATE TABLE statement is more efficient than the DELETE statement ###
1. Main reasons:
	1. **Minimal logging**: `TRUNCATE TABLE` doesn't generate individual row deletion logs
		1. It deallocates entire data pages (making it faster than the `DELETE` statement).
	2. **Fewer resources**: Truncate is more lightweight than delete option becuase it doesn't generate as much undo and redo information.
		1. It releases storage space without scanning individual rows.
	3. **Lower-level locking mechanism**: Truncate operation requires lower-level locks and is less prone to conflicts with other transactions
		1. Improves overall system concurrency.

### Why is TRUNCATE more efficient than DELETE in PostgreSQL? ###
Great question 👍

In PostgreSQL (and in most RDBMSs), `TRUNCATE` is much more efficient than `DELETE` because of **how they work internally**:

---

### 1. **Row-by-row vs. Bulk Operation**

* **`DELETE`**:

  * Works row by row.
  * For each row deleted:

    * It writes a record into the **WAL (Write-Ahead Log)** so the deletion can be rolled back or replicated.
    * It maintains indexes by removing corresponding index entries.
    * It checks row-level constraints, triggers, and foreign key references.
  * This makes `DELETE` slower for large tables.

* **`TRUNCATE`**:

  * Does not scan the table row by row.
  * Instead, it just **deallocates the data pages** that belong to the table.
  * The table is reset to an empty state almost instantly, regardless of its size.
  * WAL records are minimal (just enough to record that the table was truncated).
  * Indexes are also reset instead of being updated row by row.

---

### 2. **MVCC (Multi-Version Concurrency Control)**

* PostgreSQL uses MVCC, so when you `DELETE` rows, the rows aren’t physically removed immediately.

  * Instead, they’re marked as **dead tuples**.
  * Actual space is reclaimed later via `VACUUM`.
* With `TRUNCATE`, PostgreSQL bypasses MVCC cleanup because it just drops all table pages at once.

---

### 3. **Foreign Keys and Triggers**

* `DELETE` fires **row-level triggers** (e.g., `ON DELETE` triggers) and checks referential integrity for each row.
* `TRUNCATE` skips row-level triggers, but it:

  * Will fail if there are foreign key constraints (unless you use `CASCADE`).
  * Fires **statement-level triggers** only.

---

### 4. **Locks**

* `DELETE` acquires a row-level lock per row.
* `TRUNCATE` acquires an **Access Exclusive Lock** on the whole table (blocks reads/writes while truncating).
  This is acceptable because it’s usually used for bulk cleanup.

---

✅ **Summary**:

* Use `DELETE` when you need fine-grained row removals, triggers, or foreign key enforcement.
* Use `TRUNCATE` when you want to quickly remove all rows, reclaim space, and you don’t need per-row operations.

---

Would you like me to also show you an **example with timing** (`DELETE` vs `TRUNCATE` on a million-row table) so you can see the performance difference in action?

### Summary ###
1. Use `TRUNCATE TABLE` to delete all data from a large table very fast.
2. Use `CASCADE` option to truncate a table that is referenced by foreign key constraints.
3. The `TRUNCATE TABLE` deletes data but does not fire `ON DELETE` triggers.
	1. It fires the following triggers:
		1. `BEFORE TRUNCATE`
		2. `AFTER TRUNCATE`
4. `TRUNCATE TABLE` is transaction-safe.

## PostgreSQL Temporary Table ##
1. Summary: PostgreSQL temporary table and how to manage it effectively.

### Introduction to the PostgreSQL temporary tables ###
1. A temporary table is a table that exists only during a database session.
	1. It is created and used within a single database session and is automatically dropped at the end of the session.

#### Constructing a temporary table ####
1. `CREATE TEMPORARY TABLE` **(M)**

```sql
CREATE TEMPORARY TABLE table_name (
  column1 datatype (size) constraint,
  column2 datatype (size) constraint,
  ...,
  table_constraints
);
```

2. `TEMP` and `TEMPORARY` are interchangeable.

```sql
CREATE TEMP TABLE table_name (
  ...
);
```

3. Example:

```sql
CREATE TEMP TABLE my_temp (
  id INT
);

INSERT INTO my_temp (id)
VALUES
  (1),
  (2),
  (3)
RETURNING *;
```

	1. If you open a second database session and query data from `my_temp` table, you'll get an error.
	
	```sql
	SELECT * FROM my_temp;
	```
	
	```
	ERROR:  relation "mytemp" does not exist
	LINE 1: SELECT * FROM mytemp;
	```
	
	2. If you terminate the current database session and attempt to query data from `my_temp` table, you'll encounter an error.
		1. The temporary table gets dropped when the session that created it ended.

#### PostgreSQL temporary table names ####
1. If a temporary table has the same name as an existing permanent table, you cannot access the permanent table until the temporary table is dropped.
2. Temporary tables are created in a special schema
	1. We cannot specify a schema for temporary tables.
3. List tables: `\dt+` **(M)**
	1. It shows the temporary table instead of the permanent table.
		1. `pg_temp_3` (say) is the schema of `customers` temporary table.
4. Access to permanent table requires qualifying the table name with schema name.

```sql
SELECT * FROM public.customers;
```

#### Removing a PostgreSQL temporary table ####
1. Use `DROP TABLE` statement:

```sql
DROP TABLE temp_table_name;
```

	1. There is no special keyword.
2. `DROP TABLE customers` - drops temporary table

### When to use temporary tables ###
1. **Isolation of data**: Temporary tables are session specific.
	1. Different sessions or transactions can use the same table name for temporary tables without causing a conflict.
	2. Helps in isolating data for a specific task or session.
2. **Intermediate storage**: Temporary tables can store intermediate results of a complex query.
	1. We can break down a complex query into multiple simple ones and use temporary tables as the intermediate storage for storing the partial results.
3. **Transaction scope**: Temporary tables can be useful to store intermediate results within a transaction.
	1. A temporary table will only be visible within the transaction.

### Summary ###
1. Temporary table is a short-lived table that exists during a database session or a transaction.
2. Use `CREATE TEMP TABLE` for creation of temporary table.
3. Use `DROP TABLE` to drop a temporary table.

## PostgreSQL Copy Table: A Step-by-Step Guide with Practical Examples ##
1. Summary: How to copy an existing table including table structure and data using copy table statement.

### Introduction to PostgreSQL copy table statement ###
1. To copy a table completely (table structure and data), use the following statement:

```sql
CREATE TABLE new_table AS
TABLE existing_table;
```

2. To copy table structure only without data:

```sql
CREATE TABLE new_table AS
TABLE existing_tabe
WITH NO DATA;
```

3. To copy table with partial data from an existing table:

```sql
CREATE TABLE new_table AS
SELECT
  *
FROM
  existing_table
WHERE
  condition;
```

	1. `WHERE` clause defines which rows of the existing table must be copied.
	2. The statements only copy table structure and data but not the indexes and constraints.

### PostgreSQL copy table example ###
1. New table: `contacts`

```sql
CREATE TABLE contacts (
  id SERIAL PRIMARY KEY,
  first_name VARCHAR NOT NULL,
  last_name VARCHAR NOT NULL,
  email VARCHAR NOT NULL UNIQUE
);
```

	1. There are two constraints: `PRIMARY KEY`, and `UNIQUE`
2. Insert rows:

```sql
INSERT INTO contacts (first_name, last_name, email)
VALUES
  ('John', 'Doe', 'john.doe@example.com'),
  ('David', 'William', 'david.william@example.com')
RETURNING *;
```

3. Make a copy of `contacts`:

```sql
CREATE TABLE contact_backup
AS TABLE contacts;
```

	1. Verify the data of `contact_backup` table.
	
	```sql
	SELECT * FROM contact_backup;
	```
	
4. Examine the structure of `contact_backup`:

```psql
\d contact_backup;
```

	1. The structure is same as `contacts` table except the indexes and other constraints.
		1. Solution: Add the constraints
		
		```sql
		ALTER TABLE contact_backup
		ADD SERIAL PRIMARY KEY (id);
		
		ALTER TABLE contact_backup
		ADD UNIQUE (email);
		```
		
	2. View the structure:
	
	```psql
	\d contact_backup
	```

### Summary ###

## PostgreSQL Primary Key ##
1. Summary: Primary key and how to manage primary key constraints effectively.

### Introduction to PostgreSQL primary key ###
1. Primary key: It is a column or a group of columns used to uniquely identify a row in a table.
	1. A column that participates in a primary key is known as a primary key column.
2. A table can have zero or one primary key. (not more than one)
3. It is a good practice to add a primary key to every table.
4. When a primary key is added, PostgreSQL constructs a unique B-tree index on the column or a group of columns used for the primary key.
5. Primary key constraint:
	1. Non-Null constraint + Unique constraint
6. A primary is defined usually when defining a table:

```sql 
CREATE TABLE table_name (
  column_1 data_type PRIMARY KEY,
  column_2 data_type,
  ...
);
```

	1. Only one column is the primary key.
7. If primary key consists of multiple columns:

```sql
CREATE TABLE table_name (
  column_1 data_type,
  column_2 data_type,
  column_3 data_type,
  ...
  PRIMARY KEY (column_1, column_2, ...)
);
```

8. To add a primary key to existing table:

```sql
ALTER TABLE table_name
ADD PRIMARY KEY (column_1, column_2, ...);
```

	1. If we don't explicitly specify a name for the primary key constraint, PostgreSQL will assign a default name to the primary key constraint.
		1. Name: `table-name_pkey`
9. To assign a name to a constraint: Use `CONSTRAINT`

```sql
CONSTRAINT constraint_name PRIMARY KEY (column_1, column_2, ...);
```

### PostgreSQL primary key examples ###
#### Constructing a table with a primary key that consists of one column ####
1. Primary key of one column:

```sql
CREATE TABLE orders (
  order_id SERIAL PRIMARY KEY,
  customer_id VARCHAR (255) NOT NULL,
  order_date DATE NOT NULL
);
```

	1. Ensures that the value in `order_id` is unique for every row in the table.

#### Constructing a table with a primary key that consists of two columns ####
1. Primary key consists of `order_id` and `item_no`:

```sql
CREATE TABLE order_items (
  order_id INT,
  item_no SERIAL,
  item_description VARCHAR NOT NULL,
  quantity INTEGER NOT NULL,
  price DEC (10, 2),
  PRIMARY KEY (order_id, item_no)
);
```

#### Adding a primary key to an existing table ####
1. Adding a primary key constraint:

```sql
CREATE TABLE products (
  product_id INT,
  name VARCHAR (255) NOT NULL,
  description TEXT,
  price DEC (10, 2) NOT NULL
);

ALTER TABLE products
ADD PRIMARY KEY (product_id);
```

#### Adding an auto-incremented primary key to an existing table ####
1. New table: `vendors` that does not have a primary key

```sql
CREATE TABLE vendors (
  name VARCHAR (255)
);
```

2. Insert rows:

```sql
INSERT INTO vendors (name)
VALUES
  ('Microsoft'),
  ('IBM'),
  ('Apple'),
  ('Samsung')
RETURNING *;
```

3. Add a primary key `vendor_id` into `vendors` table with the type `SERIAL`

```sql
ALTER TABLE vendors
ADD COLUMN vendor_id SERIAL PRIMARY KEY;
```

4. Verify:

```sql
SELECT
  vendor_id,
  name
FROM
  vendors;
```

### Drop a primary key ###
1. Remove a primary key from a table:

```sql
ALTER TABLE table_name
DROP CONSTRAINT primary_key_constraint;
```

	1. `primary_key_constraint`: The name of the constraint to drop
2. Display the table structure: `\d vendors`
3. Drop the constraint:

```sql
ALTER TABLE vendors
DROP CONSTRAINT vendors_pkey;
```

	1. It only removes constraint and not the column itself.

### Summary ###
1. `PRIMARY KEY` - to define a primary key.
2. `ALTER TABLE ... ADD PRIMARY KEY` - add a primary key to a table.
3. `ALTER TABLE ... DROP CONSTRAINT` - drop a primary key from a table.

## PostgreSQL Foreign Key ##
1. Summary: How to add foreign keys to tables using foreign key constraints.

### Introduction to PostgreSQL Foreign Key Constraint ###
1. Foreign key: a column or group of columns in a table that uniquely identifies a row in another table.
	1. It establishes a link between the data in two tables by referencing the primary key or a **unique constraint** of the referenced table.
	2. The table containing the foreign key is referred to as referencing table or child table.
	3. The table referenced by a foreign key is known as the referenced table or parent table.
	4. The main purpose of foreign keys is to maintain referential integrity in a relational database
		1. It ensures that the relationships between the parent and child tables are valid.
			1. Foreign key prevents insertion of values that do not have corresponding values in the referenced table.
			2. Foreign key maintains consistency by automatically updating or deleting related rows in the child table when changes occur in the parent table.
	5. A table can have multiple foreign keys depending on its relationships with other tables.
	6. Use foreign key constraint to define a foreign key in a table.

### PostgreSQL foreign key constraint syntax ###
1. Syntax:

```sql
[CONSTRAINT fk_name]
  FOREIGN KEY (fk_columns)
  REFERENCES parent_table (parent_key_columns)
  [ON DELETE delete_action]
  [ON UPDATE update_action]
```

	1. Specify the foreign key constraint after the `CONSTRAINT` keyword.
		1. `CONSTRAINT` clause is optional
			1. If you omit it, PostgreSQL will assign an auto-generated name
	2. Specify one or more foreign key columns in parantheses after the `FOREIGN KEY` keywords
	3. Specify parent table and parent key columns referenced by the foreign key columns in `REFERENCES` clause
	4. Specify `DELETE` and `UPDATE` actions (`ON DELETE` and `ON UPDATE`)
		1. They determine the behaviors when the primary key in the parent table is deleted or updated
			1. Update action is infrequently used
2. PostgreSQL supports the following actions for `ON DELETE`:
	1. `SET NULL`
	2. `SET DEFAULT`
	3. `RESTRICT`
	4. `NO ACTION`
	5. `CASCADE`

### PostgreSQL foreign key constraint examples ###
1. Example: `customers` and `contacts` tables:

```sql
DROP TABLE IF EXISTS customers;
DROP TABLE IF EXISTS contacts;

CREATE TABLE customers (
  customer_id INT GENERATED ALWAYS AS IDENTITY,
  customer_name VARCHAR (255) NOT NULL,
  PRIMARY KEY (customer_id)
);

CREATE TABLE contacts (
  contact_id INT GENERATED ALWAYS AS IDENTITY,
  customer_id INT,
  contact_name VARCHAR (255) NOT NULL,
  phone VARCHAR (255),
  email VARCHAR (255),
  PRIMARY KEY (contact_id),
  CONSTRAINT fk_customer
    FOREIGN KEY (customer_id)
	  REFERENCES customers (customer_id)
);
```

	1. Each customer has zero or more contacts
	2. Each contact belongs to zero or one customer
	3. `fk_customer` in `contacts` defines `customer_id` as the foreign key
	4. Since `ON DELETE` and `ON UPDATE` are not defined, the default action is `NO ACTION`

### NO ACTION ###
1. Insert data:

```sql
INSERT INTO customers (customer_name)
VALUES ('BlueBird Inc'),
       ('Dolphin LLC');
	   
INSERT INTO contacts (customer_id, contact_name, phone, email)
VALUES
       (1, 'John Doe', '(408)-111-1234', 'john.doe@example.com'),
	   (1,'Jane Doe','(408)-111-1235','jane.doe@example.com'),
	   (2,'David Wright','(408)-222-1234','david.wright@example.com');
```

2. To delete a row with customer id 1:

```sql
DELETE FROM customers
WHERE customer_id = 1;
```

	1. Error:
	
	```
	ERROR:  update or delete on table "customers" violates foreign key constraint "fk_customer" on table "contacts"
	DETAIL:  Key (customer_id)=(1) is still referenced from table "contacts".
	SQL state: 23503
	```
	
		1. `NO ACTION` is assumed.
		2. `RESTRICT` is similar to `NO ACTION`
			1. Difference: If we define foreign key constraint as `DEFERRABLE` with `INITIALLY DEFERRED` or `INITIALLY IMMEDIATE` mode

### SET NULL ###
1. `SET NULL` automatically sets `NULL` to the foreign key columns in the referencing rows of child table when referenced rows in the parent table are deleted
2. Re-instantiate the tables with foreign key that uses `SET NULL` action in the `ON DELETE` clause:

```sql
DROP TABLE IF EXISTS contacts;
DROP TABLE IF EXISTS customers;

CREATE TABLE customers (
  customer_id INT GENERATED ALWAYS AS IDENTITY,
  customer_name VARCHAR (255) NOT NULL,
  PRIMARY KEY (customer_id)
);

CREATE TABLE contacts (
  contact_id INT GENERATED ALWAYS AS IDENTITY,
  customer_id INT,
  contact_name VARCHAR (255) NOT NULL,
  phone VARCHAR (15),
  email VARCHAR (100),
  PRIMARY KEY (contact_id),
  CONSTRAINT fk_customer
    FOREIGN KEY (customer_id)
	REFERENCES customers (customer_id)
	ON DELETE SET NULL
);
```

3. Insert data into `customers` and `contacts` tables:

```sql
INSERT INTO customers (customer_name)
VALUES
  ('BlueBird Inc'),
  ('Dolphin LLC');
  
INSERT INTO contacts (customer_id, contact_name, phone, email)
VALUES
  (1, 'John Doe', '(408)-111-1234', 'john.doe@example.com'),
  (1, 'Jane Doe', '(408)-111-1235', 'john.doe@example.com'),
  (2, 'David Wright', '(408)-222-1234', 'david.wright@example.com');
```

4. Delete customer with id 1:

```sql
DELETE FROM customers
WHERE customer_id = 1;
```

	1. Because of `ON DELETE SET NULL`, referencing rows in `contacts` table are set to `NULL`
5. Display data in `contacts` table:

```sql
SELECT * FROM contacts;
```

	1. `customer_id` changed to `NULL` in `contacts` table.

### CASCADE ###
1. `ON DELETE CASCADE` - automatically deletes all the referencing rows in the child table when the referenced rows in the parent table are deleted.
	1. It is a commonly used option.
	
```sql
DROP TABLE IF EXISTS contacts;
DROP TABLE IF EXISTS customers;

CREATE TABLE customers (
  customer_id INT GENERATED ALWAYS AS IDENTITY,
  customer_name VARCHAR (255) NOT NULL,
  PRIMARY KEY (customer_id)
);

CREATE TABLE contacts (
  contact_id INT GENERATED ALWAYS AS IDENTITY,
  customer_id INT,
  contact_name VARCHAR (255) NOT NULL,
  phone VARCHAR (15),
  email VARCHAR (100),
  PRIMARY KEY (contact_id),
  CONSTRAINT fk_customer
    FOREIGN KEY (customer_id)
	REFERENCES customers (customer_id)
	ON DELETE CASCADE
);


INSERT INTO customers(customer_name)
VALUES
  ('BlueBird Inc'),
  ('Dolphin LLC');
INSERT INTO contacts(customer_id, contact_name, phone, email)
VALUES
  (1,'John Doe','(408)-111-1234','john.doe@example.com'),
  (1,'Jane Doe','(408)-111-1235','jane.doe@example.com'),
  (2,'David Wright','(408)-222-1234','david.wright@example.com');
```

2. Delete customers with `customer_id` 1:

```sql
DELETE FROM customers
WHERE customer_id = 1;
```

	1. All the referencing rows in `contacts` table are automatically deleted
		1. `SELECT * FROM contacts;`

### SET DEFAULT ###
1. `ON DELETE SET DEFAULT` - sets default value to foreign key column of referencing rows in child table when referenced rows in parent table are deleted.

### Add a foreign key constraint to an existing table ###
1. `ALTER TABLE` can be used to add a foreign key constraint to an existing table:

```sql
ALTER TABLE child_table
ADD CONSTRAINT constraint_name
FOREIGN KEY (fk_column)
REFERENCES parent_table (parent_key_columns);
```

2. To add foreign key constraint with `ON DELETE CASCADE` option to an existing table:
	1. Drop existing foreign key constraint:

	```sql
	ALTER TABLE child_table
	DROP CONSTRAINT constraint_fkey;
	```
	
	2. Add new foreign key constraint with `ON DELETE CASCADE` action:
	
	```sql
	ALTER TABLE child_table
	ADD CONSTRAINT constraint_fk
	FOREIGN KEY (fk_columns)
	REFERENCES parent_table (parent_key_columns)
	ON DELETE CASCADE;
	```

### Summary ###
1. Use foreign keys to ensure referential integrity and consistency of data between two tables.
2. Use `FOREIGN KEY` constraint to define a foreign key constraint when defining a table.
3. Use `ALTER TABLE ... ADD CONSTRAINT ... FOREIGN KEY` to add a foreign key constraint to an existing table.

## PostgreSQL DELETE Cascade ##
1. Summary: `DELETE CASCADE` to delete related rows in child tables when a parent row is deleted from the parent table.

### Introduction to the PostgreSQL DELETE CASCADE ###
1. `DELETE CASCADE` is a referential action to automatically delete rows in child tables when a parent row is deleted from the parent table.
2. The feature helps us maintain referential integrity in the database by ensuring that dependent rows are removed when their corresponding rows are deleted.
3. To enable `DELETE CASCADE` we need two tables: `parent_table` and `child_table`:

```sql
CREATE TABLE parent_table (
  id SERIAL PRIMARY KEY,
  ...
);

CREATE TABLE child_table (
  id SERIAL PRIMARY KEY,
  parent_id INT,
  FOREIGN KEY (parent_id)
    REFERENCES parent_table (id)
	ON DELETE CASCADE
);
```

	1. `parent_id` is a foreign key that references the `id` column of the `parent_table`
	2. `ON DELETE CASCADE` is the action on foreign key that automatically deletes the rows from the `child_table` when the corresponding rows from the `parent_table` are deleted.

### PostgreSQL DELETE CASCADE example ###
1. New tables:

```sql
CREATE TABLE departments (
  id SERIAL PRIMARY KEY,
  name VARCHAR (100) NOT NULL
);

CREATE TABLE employees (
  id SERIAL PRIMARY KEY,
  name VARCHAR (100) NOT NULL,
  department_id INT NOT NULL,
  FOREIGN KEY (department_id)
    REFERENCES departments (id)
	ON DELETE CASCADE
);
```

	1. Each department may have one or more employees and each employee belongs to a department.

### Summary ###

## PostgreSQL CHECK Constraints ##
1. Summary: `CHECK` constraints and how to use them to constrain values in columns of a table based on a boolean expression.

### Introduction to PostgreSQL CHECK constraints ###
1. `CHECK` constraint ensures that values in a column or a group of columns meet a specific condition.
	1. Allows us to enforce data integrity rules at the database level.
	2. It uses a boolean expression to evaluate the values, ensuring that only valid data is inserted or updated in a table.

#### Defining CHECK constraints ####
1. Adding `CHECK` constraint when defining a table:

```sql
CREATE TABLE table_name (
  column1 datatype,
  ...,
  CONSTRAINT constraint_name CHECK (condition)
);
```

	1. `constraint_name` - constraint name
		1. It is optional.
			1. If ommitted, PostgreSQL will automatically generate a name for the `CHECK` constraint.
	2. `condition` - a condition to be satisfied for the constraint to be valid.
2. If a `CHECK` constraint involves only one column, we can define it as a column constraint.
3. Default name format:

```
{table}_{column}_check
```

#### Adding CHECK constraints to tables ####
1. Adding `CHECK` constraint to existing tables:

```sql
ALTER TABLE table_name
ADD CONSTRAINT constraint_name CHECK (condition);
```

#### Removing CHECK constraints ####
1. To drop `CHECK` constraint:

```sql
ALTER TABLE table_name
DROP CONSTRAINT constraint_name;
```

### PostgreSQL CHECK constraint examples ###
#### Defining PostgreSQL CHECK constraint for a new table ####
1. New table `employees`:

```sql
CREATE TABLE employees (
  id SERIAL PRIMARY KEY,
  first_name VARCHAR (50) NOT NULL,
  last_name VARCHAR (50) NOT NULL,
  birth_date DATE NOT NULL,
  joined_date DATE NOT NULL,
  salary NUMERIC CHECK (salary > 0)
);
```

	1. `salary` must be > 0
2. Try to insert a row with `salary` < 0:

```sql
INSERT INTO employees (first_name, last_name, birth_date, joined_date, salary)
VALUES ('John', 'Doe', '1972-01-01', '2015-07-01', -100000);
```

```
ERROR:  new row for relation "employees" violates check constraint "employees_salary_check"
Failing row contains (1, John, Doe, 1972-01-01, 2015-07-01, -100000). 

SQL state: 23514
Detail: Failing row contains (1, John, Doe, 1972-01-01, 2015-07-01, -100000).
```

#### Adding PostgreSQL CHECK constraints for existing tables ####
1. `ALTER TABLE ... ADD CONSTRAINT`

```sql
ALTER TABLE employees
ADD CONSTRAINT joined_date_check
CHECK ( joined_date > birth_date );
```

2. Attempt to insert a new row:

```
INSERT INTO employees (first_name, last_name, birth_date, joined_date, salary)
VALUES ('John', 'Doe', '1990-01-01', '1989-01-01', 100000);
```

```
ERROR:  new row for relation "employees" violates check constraint "joined_date_check"
Failing row contains (2, John, Doe, 1990-01-01, 1989-01-01, 100000). 

SQL state: 23514
Detail: Failing row contains (2, John, Doe, 1990-01-01, 1989-01-01, 100000).
```

#### Using functions in CHECK constraints ####
1. `CHECK` constraint to ensure that first name has at least 3 characters:

```sql
ALTER TABLE employees
ADD CONSTRAINT first_name_check
CHECK ( LENGTH(TRIM(first_name)) >= 3 );
```

	1. `TRIM()` removes leading and trailing whitespaces from the `first_name`.
	2. `LENGTH()` returns character length of the result of `TRIM()` function.
2. Try to insert a row with first name having only 2 characters:

```sql
INSERT INTO employees (first_name, last_name, birth_date, joined_date, salary)
VALUES ('Ab', 'Doe', '1990-01-01', '2008-01-01', 100000);
```

```
ERROR:  new row for relation "employees" violates check constraint "first_name_check"
Failing row contains (3, Ab, Doe, 1990-01-01, 2008-01-01, 100000). 

SQL state: 23514
Detail: Failing row contains (3, Ab, Doe, 1990-01-01, 2008-01-01, 100000).
```

#### Removing a CHECK constraint example ####
1. Remove `CHECK` constraint:

```sql
ALTER TABLE employees
DROP CONSTRAINT joined_date_check;
```

### Summary ###

## PostgreSQL UNIQUE Constraint ##
1. Summary: `UNIQUE` constraint makes sure that values stored in a column or a group of columns are unique across rows in a table.

### Introduction to PostgreSQL UNIQUE constraint ###
1. Example: email addresses, usernames, ...
2. When `UNIQUE` constraint is in place, everytime we insert a new row, it checks if the value is already in the table
	1. It rejects the change an issues an error if the value already exists.
	2. Same for updating data.
3. A unique index is automatically created on the column or the group of columns.

### PostgreSQL UNIQUE constraint exmaple ###
1. New table:

```sql
CREATE TABLE person (
  id SERIAL PRIMARY KEY,
  first_name VARCHAR (50),
  last_name VARCHAR (50),
  email VARCHAR (50) UNIQUE
);
```

```sql
CREATE TABLE person (
  id SERIAL PRIMARY KEY,
  first_name VARCHAR (50),
  last_name VARCHAR (50),
  email VARCHAR (50),
  UNIQUE (email)
);
```

2. Insert rows:

```sql
INSERT INTO person (first_name, last_name, email)
VALUES ('john', 'doe', 'john.doe@example.com');
```

	1. Try to insert a second row with the same email:
	
	```sql
	INSERT INTO person (first_name, last_name, email)
	VALUES ('jack', 'doe', 'john.doe@example.com');
	```
	
	```
	ERROR:  duplicate key value violates unique constraint "person_email_key"
	Key (email)=(john.doe@example.com) already exists. 

	SQL state: 23505
	Detail: Key (email)=(john.doe@example.com) already exists.
	```

### Defining a UNIQUE constraint on multiple columns ###
1. `UNIQUE` constraint to a group of columns:

```sql
CREATE TABLE table (
  c1 data_type,
  c2 data_type,
  c3 data_type,
  UNIQUE (c2, c3)
);
```

	1. The combination of values in columns `c2` and `c3` will be unique across the whole table.

### Adding unique constraints using a unique index ###
1. Adding `UNIQUE` constraint to an existing column or a group of columns.
2. Table:

```sql
CREATE TABLE equipment (
  id SERIAL PRIMARY KEY,
  name VARCHAR (50) NOT NULL,
  equip_id VARCHAR (16) NOT NULL
);
```

2. New index:

```sql
CREATE UNIQUE INDEX CONCURRENTLY equipment_equip_id
ON equipment (equip_id);
```

3. Add a unique constraint to the `equipment` table using the `equipment_equip_id` index.

```sql
ALTER TABLE equipment
ADD CONSTRAINT unique_equip_id
UNIQUE USING INDEX equipment_equip_id;
```

	1. `ALTER TABLE` acquires an exclusive lock on the table.
		1. If we have any pending transactions, it will wait for all transactions to complete before changing the table.
			1. Check `pg_stat_activity` table to see the current pending transactions that are ongoing using the following query:
			
			```sql
			SELECT
			  datid,
			  datname,
			  usename,
			  state
			FROM
			  pg_stat_activity;
			```
			
				1. Look for `stat` column with the value `idle in transaction`
					1. The transactions that are pending to complete

### Summary ###

## PostgreSQL Not-Null Constraint ##
1. Summary: Ensures that the values of a column are not null.

### Introduction to NULL ###
1. `NULL` means unknown or missing information.
	1. It is not the same as empty string or zero.
	2. It does not equal anything including itself (`NULL` = `NULL` is `NULL`)
2. `IS NULL` - to check if the value is `NULL` or not.

```sql
email_address IS NULL
```

3. `IS NOT NULL` negates the result of `IS NULL`.

### PostgreSQL NOT NULL constraints ###
1. To control whether a column can accept `NULL`, use `NOT NULL` constraint:

```sql
CREATE TABLE table_name (
  ...
  column_name data_type NOT NULL,
  ...
);
```

### Declaring NOT NULL columns ###
1. New table:

```sql
CREATE TABLE invoices (
  id SERIAL PRIMARY KEY,
  product_id INT NOT NULL,
  qty NUMERIC NOT NULL CHECK ( qty > 0 ),
  net_price NUMERIC CHECK ( net_price > 0 )
);
```

	1. A column can have multiple constraints (`NOT NULL`, `CHECK`, `UNIQUE`, `FOREIGN KEY`) appearing next to each other.
		1. The order of the constraints is not important.
			1. PostgreSQL can check constraints in any order.
	2. `NULL` - column accepts both `NULL` and non-`NULL` values.
		1. It is the default.

### Adding NOT NULL Constraints to existing columns ###
1. To add `NOT NULL` constraint to a column of existing table:

```sql
ALTER TABLE table_name
ALTER COLUMN column_name SET NOT NULL;
```

2. To add multiple `NOT NULL` constraints to multiple columns:

```sql
ALTER TABLE table_name
ALTER COLUMN column_name_1 NOT NULL,
ALTER COLUMN column_name_2 NOT NULL,
...;
```

3. Example:

```sql
CREATE TABLE production_orders (
  id SERIAL PRIMARY KEY,
  description VARCHAR (40) NOT NULL,
  material_id VARCHAR (16),
  qty NUMERIC,
  start_date DATE,
  finish_date DATE
);
```

4. Insert new row: `production_orders`:

```sql
INSERT INTO production_orders (description)
VALUES ('Make for Infosys inc.');
```

5. If we try to add `NOT NULL` constraint to `qty` field even if it contains `NULL` values, PotgreSQL will issue an error.
	1. Solution: Update to a non-`NULL` value and then add the constraint.
	
	```sql
	UPDATE production_orders
	SET qty = 1;
	```
	
	```sql
	ALTER TABLE production_orders
	ALTER COLUMN qty
	SET NOT NULL;
	```
	
	```sql
	UPDATE production_orders
	SET material_id = 'ABC',
	    start_date = '2015-09-01',
		finish_date = '2015-09-01';
	```
	
6. Add not-null constraints to multiple columns:

```sql
ALTER TABLE production_orders
ALTER COLUMN material_id SET NOT NULL,
ALTER COLUMN start_date SET NOT NULL,
ALTER COLUMN finish_date SET NOT NULL;
```

7. Try to set `qty` column to `NULL`:

```sql
UPDATE production_orders
SET qty = NULL;
```

```
ERROR:  null value in column "qty" of relation "production_orders" violates not-null constraint
Failing row contains (1, Make for Infosys inc., ABC, null, 2015-09-01, 2015-09-01). 

SQL state: 23502
Detail: Failing row contains (1, Make for Infosys inc., ABC, null, 2015-09-01, 2015-09-01).
```

### The special case of NOT NULL constraint ###
1. `CHECK` constraint can be used to enforce non-`NULL` values:

```
CHECK ( column IS NOT NULL );
```

	1. Use-case: If we want either column `a` or `b` not null, but not both.
2. Example: Either `username` or `email` column of `user` tables is not null or empty
 
```sql
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  username VARCHAR (50),
  email VARCHAR (50),
  CONSTRAINT username_email_not_null CHECK (
    NOT (
	  (
	    username IS NULL OR
	    username = ''
	  )
	  AND
	  (
	    email IS NULL OR
		email = ''
	  )
	)
  );
);
```

3. The following statement works:

```sql
INSERT INTO users (username, email)
VALUES
  ('user1', null),
  (NULL, 'user2@example.com'),
  ('user2', 'user3#example.com'),
  ('user3', '');
```

4. The following statement will not work:

```sql
INSERT INTO users (username, email)
VALUES
  (NULL, NULL),
  (NULL, ''),
  ('', NULL),
  ('', '');
```

```
ERROR:  new row for relation "users" violates check constraint "username_email_not_null"
Failing row contains (5, null, null). 

SQL state: 23514
Detail: Failing row contains (5, null, null).
```

### How does `VARCHAR` work in PostgreSQL internally? ###

Great question! Let’s go deep into **how `VARCHAR` works internally in PostgreSQL**.

---

## 1. `VARCHAR` Overview

In PostgreSQL, `VARCHAR(n)` (a.k.a. character varying) is a **variable-length string type** with a **limit of `n` characters**. There’s also `VARCHAR` without a length specifier, which means unlimited length (like `TEXT`).

PostgreSQL treats `VARCHAR` and `TEXT` almost the same internally — the only difference is that `VARCHAR(n)` enforces a length check.

---

## 2. Storage Representation

PostgreSQL stores `VARCHAR` values using its **varlena** (variable-length) data structure:

* `varlena` = variable-length data type with a **4-byte header** (or 1-byte header for short strings).
* Layout:

  ```
  [length header][string data][optional padding]
  ```

  * **Header** stores the total length of the value in bytes.
  * **Data** is the UTF-8 encoded string.
  * **No null terminator** is stored (unlike C-strings).

So if you insert `"hello"`:

* Stored as:

  ```
  [4-byte length = 5][68 65 6C 6C 6F]
  ```

---

## 3. `VARCHAR(n)` Enforcement

* PostgreSQL does **not pad** strings (unlike `CHAR(n)`).
* When you insert into `VARCHAR(n)`:

  1. It checks that the number of **characters (not bytes)** ≤ `n`.
  2. If it exceeds, PostgreSQL throws an error (`value too long for type character varying(n)`).

👉 The check is **per-character**, not per-byte, since PostgreSQL supports multibyte UTF-8.

Example:

```sql
CREATE TABLE demo (name VARCHAR(3));

INSERT INTO demo VALUES ('abc');  -- OK
INSERT INTO demo VALUES ('abcd'); -- ERROR
```

---

## 4. Storage vs `TEXT`

* Internally, **`TEXT` and `VARCHAR` are the same**.
* Both use `varlena`.
* The only difference:

  * `TEXT` = unlimited length (up to 1 GB technically).
  * `VARCHAR(n)` = unlimited length, but with a constraint check.
* That’s why casting between `TEXT` and `VARCHAR` is basically free (no data rewrite).

---

## 5. TOAST (The Oversized-Attribute Storage Technique)

* PostgreSQL has a mechanism called **TOAST** for large values.
* If a `VARCHAR`/`TEXT` value is too big to fit in a row:

  1. It gets compressed (LZ compression).
  2. If still too large, it gets moved to a TOAST table, and only a pointer is stored in the main table.
* This allows very large strings (up to 1 GB) to be stored efficiently.

---

## 6. Performance Considerations

* `VARCHAR(n)` has a tiny overhead for length checking during inserts/updates.
* `TEXT` and `VARCHAR` (without length) are usually preferred for performance.
* `CHAR(n)` is generally avoided (due to padding overhead).
* Indexing, sorting, and comparisons work the same for `TEXT` and `VARCHAR`.

---

✅ **Summary:**

* `VARCHAR` is stored as a **varlena structure** (same as `TEXT`).
* Difference: `VARCHAR(n)` enforces a max character limit.
* Strings longer than a page can be compressed and stored externally with TOAST.
* Practically, `TEXT` and `VARCHAR` are equivalent — the choice is mostly semantic.

---

Would you like me to also explain **how PostgreSQL enforces the character count (`n`) internally** (since it needs to handle multibyte encodings like UTF-8)?

### Summary ###
1. `=` cannot be used for `NULL` because it always returns `NULL`.

## PostgreSQL DEFAULT Value ##
1. Summary: Assigning default value using `DEFAULT` constraint.

### Defining the DEFAULT value for a column of a new table ###
1. Syntax:

```sql
CREATE TABLE table_name (
  column1 type,
  column2 type DEFAULT default_value,
  column3 type,
  ...
);
```

2. `column2` will receive the `default_value` when we insert into the `table_name` without specifying a value for the column.
	1. If we don't specify `DEFAULT` constraint, the default value is `NULL`
	
	```sql
	CREATE TABLE table_name (
	  column1 type,
	  column2 type,
	  column3 type,
	  ...
	);
	```
	
		1. Default value can be: Number, string, JSON object, etc.
			1. It can be an expression that will be evaluated when the default value is inserted into the table.
			
			```sql
			CREATE TABLE table_name (
			  column1 type,
			  column2 type DEFAULT expression,
			  column3 type,
			  ...
			);
			```
		
		2. When inserting a new row into the table, we can ignore the column that has a default value
		
		```sql
		INSERT INTO table_name (column1, column3)
		VALUES (value1, value3);
		```
		
		3. To explicitly use the `DEFAULT`:
		
		```sql
		INSERT INTO table_name (column1, column2, column3)
		VALUES (value1, DEFAULT, value3);
		```

### Defining the DEFAULT value for a column of an existing table ###
1. To specify default value for an existing table:

```sql
ALTER TABLE table_name
ALTER COLUMN column2
SET DEFAULT default_value;
```

### Removing the DEFAULT value from a column ###
1. Drop a default value:

```sql
ALTER TABLE table_name
ALTER COLUMN column2
DROP DEFAULT;
```

### PostgreSQL default value examples ###
#### Basic PostgreSQL default value examples ####
1. `products` table:

```sql
CREATE TABLE products (
  id SERIAL PRIMARY KEY,
  name VARCHAR (255) NOT NULL,
  price DECIMAL (19, 2) NOT NULL DEFAULT 0
);
```

2. Insert a row:

```sql
INSERT INTO products (name)
VALUES ('Laptop')
RETURNING *;
```

3. Insert another row:

```sql
INSERT INTO products (name, price)
VALUES ('Smartphone', DEFAULT)
RETURNING *;
```

4. Insert another row:

```sql
INSERT INTO products (name, price)
VALUES ('Tablet', 699.99)
RETURNING *;
```

#### Using DEFAULT constraint with TIMESTAMP columns ####
1. New `logs` table:

```sql
CREATE TABLE logs (
  id SERIAL PRIMARY KEY,
  message TEXT NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

2. Insert a row:

```sql
INSERT INTO logs (message)
VALUES ('Started the server')
RETURNING *;
```

	1. PostgreSQL uses `CURRENT_TIMESTAMP` for the insertion.

#### Using DEFAULT constraint with JSONB type ####
1. `settings` table to store configuration data:

```sql
CREATE TABLE settings (
  id SERIAL PRIMARY KEY,
  name VARCHAR (50) NOT NULL,
  configuration JSONB DEFAULT '{}'
);
```

2. Insert a new row:

```sql
INSERT INTO settings (name)
VALUES ('global')
RETURNING *;
```

	1. Empty JSON object is used for insertion as the default value.
	
3. To remove default value:

```sql
ALTER TABLE settings
ALTER COLUMN configuration
DROP DEFAULT;
```

### Summary ###

## PostgreSQL Boolean Data Type with Practical Examples ##
1. Summary: Boolean data type. How to use it in designing tables.

### Introduction to the PostgreSQL Boolean type ###
1. PostgreSQL supports a single Boolean data type: `BOOLEAN`
2. It can have three values: `true`, `false`, or `NULL`
3. PostgreSQL uses one byte for storing a boolean value in the database
4. `BOOL` - abreviation of `BOOLEAN`
5. PostgreSQL is flexible when dealing with `TRUE` and `FALSE` values:
	1. True
		1. `true`
		2. `'t'`
		3. `'true'`
		4. `'y'`
		5. `'yes'`
		6. `'1'`
	2. False
		1. `false`
		2. `'f'`
		3. `'false'`
		4. `'n'`
		5. `'no'`
		6. `'0'`
	3. All constants exception `true` and `false` must be enclosed in single quotes.

### PostgreSQL Boolean examples ###
1. New table `stock_availability` to log which products are available.

```sql
CREATE TABLE stock_availability (
  product_id INT PRIMARY KEY,
  available BOOLEAN NOT NULL
);
```

2. Insert sample data:

```sql
INSERT INTO stock_availability (product_id, available)
VALUES
  (100, TRUE),
  (200, FALSE),
  (300, 't'),
  (400, 'f'),
  (500, 'true'),
  (600, 'false'),
  (700, 'y'),
  (800, 'n'),
  (900, 'yes'),
  (1000, 'no'),
  (1100, '1'),
  (1200, '0');
```

3. Check for availability of products:

```sql
SELECT *
FROM stock_availability
WHERE available = 'yes';
```

4. We can imply true value by using Boolean column without any operator.
	1. Example:
	
	```sql
	SELECT * FROM stock_availability
	WHERE available;
	```
	
5. Return products that are not available:

```sql
SELECT * FROM stock_availability
WHERE available = 'no';
```

6. Return products that are not available using `NOT` operator:

```sql
SELECT 
  * 
FROM 
  stock_availability
WHERE 
  NOT available;
```

### Set the default values for Boolean columns ###
1. To set a default value for an existing Boolean column, use `SET DEFAULT` clause in `ALTER TABLE`:

```sql
ALTER TABLE stock_availability
ALTER COLUMN available
SET DEFAULT FALSE:
```

2. If you insert a row, PostgreSQL will use `FALSE` by default.

```sql
INSERT INTO stock_availability (product_id)
VALUES (900);
```

```sql
SELECT *
FROM stock_availability
WHERE product_id = 900;
```

3. Use `DEFAULT` constraint in column definition during creation of a table:

```sql
CREATE TABLE boolean_demo (
  ...
  is_ok BOOL DEFAULT 't'
);
```

### Summary ###

## PostgreSQL Character Types: CHAR, VARCHAR, and TEXT ##
1. Summary: `CHAR`, `VARCHAR`, and `TEXT`

### Introduction to the PostgreSQL character types ###
1. PostgreSQL provides three primary character types:
	1. `CHARACTER(n)` or `CHAR(n)`
	2. `CHARACTER VARYING(n)` or `VARCHAR(n)`
	3. `TEXT`
2. `n` - positive integer that specifies the number of characters.
3. `CHARACTER VARYING(n)`, `VARCHAR(n)` - variable length with length limit.
4. `CHARACTER(n)`, `CHAR(n)` - fixed-length, blank padded.
5. `TEXT`, `VARCHAR` - variable unlimited length.
6. `CHAR(n)`, and `VARCHAR(n)` can store up to `n` characters.
	1. If we attempt to store more than `n` characters, PostgreSQL will issue an error.
		1. Exception: If the excessive characters are all spaces, PostgreSQL truncates the spaces to the maximum length (`n`) and stores the trimmed characters.
	2. If a string explicitly casts to a `CHAR(n)` or `VARCHAR(n)`, PostgreSQL will truncate the string to `n` characters before inserting it into the table.
7. `TEXT` can store a string with unlimited length.
	1. `VARCHAR` behaves similar to `TEXT` if `n` is not specified.
		1. The performance of both are the same.
8. The purpose of specifying `n` for `VARCHAR` is that PostgreSQL will issue an error if you attempt to insert a string that has more than `n` characters into the `VARCHAR(n)` column.
9. `CHARACTER` or `CHAR` without `n` is `CHARACTER(1)` or `CHAR(1)`.
10. In PostgreSQL, there is no performance difference between the three character types.
11. Tip: Use `TEXT` or `VARCHAR` in general but use `VARCHAR(n)` if you want PostgreSQL to check for the length.

### PostgreSQL character type examples ###
1. New table: `character_tests`:

```sql
CREATE TABLE character_tests (
  id SERIAL PRIMARY KEY,
  x CHAR (1),
  y VARCHAR (10),
  z TEXT
);
```

2. Insert a new row:

```sql
INSERT INTO character_tests (x, y, z)
VALUES
  (
    'Yes', 'This is a test for varchar',
	'This is a very long text for the PostgreSQL text column'
  );
```

```
ERROR:  value too long for type character(1) 

SQL state: 22001
```

3. Fix:

```sql
INSERT INTO character_tests (x, y, z)
VALUES
  (
    'Y', 'This is a test for varchar',
	'This is a very long text for the PostgreSQL text column'
  );
```

4. Fix:

```sql
INSERT INTO character_tests (x, y, z)
VALUES
  (
    'Y', 
	'varchar(n)',
	'This is a very long text for the PostgreSQL text column'
  )
RETURNING *;
```

### Summary ###
1. `CHAR` - fixed length data type
2. `VARCHAR` and `TEXT` - varying length data types
3. `VARCHAR(n)` - to validate the length of the string before inserting into or updating a column.
4. `VARCHAR` and `TEXT` are equivalent.

## PostgreSQL NUMERIC Type ##
1. Summary: `NUMERIC` **(M)** type

### Introduction to PostgreSQL NUMERIC data type ###
1. `NUMERIC` type can store numbers with a lot of digits
	1. Typically used to store numbers that require exactness (monetary amounts or quantities)
2. Syntax:

```sql
column_name NUMERIC (precision, scale)
```

	1. `precision` - total number of digits
	2. `scale` - number of digits in the fraction part
3. The storage type depends on `precision` and `scale`
	1. There can be maximum `131,072` digits before the decimal point.
	2. There can be maximum `16,383` digits after the decimal point.
	3. `scale` can be 0, +ve, or -ve (PostgreSLQ 15 or above)
4. Example:

```sql
price NUMERIC (7, 2)
```

	1. `7` - total number of digits
	2. `2` - digits after the decimal point (`5` digits before the decimal point)
5. Negative scale:

```sql
amount NUMERIC (5, -2)
```

	1. `precision` + `scale` digits on the left and no digits on the right. (`5 + 2` = `7` digits on the left)
	
6. Numeric with zero scale:

```sql
quantity NUMERIC (5, 0)
```

	1. It is equivalent to the following:
	
	```sql
	quantity NUMERIC (5)
	```
	
7. If we ommit `precision` and `scale`, they will default to the maximum.

```sql
NUMERIC
```

#### NUMERIC, DECIMAL, and DEC types ####
1. `NUMERIC` and `DECIMAL` are synonymous and can be used interchangeably.

```sql
DECIMAL (p, s)
```

	1. `DEC` - shorter name
2. **If precision is not required, `NUMERIC` must not be used because they are typically slower than `integer`, `float`, and double precisions.**

##### Special values #####
1. `NUMERIC` type has special values:
	1. `Infinity`
	2. `-Infinity`
	3. `NaN`

### PostgreSQL NUMERIC data type examples ###
#### Storing numeric values ####
1. If we store a value with a scale that is greater than the declared scale of `NUMERIC` column, PostgreSQL will round the value to a specified number of fractional digits.
	1. Example: New table.
	
	```sql
	CREATE TABLE products (
	  id SERIAL PRIMARY KEY,
	  name VARCHAR (100) NOT NULL,
	  price NUMERIC (5, 2)
	);
	```
	
		1. Insert some products with prices whose scales exceed the scale declared in the `price` column:
		
		```sql
		INSERT INTO products (name, price)
		VALUES ('Phone', 500.215),
		       ('Tablet', 500.214);
		```
		
			1. PostgreSQL rounds the value up to `500.22` and `500.21` respectively.
		2. Returning all rows of the `products` table:
		
		```sql
		SELECT * FROM products;
		```
		
2. If you store a value whose precision exceeds the declared precision, PostgreSQL will raise an error.

```sql
INSERT INTO products (name, price)
VALUES ('Phone', 123456.21);
```

```
ERROR:  numeric field overflow
A field with precision 5, scale 2 must round to an absolute value less than 10^3. 

SQL state: 22003
Detail: A field with precision 5, scale 2 must round to an absolute value less than 10^3.
```

#### PostgreSQL NUMERIC type and NaN ####
1. `NaN` - Not a number
2. Example:

```sql
UPDATE products
SET price = 'NaN'
WHERE id = 1;
```

	1. Use single quotes to wrap `NaN`.
	2. Return data of `products` table:
	
	```sql
	SELECT * FROM products;
	```
	
		1. Typically `NaN` is not equal to any number including itself.
			1. `NaN = NaN` is `false`. 
				1. Exception: In PostgreSQL, `NaN` values are equal.
				2. Exception: `NaN` values are greater than regular numbers (1, 2, 3, ...)
					1. Allows PostgreSQL to sort `NUMERIC` values and use then in three-based indexes.
						1. Example: Sort products based on prices from high to low:
						
						```sql
						SELECT * FROM products
						ORDER BY price DESC;
						```

### Summary ###
1. `NUMERIC` data type is used to store numbers that require exactness.

## PostgreSQL DOUBLE PRECISION Data Type ##
1. Summary: `DOUBLE PRECISION` data type.

### Introduction to the PostgreSQL double precision type ###
1. `DOUBLE PRECISION` - inexact, variable-precision numeric type.
	1. Inexact: PostgreSQL cannot exactly convert some values into an internal format but can only store them as approximations.
		1. Storing and querying a value might show a slight difference
			1. Alternative: Use numeric type if your application requires exact storage and calculation
	2. It is an implementation of the IEEE Standard 754 for Floating-Point Arithmetic.
2. Syntax:

```sql
column_name DOUBLE PRECISION
```

3. Syntax: `FLOAT8` or `FLOAT` - same as `DOUBLE PRECISION`

```
column_name FLOAT
```

4. Range: Around `1E-307` to `1E+308` which a precision of at least 15 digits
	1. If we try to store a value that is out of the range, PostgreSQL will not be able to store it and raise an error
	2. Is we try to store numbers with very high precision, PostgreSQL may round them to fit within the limitation of double precision (causes some precision to be lost)
	3. If we try to store very small numbers close to zero, PostgreSQL may raise an underflow error due to the limitations of double precision data type.
		1. It may be unable to represent such small values distinct from zero
5. Application: Used for storing scientific measurements

### PostgreSQL double precision type examples ###
#### Basic double precision data type example ####
1. Table: `temperatures`:

```sql
CREATE TABLE temperatures (
  id SERIAL PRIMARY KEY,
  location TEXT NOT NULL,
  temperature DOUBLE PRECISION
);
```

2. Insert some rows into `temperatures` table:

```sql
INSERT INTO
  temperatures (location, temperature)
VALUES
  ('Lab Room 1', 23.5),
  ('Server Room 1', 21.8),
  ('Server Room 2', 24.3)
RETURNING *;
```

3. Average temperature of all locations:

```sql
SELECT AVG(temperature)
FROM temperatures;
```

#### Storing inexact values ####
1. New table `t`:

```sql
CREATE TABLE t (c DOUBLE PRECISION);
```

2. Insert rows into `t`:

```sql
INSERT INTO t (c)
VALUES
  (0.1),
  (0.1),
  (0.1)
RETURNING *;
```

3. Calculate sum of values using `SUM` function:

```sql
SELECT SUM(c)
FROM t;
```

	1. `0.300....04`
		1. That is because PostgreSQL cannot store `0.1` exactly.

#### Inserting too small numbers ####
1. Attempt to insert a very small number:

```sql
INSERT INTO t (c)
VALUES (1E-400);
```

	1. The number is too small and very close to zero.
		1. PostgreSQL cannot store it due to the limitation of the double precision type.

### Summary ###
1. `DOUBLE PRECISION` data type represents inexact numbers.
2. `DOUBLE PRECISION`, `FLOAT8`, or `FLOAT` are synonyms.

## PostgreSQL REAL Data Type ##
1. Summary: `REAL` data type is used to store single-precision floating point numbers in the database

### Introduction to the PostgreSQL REAL data type ###
1. It takes 4 bytes of storage space.
	1. Valid range: -3.40282347 x 1E38 to 3.40282347 x 1E38
	2. Used to store large ranges and when precision is not critical
	3. Used when we are concerned about the storage space
	4. `DOUBLE PRECISION` data type has higher precision

### PostgreSQL REAL data type example ###
1. Table `weathers` to store wind speed (meter per second) and temperature (celsius) data

```sql
CREATE TABLE weathers (
  id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
  location VARCHAR (255) NOT NULL,
  wind_speed_mps REAL NOT NULL,
  temperature_celcius REAL NOT NULL,
  recorded_at TIMESTAMP NOT NULL
);
```

2. Insert rows into the `weathers` table:

```sql
INSERT INTO weathers (location, wind_speed_mps, temperature_celsius, recorded_at)
VALUES
    ('New York', 5.2, 15.3, '2024-04-19 09:00:00'),
    ('New York', 4.8, 14.9, '2024-04-19 10:00:00'),
    ('New York', 6.0, 16.5, '2024-04-19 11:00:00'),
    ('New York', 5.5, 15.8, '2024-04-19 12:00:00'),
    ('New York', 4.3, 14.2, '2024-04-19 13:00:00'),
    ('New York', 5.9, 16.1, '2024-04-19 14:00:00'),
    ('New York', 6.8, 17.3, '2024-04-19 15:00:00'),
    ('New York', 5.1, 15.6, '2024-04-19 16:00:00'),
    ('New York', 4.7, 14.8, '2024-04-19 17:00:00'),
    ('New York', 5.3, 15.9, '2024-04-19 18:00:00');
```

3. Calculate average wind speed and temperature in New York on April 19, 2024:

```sql
SELECT 
  AVG(wind_speed_mps) wind_speed,
  AVG(temperature_celsius) temperature
FROM
  weathers
WHERE
  location = 'New York'
  AND
  DATE(recorded_at) = '2024-04-19';
```

### Summary ###

## PostgreSQL Integer Data Types ##
1. Summary: `SMALLINT`, `INTEGER`, and `BIGINT`

### Introduction to PostgreSQL integer types ###
1. Use one of the following:
	1. `SMALLINT` - 2 bytes
	2. `INTEGER` - 4 bytes
	3. `BIGINT` - 8 bytes
2. If you attempt to store a value outside the permitted ranges, PostgreSQL will issue an error.
3. PostgreSQL does not provide unsigned integer types (unlike MySQL).

### SMALLINT ###
1. Requires 2 bytes storage size.
2. Range: -32,768 to 32,767
3. Usage: Ages of people, number of pages in a book, ...
4. Example: `books` class:

```sql
CREATE TABLE books (
  book_id SERIAL PRIMARY KEY,
  title VARCHAR (255) NOT NULL,
  pages SMALLINT NOT NULL CHECK ( pages > 0 )
);
```

### INTEGER ###
1. It is the most common choice.
	1. It offers the best balance between storage size, range, and performance
2. It requires 4 bytes storage size
	1. Range: (-2,147,483,648, 2,147,483,647)
3. Usage: To store population of a city, or country.
4. Example:

```sql
CREATE TABLE cities (
  city_id SERIAL PRIMARY KEY,
  city_name VARCHAR (255) NOT NULL,
  population INT NOT NULL CHECK ( population >= 0 )
);
```

5. `INT` is synonym of `INTEGER`

### BIGINT ###
1. To store whole numbers out of the range of `INTEGER`, use `BIGINT` type.
2. Size: 8 bytes
	1. Range: (-9,223,372,036,854,775,808,+9,223,372,036,854,775,807)
3. It consumes more storage.
4. It decreases performance of the Database
	1. Have a good reason to use it.

### Summary ###

## PostgreSQL DATE Data Type ##
1. Summary: `DATE` data type.
	1. Handy date functions to handle date values.

### Introduction to the PostgreSQL DATE data type ###
1. `DATE` allows you to store date data.
2. PostgreSQL uses 4 bytes to store a date value.
	1. Range: 4713 BC to 5874897 AD
3. Format: `yyyy-mm-dd`
	1. For insertion and storage
4. `CURRENT_DATE` - can be used to specify default value of a column using the `DEFAULT` constraint
5. Example:

```sql
CREATE TABLE documents (
  document_id SERIAL PRIMARY KEY,
  header_text VARCHAR (255) NOT NULL,
  posting_date DATE NOT NULL DEFAULT CURRENT_DATE
);
```

6. Inserting current date:

```sql
INSERT INTO documents (header_text)
VALUES ('Billing to customer XYZ')
RETURNING *;
```

### PostgreSQL DATE functions ###
1. Example: `employees` table with `employee_id`, `first_name`, `last_name`, `birth_date`, and `hire_date`

```sql
CREATE TABLE employees (
  employee_id SERIAL PRIMARY KEY,
  first_name VARCHAR (255) NOT NULL,
  last_name VARCHAR (255) NOT NULL,
  birth_date DATE NOT NULL,
  hire_date DATE NOT NULL
);

INSERT INTO employees (first_name, last_name, birth_date, hire_date)
VALUES ('Shannon','Freeman','1980-01-01','2005-01-01'),
       ('Sheila','Wells','1978-02-05','2003-01-01'),
       ('Ethel','Webb','1975-01-01','2001-01-01')
RETURNING *;
```

#### Get the current date ####
1. Get the current date:

```sql
SELECT CURRENT_DATE; -- works

SELECT NOW(); -- **(M)** longer date format - 2025-09-11 19:17:29.96476+05:30
```

2. Type-casting: `::`
	1. To get date part only:
	
	```sql
	SELECT NOW()::DATE;
	```
	
3. A quick way to get the current date:

```sql
SELECT CURRENT_DATE;
```

4. The date can be formatted into a different format using the `TO_CHAR()` function.

#### Output a PostgreSQL date value in a specific format ####
1. `TO_CHAR()` - to output date in a different format.
	1. Parameters:
		1. Value to format
		2. Template that defines the output format
	2. Example: To display date in the format: `dd/mm/yyyy`
	
	```sql
	SELECT TO_CHAR(NOW()::DATE, 'dd/mm/yyyy');
	
	SELECT TO_CHAR(CURRENT_DATE, 'dd/mm/yyyy');
	```
	
	3. Display date in the following format: `Mon dd, yyyy`
	
	```sql
	SELECT TO_CHAR(NOW()::DATE, 'Mon dd, yyyy');
	```

#### Get the interval between two dates ####
1. `-` operator - to get interval between two dates.
2. To retrieve service days of employees - subtract hire_date from today's date.

```sql
SELECT
  first_name,
  last_name,
  now() - hire_date as diff
FROM
  employees;
```

#### Calculate ages in years, months, and days ####
1. `AGE` **(M)**: To calculate age at current date in years, months, and days.

```sql
SELECT
  employee_id,
  first_name,
  last_name,
  AGE(birth_date)
FROM
  employees;
```

2. If you pass date value to `AGE()` function, it will subtract the date value from the current date.
3. If you pass two arguments to `AGE()` function, it will subtract the second argument from the first argument.
	1. Example: Get the age of employees on `01/01/2015`
	
	```sql
	SELECT
	  employee_id,
	  first_name,
	  last_name,
	  AGE('2015-01-01', birth_date)
	FROM
	  employees;
	```

#### Extract year, quarter, month, week, and day from a date value ####
1. `EXTRACT()` - used to get year, quarter, month, week, and day from a date value
2. Example:

```sql
SELECT
  employee_id,
  first_name,
  last_name,
  EXTRACT (YEAR FROM birth_date) AS YEAR,
  EXTRACT (MONTH FROM birth_date) AS MONTH,
  EXTRACT (DAY FROM birth_date) AS DAY
FROM
  employees;
```

## PostgreSQL Timestamp Data Types ##
1. Summary: `TIMESTAMP` and `TIMESTAMPZ`
	1. Handy functions to handle timestamp effectively

### Introduction to PostgreSQL timestamp ###
1. Two data types:
	1. `TIMESTAMP` - Timestamp without a timezone.
	2. `TIMESTAMPTZ` - Timestamp with a timezone.
2. `TIMESTAMP` - It allows us to store both date and time.
	1. It does not have any timezone
	2. If we change the timezone of database server, the timestamp value stored in the database will not change automatically
3. `TIMESTAMPTZ` - Timezone-aware date and time data type
	1. `TIMESTAMPTZ` is internally stored in UTC value.
		1. Stored in 8 bytes
			1. Stores number of microseconds since PostgreSQL's epoch (`2000-01-01 00:00:00 UTC` - different from UNIX epoch)
				1. UTC microseconds since epoch
		2. When we query the value, PostgreSQL applies the current session time zone for display.
	2. When you insert a value into a `TIMESTAMPTZ` column, PostgreSQL converts the value into a UTC value and stores the UTC value in the table.
	3. When you retrieve data from `TIMESTAMPTZ` column, PostgreSQL converts the UTC value back to the time value of the timeszone set by the database server, the user, or the current database connection
4. Size:

```sql
SELECT
  typname,
  typlen
FROM
  pg_type
WHERE
  typname ~ '^timestamp';
```

### PostgreSQL timestamp example ###
1. Table `timestamp_demo`:

```sql
CREATE TABLE timestamp_demo (
  ts TIMESTAMP,
  tstz TIMESTAMPTZ
);
```

2. Set timezone of DB server to `America/Los_Angeles`

```sql
SET timezone = 'America/Los_Angeles';
```

	1. See the current timezone:
	
	```sql
	SHOW TIMEZONE;
	```
	
3. Insert a new row:

```sql
INSERT INTO timestamp_demo (ts, tstz)
VALUES ('2016-06-22 19:10:25-07', '2016-06-22 19:10:25-07');
```

4. Query data:

```sql
SELECT
  ts, tstz
FROM
  timestamp_demo;
```

	1. The value in `timestamp` column does not change but value in `timestamptz` column is adjusted to the new time zone of 'America/New_York'.
5. Tip: Use `TIMESTAMPTZ` to store timestamp data.

### PostgreSQL timestamp functions ###
1. Handy functions to handle timestamp data effectively.

#### Getting the current time ####
1. `NOW()` **(M)** - to get current timestamp

```sql
SELECT NOW();
```

2. `CURRENT_TIMESTAMP` - alternative

```sql
SELECT CURRENT_TIMESTAMP;
```

3. `CURRENT_TIME` **(M)** - time without date
	1. Returns time with timezone.
	
4. `TIMEOFDAY()` **(M)** - returns time of the day in string format.

#### Convert between timezones ####
1. `timezone(zone, timestamp)` **(M)** - to convert timestamp to another timezone

```sql
SHOW TIMEZONE;
```

2. To convert `2016-06-01 00:00` to `America/Los_Angeles` timezone:

```sql
SELECT timezone('America/Los_Angeles', '2016-06-01 00:00');
```

	1. The timestamp string is implicitly cast to `TIMESTAMPTZ`
		1. Explicit casting is better:
		
		```sql
		SELECT timezone('2016-06-01 00:00', 'America/Los_Angeles'::TIMESTAMPTZ);
		```

### Using default values for timestamp columns ###
1. New table: `department`:

```sql
CREATE TABLE department (
  id SERIAL PRIMARY KEY,
  name VARCHAR NOT NULL,
  created_at TIMESTAMPTZ DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMPTZ DEFAULT CURRENT_TIMESTAMP
);
```

	1. The default values are `CURRENT_TIMESTAMP` function values
2. New row:

```sql
INSERT INTO department (name)
VALUES ('IT')
RETURNING *;
```

	1. Current time is inserted into `created_at` and `updated_at` columns.
	2. To update value in `updated_at` column each time a row is updated, `BEFORE UPDATE` trigger needs to be created.
		1. MySQL has `ON UPDATE CURRENT_TIMESTAMP` - automatically updates `TIMESTAMP` column. - PostgreSQL does not support this feature.
		2. `BEFORE UPDATE` trigger:
		
		```sql
		CREATE OR REPLACE FUNCTION update_updated_at()
		RETURNS TRIGGER AS $$
		BEGIN
		  NEW.updated_at = current_timestamp;
		  RETURN NEW;
		END;
		$$ LANGUAGE plpgsql;
		
		CREATE TRIGGER department_updated_at_trigger
		BEFORE UPDATE ON department
		FOR EACH ROW
		EXECUTE FUNCTION update_updated_at();
		```
		
3. Update name of IT department to ITD without specifying a value for `updated_at` column:

```sql
UPDATE department
SET name = 'ITD'
WHERE id = 1
RETURNING *;
```

	1. `updated_at` is updated automatically.

### Summary ###
1. PostgreSQL stores `timestamptz` values in the database as UTC values.

## PostgreSQL Interval Data Type ##
1. Summary: PostgreSQL interval data type
	1. How to manipulate interval values.

### Introduction to PostgreSQL Interval Data Type ###
1. It allows us to store and manipulate a period in years, months, days, hours, minutes, and seconds.

```sql
@ interval [ fields ] [ (p) ]
```

	1. Interval value requires 16 bytes of storage (128 bits - 1/4 K bits)
	2. Range: -178,000,000 to 178,000,000 years
	3. `p` - optional precision value
		1. Range: 0 to 6
		2. It is the number of fraction digits retained in the second field
	4. `@` is optional - it can be ommitted
2. Examples:

```sql
interval '2 months ago';
interval '3 hours 20 minutes';
```

	1. Internally, the values are stored in months, days, and seconds.
		1. Months and days are integers
		2. Seconds can have fractions
3. Use-cases:
	1. For date and time arithmetic.
		1. Example: 3 hours 20 minutes ago at the current time of last year
		
		```sql
		SELECT
		  now(),
		  now() - INTERVAL '1 year 3 hours 20 minutes'
		    AS "3 hours 20 minutes ago of last year";
		```

### PostgreSQL interval input format ###
1. Syntax to write the interval values:

```sql
quantity unit [quantity unit...] [direction]
```

	1. `quantity`: a number. + or - are also accepted.
	2. `unit`: 
		1. `millenium`
		2. `century`
		3. `decade`
		4. `year`
		5. `month`
		6. `week`
		7. `day`
		8. `hour`
		9. `minute`
		10. `second`
		11. `millisecond`
		12. `microsecond`
		13. Abbreviation - `y`, `m`, `d`, ...
		14. Plural forms - `months`, `days`, ...
	3. `direction`: `ago` or `` (empty string)
2. The format is called `postgres_verbose`
	1. It is also used as the interval output format
3. Examples:

```sql
INTERVAL '1 year 2 months 3 days'; -- returns it as it is
INTERVAL '2 weeks ago'; -- returns a negative value of '-14 days'
```

#### ISO 8601 interval format ####
1. Postgres allows us to write interval values using `ISO 8601` time intervals
	1. In two ways.
		1. Format with designators
			1. `P quantity unit [ quanity unit ...] [ T [ quantity unit ...]]`
				1. `P` - interval value must start with this letter.
				2. `T` - To determine time of day unit
		2. Alternative format
			1. `P [ years-months-days ] [ T hours:minutes:seconds ]`
				1. `P` - interval value must start with this letter.
				2. `T` - separates the date and time parts of the interval value.
2. ISO 8601 interval unit abbreviations
	1. `Y` - years
	2. `M` - months
	3. `W` - weeks
	4. `D` - days
	5. `H` - hours
	6. `M` - minutes
		1. It is minutes if it appears after `T`
	7. `S` - seconds
3. Example: '6 years 5 months 4 days 3 hours 2 minutes 1 second'
	1. ISO 8601: `P6Y5M4DT3H2M1S`
	2. ISO 8601: `P0006-05-04T03:02:01` 

### PostgreSQL interval output format ###
1. The output style of interval values is set by using the `SET intervalstyle` **(M)** command.
	1. `SET intervalstyle = 'sql_standard';`
		1. PostgreSQL provides 4 output formats:
			1. `sql_standard`
			2. `postgres` (default)
			3. `postgres_verbose`
			4. `iso_8601`
2. Examples:

```sql
SET intervalstyle = 'sql_standard';
SELECT
  INTERVAL '6 years 5 months 4 days 3 hours 2 minutes 1 second'; -- +6-5 +4 +3:02:01
  
SET intervalstyle = 'postgres';
SELECT
  INTERVAL '6 years 5 months 4 days 3 hours 2 minutes 1 second'; -- 6 years 5 mons 4 days 03:02:01
  
SET intervalstyle = 'postgres_verbose';
SELECT
  INTERVAL '6 years 5 months 4 days 3 hours 2 minutes 1 second'; -- @ 6 years 5 mons 4 days 3 hours 2 mins 1 sec
  
SET intervalstyle = 'iso_8601';
SELECT
  INTERVAL '6 years 5 months 4 days 3 hours 2 minutes 1 second'; -- P6Y5M4DT3H2M1S
```

### PostgreSQL interval-related operators and functions ###
#### Interval operators ####
1. We can apply arithmetic operator (+, -, *, etc) to the interval values.
2. Example:

```sql
SELECT INTERVAL '2h 50m' + INTERVAL '10m'; -- 03:00:00
SELECT INTERVAL '2h 50m' - INTERVAL '50m'; -- 02:00:00
SELECT 600 * INTERVAL '1 minute'; -- 10:00:00
```

#### Converting PostgreSQL interval to string ####
1. Use `TO_CHAR()` **(M)**

```sql
TO_CHAR(interval, format)
```

2. `TO_CHAR()` function takes the first argument as an interval value, the second one as the format, and returns a string that represents the interval in the specified format.

```sql
SELECT
  TO_CHAR(
    INTERVAL '17h 20m 05s',
	'HH24:MI:SS'
  );
  
-- 17:20:05
```

#### Extracting data from a PostgreSQL interval ####
1. `EXTRACT()` - to extract year, month, date, etc.
2. Syntax:

```sql
EXTRACT(field FROM interval) -- **(M)**
```

	1. `field` - `year`, `month`, `date`, `hour`, `minutes`, ...
	2. It returns a value of type double precision.
3. Example:

```sql
SELECT
  EXTRACT (
    MINUTE
	FROM
	INTERVAL '5 hours 21 minutes'
  );
  
-- 21
-- MINUTES - works
```

#### Adjusting interval values ####
1. `justify_days` **(M)** - adjusts interval of 30-day as 1 month.
2. `justify_hours` **(M)** - adjusts interval of 24-hours as one day.
3. `justify_interval` **(M)** adjusts interval using `justify_days` and `justify_hours` with additional sign adjustments.
	
	```sql 
	SELECT 
	  justify_interval(INTERVAL '1 year -1 hour');
	  
	-- 11 mons 29 days 23:00:00 -- postgres format `SET intervalstyle = 'postgres';`
	```

### Using interval type in a table ###
1. `event` table

```sql
CREATE TABLE event (
  id SERIAL PRIMARY KEY,
  event_name VARCHAR (255) NOT NULL,
  duration INTERVAL NOT NULL
);
```

2. Insert rows:

```sql
INSERT INTO event (event_name, duration)
VALUES 
  ('pgConf', '1 hour 20 minutes'),
  ('pgDAY', '2 days 5 hours')
RETURNING *;
```

3. Extract components (days, hours, minutes) from values in the `interval` column:

```sql
SELECT
  event_name,
  duration,
  EXTRACT(DAYS FROM duration) AS days,
  EXTRACT(HOURS FROM duration) AS hours,
  EXTRACT(MINUTES FROM duration) AS minutes
FROM 
  event;
```

4. Retrieve events who duration is longer than one day:

```sql
SELECT
  event_name,
  duration
FROM
  event
WHERE duration > INTERVAL '1 day';
```

5. Calculate the total duration for all events:

```sql
SELECT
  SUM(duration) AS total_duration
FROM
  event;
```

6. Extract components of total duration using a common table expression (CTE):

```sql
WITH cte AS(
  SELECT SUM(duration) AS total_duration
  FROM event
)
SELECT
  total_duration,
  EXTRACT(DAY FROM total_duration) AS day,
  EXTRACT(HOUR FROM total_duration) AS hours,
  EXTRACT(MINUTE FROM total_duration) AS minutes
FROM
  cte;
```

## PostgreSQL TIME Data Type ##
1. Summary: `TIME` data types
	1. Handy functions to handle time values.
	
### Introduction to PostgreSQL TIME data type ###
1. To store time data.
2. Syntax:

```sql
column_name TIME(precision);
```

	1. `precision` - factional seconds precision for the time value (1 to 6)
	2. It requires 8 bytes.
	3. Allowed range: `00:00:00` to `24:00:00`
3. Common formats of time value:

```sql
HH:MI
HH:MI:SS
HHMISS
```

4. Examples:

```sql
01:02
01:02:03
010203
```

5. Time value with precision:

```sql
MI:SS.pppppp
HH:MI:SS.pppppp 
HHMISS.pppppp
```

6. Examples:

```sql
04:59.999999
04:05:06.999999
040506.999999
```

5. Any `TIME` format is acceptable including SQL-compatible, ISO 8601, ...

### PostgreSQL TIME data type example ###
1. Used to store only time of day - time of an event or shift.
2. New table: `shifts`

```sql
CREATE TABLE shifts (
  id SERIAL PRIMARY KEY,
  shift_name VARCHAR NOT NULL,
  start_at TIME NOT NULL,
  end_at TIME NOT NULL
);
```

3. Insert rows:

```sql
INSERT INTO shifts (shift_name, start_at, end_at)
VALUES ('Morning', '08:00:00', '12:00:00')
       ('Afternoon', '13:00:00', '17:00:00'),
	   ('Night', '18:00:00', '22:00:00');
```

4.  Query data:

```sql
SELECT * FROM shifts;
```

### PostgreSQL TIME WITH TIME ZONE type ###
1. `TIME WITH TIME ZONE` **(M)** data type
	1. To manipulate time of day with time zone.
2. Declaration:

```sql
column TIME WITH TIME ZONE
```

	1. Storage size: 12 bytes
	2. Time zone range: `00:00:00+1459` to `24:00:00-1459`
	3. Examples:
	
	```sql
	04:05:06 PST
	04:05:06.789-8
	```
	
		1. Recommendation: `TIMESTAMP` instead of `TIME WITH TIME ZONE`
			1. Time zone has little meaning unless it is associated with both date and time

### Handling PostgreSQL TIME values ###
#### Getting the current time ####
1. To get current time with time zone:

```sql
SELECT CURRENT_TIME;
```

2. To get current time with specific precision:

```sql
SELECT CURRENT_TIME(5);
```

	1. Without the precision, `CURRENT_TIME` returns a time value with full precision.
3. To get local time:

```sql
SELECT LOCALTIME;
```

4. Local time with specific precision:

```sql
SELECT LOCALTIME(0);
```

#### Converting time to a different time zone ####
1. Syntax:

```sql
[TIME with time zone] AT TIME ZONE time_zone
```

2. Example: Convert `LOCALTIME` to time zone `UTC-7`

```sql
SELECT LOCALTIME AT TIME ZONE 'UTC-7';
```

#### Extracting hours, minutes, and seconds from a time value ####
1. Use `EXTRACT` function to extract hours, minutes, and seconds

```sql
EXTRACT (field FROM time_value);
```

2. Examples:

```sql
SELECT
  LOCALTIME, 
  EXTRACT (HOUR FROM LOCALTIME) as hour,
  EXTRACT (MINUTE FROM LOCALTIME) as minute,
  EXTRACT (SECOND FROM LOCALTIME) as second,
  EXTRACT (MILLISECONDS FROM LOCALTIME) as milliseconds;
```

### PostgreSQL TIME example ###
#### Arithmetic operations on time values ####
1. PostgreSQL allows arithmetic operations such as +, -, and `*` on time values and between time and interval values
2. Example: Return interval between two times

```sql
SELECT TIME '10:00' - TIME '02:00' AS result;
```

3. Add 2 hours to local time:

```sql
SELECT LOCALTIME + INTERVAL '2 hour' AS result;
```

	1. The sum of a time value and an interval value is a time value

### Summary ###
1. `TIME` is used to store time data.

## PostgreSQL UUID Data Type ##
1. Summary: UUID data type, generating UUID values using a supplied module.

### Introduction to PostgreSQL UUID type ###
1. UUID: Universal Unique Identifier
2. UUID is a 128-bit quantity generated by an algorithm that makes it unique in the known universe using the same algorithm.
3. UUID is a sequence of 32 digits of hexadecimal digits represented in groups separated by hyphens
4. Use-cases:
	1. Found in distributed systems
		1. It guarantees uniqueness than the `SERIAL` data type which generates unique values within a single database
5. `UUID` datatype to store UUID values

### Generating UUID values ###
1. `gen_random_uuid()` **(M)**
2. Example:

```sql
SELECT gen_random_uuid();
```

### Constructing a table with a UUID column ###
1. Table with UUID as the primary key
2. The values will be generated automatically using `gen_random_uuid()` function:

```sql
CREATE TABLE contacts (
  contact_id UUID DEFAULT gen_random_uuid(),
  first_name VARCHAR NOT NULL,
  last_name VARCHAR NOT NULL,
  email VARCHAR NOT NULL,
  phone VARCHAR,
  PRIMARY KEY (contact_id)
);
```

	1. Whenever we insert a new row without specifying the value for `contact_id`, PostgreSQL will call `gen_random_uuid()` function to generate the value for it.
3. Insert some data:

```sql
INSERT INTO contacts (first_name, last_name, email, phone)
VALUES
  ('John', 'Smith', 'john.smith@example.com', '408-237-2345'),
  ('Jane', 'Smith', 'jane.smith@example.com', '408-237-2344'),
  ('Alex', 'Smith', 'alex.smith@example.com', '408-237-2343')
RETURNING *;
```

### Using uuid-ossp module in the old version of PostgreSQL ###
1. [uuid-ossp](https://www.postgresql.org/docs/16/uuid-ossp.html)
	1. Provides specific algorithms to generate UUIDs
	2. Installation:
	
	```sql
	CREATE EXTENSION IF NOT EXISTS "uuid-ossp";
	```
	
	3. Generation of values:
	
	```sql
	SELECT uuid_generate_v4();
	```

### Summary ###
1. UUID: Universal Unique Identifier
2. Use `gen_random_uuid()` to generate a version 4 (random) UUID.

## PostgreSQL Array ##
1. Summary: PostgreSQL array, handy functions for array manipulation

### Introduction to PostgreSQL array data type ###
1. An array of a collection of elements that have the same data type
2. Arrays can be one-dimensional, multidimensional, or nested arrays
3. **Every data type has its companion array type**
	1. `integer[]`
	2. `character[]`
4. If a user-defined data type is defined, PostgreSQL automatically constructs a corresponding array type automatically
5. Defining a column:

```sql
column_name datatype []
```

6. Example: A new table `contacts` with the `phones` column defined with an array of text

```sql
CREATE TABLE contacts (
  id SERIAL PRIMARY KEY,
  name VARCHAR (100),
  phones TEXT []
);
```

	1. `phones` - 1-D array that holds phone numbers
7. Multi-dimensional array:

```sql
column_name data_type [][]
```

### Inserting data into an array ###
1. Example: Insert new contact

```sql
INSERT INTO contacts (name, phones) VALUES ('John Doe', ARRAY ['(408)-589-5846', '(408)-589-5555']);
```

	1. Uses `ARRAY` constructor
		1. Constructs an array.
2. Using curly braces (alternative):

```sql
INSERT INTO contacts (name, phones) VALUES ('Lily Bush', '{"(408)-589-5841"}'),
  ('William Gate', '{"(408)-589-5842", "(408)-589-58423"}');
```

	1. `''` must be used to wrap the array with `{}`
	2. `""` must be used to wrap the text items

### Querying array data ###
1. Example:

```sql
SELECT
  name,
  phones
FROM
  contacts;
```

2. To access an array element, we use subscript within `[]`
	1. 1-based numbering is used by default
3. To retrieve the contact's name and first phone number:

```sql
SELECT
  name,
  phones [1]
FROM
  contacts;
```

4. Array element can be used in `WHERE` clause as a condition to filter the rows:
5. Example: Contacts with a particular phone number as the second phone number:

```sql
SELECT
  name,
FROM
  contacts
WHERE
  phones [2] = '(408)-589-58423';
```

### Modifying PostgreSQL array ###
1. We can update each element of an array or the whole array
2. Updating the second phone number of `'William Gate'`

```sql
UPDATE contacts
SET phones [2] = '(408)-589-5843'
WHERE ID = 3
RETURNING *;
```

3. Updating the array as a whole:

```sql
UPDATE contacts
SET phones = ARRAY ['(408)-589-5843']
WHERE ID = 3
RETURNING *;
```

### Searching in PostgreSQL Array ###
1. To know who has a phone number regardless of the position of the phone number in `phones` array, use `ANY` function:

```sql
SELECT
  name,
  phones
FROM
  contacts
WHERE
  '(408)-589-5555' = ANY (phones);
```

### Expanding Arrays ###
1. `unnest` - Function to expand an array to a list of rows.

```sql
SELECT
  name,
  unnest(phones)
FROM
  contacts;
```

### Summary ###
1. An array is a collection of elements with the same data type
2. `data_type []` - to define one-dimensional array for a column
3. `[index]` - used to access the `index` element of an array.
	1. The first element has an index of 1
4. Use `unnest()` to expand an array to a list of rows.

## PostgreSQL hstore ##
1. Summary: PostgreSQL hstore data type
2. hstore module implements hstore data type for storing key-value pairs in a single value
	1. The keys and values are text strings only
3. Use-cases: Semi-structured data or rows with many attributes that are rarely queried

### Enable PostgreSQL hstore extension ###
1. Enable hstore extension
	1. It loads the contrib module to PostgeSQL instance
2. Statement:

```sql
CREATE EXTENSION hstore;
```

### Construct a table with hstore data type ###
1. A table named `books` that has three columns:
	1. `id`: primary key that identifies the book
	2. `title`: Title of the products
	3. `attr`: Stores attributes of the books like ISBN, weight, and paperback.
2. Statement:

```sql
CREATE TABLE books (
  id SERIAL PRIMARY KEY,
  title VARCHAR (255),
  attr hstore
);
```

### Insert data into the PostgreSQL hstore column ###
1. Insert statement:

```sql
INSERT INTO books (title, attr)
VALUES (
  'PostgreSQL Tutorial',
  '
  "publisher" => "postgresqltutorial.com",
  "language" => "English",
  "ISBN-13" => "978-1449370000",
  "weight" => "11.2 ounces"
  '
);
```

	1. Data inserted into hstore column is a `,` separated key-value pairs
	2. Both keys are values are quoted in `"`
2. Second row:

```sql
INSERT INTO books (title, attr)
VALUES (
  'PostgreSQL Cheat Sheet',
  '
  "paperback" => "5",
  "publisher" => "postgresqltutorial.com",
  "language" => "English",
  "ISBN-13" => "978-1449370001",
  "weight" => "1 ounce"
  '
);
```

### Query data from an hstore column ###
1. It is similar to querying data from a column with native data type using the `SELECT` statement.

```sql
SELECT attr FROM books;
```

### Query value for a specific key ###
1. `->` operator
	1. Used to query value of a specific key from an hstore column
	2. Example: Get ISBN-13 of all available books:
	
	```sql
	SELECT
	  attr -> 'ISBN-13' AS isbn
	FROM
	  books;
	```

### Use value in the WHERE clause ###
1. `->` operator can be used in the `WHERE` clause to filter the rows whose values of the hstore column match the input value
2. Example: Retrieve `title` and `weight` of a book that has `ISBN-13` value matching `978-1449370000`;

```sql
SELECT
  title, attr -> 'weight' AS weight
FROM
  books
WHERE
  attr -> 'ISBN-13' = '978-1449370000';
```

### Add key-value pairs to existing rows ###
1. Adding new key-value pair to existing rows

```sql
UPDATE books
SET attr = attr || '"freeshipping" => "yes"' :: hstore;
```

```sql
SELECT
  title,
  attr -> 'freeshipping' AS freeshipping
FROM
  books;
```

### Update existing key-value pair ###
1. Updating an existing key:

```sql
UPDATE books
SET attr = attr || '"freeshipping" => "no"' :: hstore;
```

### Remove existing key-value pair ###
1. Deleting a key-value pair from hstore column:

```sql
UPDATE books
SET attr = delete(attr, 'freeshipping');
```

### Check for a specific key in hstore column ###
1. `?` - operator to check for a specific key in an hstore column in `WHERE` clause.
2. Return all rows with `attr` containing key `publisher`:

```sql
SELECT
  title,
  attr -> 'publsher' as publisher,
  attr
FROM
  books
WHERE
  attr ? 'publisher';
```

### Check for a key-value pair ###
1. `@>` - operator to query based on hstore key-value pair
2. Retrieve all rows whose `attr` column contains a key-value pair that matches `"weight" => "11.2 ounces"`

```sql
SELECT
  title
FROM
  books
WHERE
  attr @> '"weight" => "11.2 ounces"' :: hstore;
```

### Query rows that contain multiple specific keys ###
1. `?&` - Operator to query rows whose hstore column contains multiple keys.
2. Get books where `attr` column contains `language` and `weight` keys.

```sql
SELECT
  title
FROM
  books
WHERE
  attr ?& ARRAY ['language', 'weight'];
```

3. To check if a column contains any key from a list of keys: `?|` (OR operator)

### Get all keys from an hstore column ###
1. `akeys()` **(M)** - function

```sql
SELECT
  akeys (attr)
FROM
  books;
```

### Get all values from an hstore column ###
1. `avals()` - get all values as array

```sql
SELECT
  avals (attr)
FROM
  books;
```

2. `svals()` - get all values as a set

### Convert hstore data to JSON ###
1. `hstore_to_json()` **(M)** - to convert `hstore` data to json

```sql
SELECT
  title,
  hstore_to_json(attr) AS json
FROM
  books;
```

### Convert hstore data to sets ###
1. `each()` - to convert hstore data to sets

```sql
SELECT
  title,
  (each(attr)).*
FROM
  books;
```

	1. `(each(attr)).*` - key and value in separate columns

## PostgreSQL JSON ##
1. Summary: JSON and how to work with JSON in PostgreSQL
	1. Data types:
		1. JSON
		2. JSONB
		
### What is JSON ###
1. JSON - JavaScript Object Notation.
	1. It is a lightweight data-interchange format that is readable for humans and simple for computers to parse
	2. It is based on two main data structures
		1. Objects
		2. Arrays

#### Objects ####
1. Object is an unordered collection of key-value pairs enclosed in curly braces `{}`
2. Each pair includes
	1. A key which is a string surrounded by double quotes (`"`)
	2. A colon `:` that separates the key and value
	3. A value that can be a string, a number, or even an object
3. JSON object that represents a film: `{"title": "Chamber Italian", "release_year", 2006, "length": 117}`
	1. Three keys: `title`, `release_year`, `length`

#### Arrays ####
1. It is an ordered list of values enclosed in square brackets: `[]`
	1. Values do not have to be the same type
	2. It can contain values of any valid JSON data type including objects and arrays
2. Array of film titles:

```json
["Chamber Italian", "Grosse Wonderful", "Airport Pollock"]
```

#### Data types in JSON ####
1. Data types supported
	1. String: "Joe"
	2. Number: 100, 9.99, ...
	3. Boolean: true and false
	4. Null: null
2. Use-cases: Configuration files, exchanging data between a client and a server

### PostgreSQL JSON data types ###
1. Two data types are offered:
	1. JSON - to store an exact copy of the JSON text
	2. JSONB - to store the JSON data in binary format

#### JSON vs. JSONB ####
1. Differences:
	1. JSON
		1. Storage: Textual representation (verbatim)
		2. Size: Typically larger (it retains the whitespace in JSON data)
		3. Indexing: Fully-text search indexes
		4. Performance: Slightly slower
		5. Query performance: SLower due to parsing
		6. Parsing: Parse each time
		7. Data manipulation: Simple and easy
		8. Ordering of keys: Preserved
		9. Duplicate keys: ALlow duplicate keys, the last value is retained
		10. Use cases: Storing configuration data, log data, simple JSON documents
	2. JSONB
		1. Storage: Binary storage format
		2. Size: Typically smaller
		3. Indexing: Binary indexes
		4. Performance: Generally faster
		5. Query performance: Faster due to binary storage
		6. Parsing: Parse once, store in binary format
		7. Data manipulation: More complex
		8. Ordering of keys: Not preserved
		9. Duplicate keys: Do not allow duplicate keys
		10. Use cases: Storing JSON documents where fast querying and indexing are required
2. Use-cases:
	1. JSONB must be used to store JSON data unless we want to retain the ordering of keys in JSON documents

### PostgreSQL JSON examples ###
#### Storing JSON objects example ####
1. Products table:

```sql
CREATE TABLE products (
  id SERIAL PRIMARY KEY,
  name VARCHAR(255) NOT NULL,
  properties JSONB
);
```

	1. `properties` - size, color, etc.
2. Insert JSON data into products table:

```sql
INSERT INTO products (name, properties)
VALUES ('Ink Fusion T-Shirt', '{"color": "white", "size": ["S", "M", "L", "XL"]}')
RETURNING *;
```

3. Insert multiple rows into the `products` table:

```sql
INSERT INTO products (name, properties)
VALUES ('ThreadVerse T-Shirt', '{"color": "black", "size": ["S", "M", "L", "XL"]}'),
  ('Design Dynamo T-Shirt', '{"color": "black", "size": ["S", "M", "L", "XL"]}')
RETURNING *;
```

4. Retrieve JSON data:

```sql
SELECT id, name, properties
FROM products;
```

5. Extract colors from the JSON data:

```sql
SELECT
  id,
  name,
  properties -> 'color' color
FROM
  products;
```

	1. `->` - operator that extracts a JSON object field by a key
		1. The value is surrounded by `""`
6. To extract JSON object field by a key as text:

```sql
SELECT
  id,
  name,
  properties ->> 'color' AS color
FROM
  products;
```

7. Retrieve products with colors black and white using `->>` operator in WHERE clause

```sql
SELECT
  id,
  name,
  properties ->> 'color' color
FROM
  products
WHERE
  properties ->> 'color' IN ('black', 'white');
```

#### Storing JSON arrays example ####
1. `contacts` table:

```sql
CREATE TABLE contacts (
  id SERIAL PRIMARY KEY,
  name VARCHAR (255) NOT NULL,
  phones JSONB
);
```

2. Insert new rows:

```sql
INSERT INTO contacts (name, phones)
VALUES
  ('John Doe', '["408-111-2222", "408-111-2223"]'),
  ('Jane Doe', '["212-111-2222", "212-111-2223"]')
RETURNING *;
```

3. Retrieve the contacts with work phone numbers from `contacts` table:

```sql
SELECT
  name,
  phones ->> 0 "work phone"
FROM
  contacts;
```

	1. `->> index` - Extracts the index element in an array
3. [Check JSON functiosn to process JSON data](https://neon.com/postgresql/postgresql-json-functions)

### Summary ###
1. JSON stands for JavaScript Object Notation
2. Use JSONB data type to store JSON data

## A Look at PostgreSQL User-defined Data Types ##
1. Summary: `CREATE DOMAIN` and `CREATE TYPE` - for user-defined data types
	1. `CREATE DOMAIN` - user-defined data types with constraints `NOT NULL`, `CHECK`, etc.
	2. `CREATE TYPE` - composite type used in stored procedures as the data types of returned values.

### PostgreSQL CREATE DOMAIN statement ###
1. Domain is a data type with optional constraints:
	1. `NOT NULL`
	2. `CHECK`
2. Domain has a unique name within the schema scope
3. Used for centralizing the management of fields within common constraints
	1. Example: Some tables may have the same colun that do not accept NULL and spaces
4. Example: `mailing_list` table:

```sql
CREATE TABLE mailing_list (
  id SERIAL PRIMARY KEY,
  first_name VARCHAR NOT NULL,
  last_name VARCHAR NOT NULL,
  email VARCHAR NOT NULL,
  CHECK (
    first_name !~ '\s'
	AND last_name !~ '\s'
  )
);
```

	1. `first_name` and `last_name` do not accept null and spaces.
5. Alternative: `contact_name` domain, which can be reused in multiple columns

```sql
CREATE DOMAIN contact_name AS
  VARCHAR NOT NULL CHECK (value !~ '\s');
```

```sql
CREATE TABLE mailing_list (
  id SERIAL PRIMARY KEY,
  first_name contact_name,
  last_name contact_name,
  email VARCHAR NOT NULL
);
```

6. Insert a new row:

```sql
INSERT INTO mailing_list (first_name, last_name, email)
VALUES ('Jame V', 'Doe', 'james.doe@example.com');
```

	1. `ERROR:  value for domain contact_name violates check constraint "contact_name_check"`

```sql
INSERT INTO mailing_list (first_name, last_name, email)
VALUES ('Jane', 'Doe', 'james.doe@example.com');
```

7. To change or remove domain: `ALTER DOMAIN`, and `DROP DOMAIN` respectively.
8. To view all domains: `\dD` **M(M)**

#### Getting domain information ####
1. To get all domains in a specific schema:

```sql
SELECT typname
FROM pg_catalog.pg_type
  JOIN pg_catalog.pg_namespace
  ON pg_namespace.oid = pg_type.typnamespace
WHERE
  typtype = 'd' AND nspname = '<schema_name>';
```

3. Example: Return domains in `public` schema of current database:

```sql
SELECT typname
FROM pg_catalog.pg_type
  JOIN pg_catalog.pg_namespace
  ON pg_namespace.oid = pg_type.typnamespace
WHERE
  typtype = 'd' AND nspname = 'public';
```

### PostgreSQL CREATE TYPE ###
1. `CREATE TYPE` allows creation of composite type
	1. Use-case: Return type of a function
2. Scenario: To return several values: `film_id`, `title`, and `release_year` as `film_summary`

```sql
CREATE TYPE film_summary AS (
  film_id INT,
  title VARCHAR,
  release_year SMALLINT
);
```

3. Returning `film_summary` data type as a return type of a function:

```sql
CREATE OR REPLACE FUNCTION get_film_summary (f_in INT)
  RETURNS film_summary AS
$$
SELECT
  film_id,
  title,
  release_year
FROM
  film 
WHERE
  film_id = f_id;
$$
LANGUAGE SQL;
```

4. Call `get_film_summary()` function:

```sql
SELECT * FROM get_film_summary (40);
```

5. To change a user-defined type: `ALTER TYPE`
6. To remove a user-defined type: `DROP TYPE`
7. To list all types:

```psql
\dT
\dT+
```

## PostgreSQL enum ##
1. Summary: Enum data type is used to define a list of fixed values for a column.

### Introduction to the PostgreSQL enum data type ###
1. Enum type is a custom data type that allows you to define a list of possible values for a column.

```sql
CREATE TYPE enum_name
AS
ENUM ('value1', 'value2', 'value3', ...);
```

	1. Specify name after `CREATE TYPE`
	2. Provide a comma-separated enum values after `ENUM` keyword
	3. If we declare a column with the enum_type, it can only accept fixed values declared in the enum
2. `column_name enum_type`
	1. If you try to insert a row with a value not in the list, PostgreSQL will issue an error
	2. The order of values in a enum is the order in which you list them when you define the enum
	3. We can use comparison operators (>, >=, <, <=, =, <>) and aggregation functions with enum values

### PostgreSQL enum data type example ###
1. New enum type: `prority` with values `low`, `medium`, and `high`.

```sql
CREATE TYPE priority
AS
ENUM ('low', 'medium', 'high');
```

2. Table `requests` with a column using `priority` enum:

```sql
CREATE TABLE requests (
  id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
  title VARCHAR (255) NOT NULL,
  priority PRIORITY NOT NULL,
  request_date DATE NOT NULL
);
```

3. Insert some rows:

```sql
INSERT INTO requests (title, priority, request_date)
VALUES
  ('Construct an enum tutorial in PostgreSQL', 'high', '2019-01-01'),
  ('Review the enum tutorial', 'medium', '2019-01-01'),
  ('Publish the PostgreSQL enum tutorial', 'low', '209-01-01')
RETURNING *;
```

4. Sort requests by priority from 'low' to 'high':

```sql
SELECT *
FROM requests
ORDER BY priority;
```

5. Find requests whose priority is higher than `low`:

```sql
SELECT *
FROM requests
WHERE priority > 'low'
ORDER BY priority;
```

6. Find requests whose priority is 'high':

```sql
SELECT *
FROM requests
WHERE priority = 'high'
ORDER BY priority;
```

7. Attempt to insert an invalid value:

```sql
INSERT INTO requests (title, priority, request_date)
VALUES
  ('Revise the enum tutorial', 'urgent', '2019-01-02')
RETURNING *;
```

### Adding new values to enums ###
1. Use: `ALTER TYPE ... ADD VALUE` **(M)**

```sql
ALTER TYPE enum_name
ADD VALUE [IF NOT EXISTS] 'new_value'
[{BEFORE|AFTER} 'existing_enum_value'];
```

	1. Specify the name of the enum after `ALTER TYPE`
	2. Specify a new value after `ADD VALUE`
		1. `IF NOT EXISTS` - to conditionally add a value if it does not exist
	3. Specify the position of the new value relative to an existing value
		1. The statement adds the new enum value at the end of the list by default.
2. Example:

```sql
ALTER TYPE priority
ADD VALUE IF NOT EXISTS 'urgent';
```

### Retrieving a list of enum values ###
1. `enum_range(null::enum_name)`
	1. Returns as an array
2. Example:

```sql
SELECT enum_range(null::priority);
```

### Getting the first and last values in an enum ###
1. Use `enum_first()` and `enum_last()`
2. Example:

```sql
SELECT
  enum_first(NULL::priority) first_value,
  enum_last(NULL::priority) last_value;
```

### Renaming an enum value ###
1. Use `ALTER TABLE ... RENAME VALUE` **(M)**

```sql
ALTER TYPE enum_name
RENAME VALUE existing_enum_value TO new_enum_value;
```

2. Example: Change `urgent` to `very high`

```sql
ALTER TYPE priority
RENAME VALUE 'urgent' TO 'very high';
```

	1. If a value has space, PostgreSQL uses `""`

### When to use enums ###
1. enums are similar to foreign keys
	1. Both allow us to define a set of values for a column
2. Advantages of using enums:
	1. Performance: We can use a single table instead of using join to retrieve data from two tables
	2. Simplicity: SQL statement is simpler for enums
3. Disadvantages of using enums:
	1. Limited flexibility: Changing enum values requires changing db schema instead of adding values to the lookup table.
	2. Portability: Some database systems do not support enum
		1. If we try to migrate PostgreSQL database schema to a database system that does not support enum, we'll have an issue.
4. Use-cases:
	1. If we have a fixed set of values that are unlikely to change
		1. Example: RCB colors (red, green, blue).

### Summary ###
1. Enum is used to define fixed values for a table column
2. `CREATE TYPE` to define new enum data type
3. Order of values is the order in which we have declared them when defining enum type
4. `ALTER TYPE ... ADD VALUE` - new value to an enum
5. `ALTER TYPE ... RENAME VALUE` - rename an enum value
6. Use enum if you have a small list of fixed values
	1. Otherwise use lookup table with foreign keys

## PostgreSQL XML Data Type ##
1. Summary: PostgreSQL XML data type is used to store XML documents in the database.

### Introduction to the PostgreSQL XML data type ###
1. Syntax:

```sql
column_name XML
```

	1. Benefits:
		1. Type Safety: PostgreSQL can validate when inserting/updating data, to ensure that XML confirms to XML standards
		2. Built-in XML functions and operators: PostgreSQL supports many XML functions and operators to manipulate XML data effectively.

### PostgreSQL XML data type example ###
1. New table: `person`

```sql
CREATE TABLE person (
  id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
  info XML
);
```

	1. `id` - identity column that serves as primary key column of the table
	2. `info` - stores XML data
2. Insert a row in `perosn` table:

```sql
INSERT INTO person (info)
VALUES (
  XMLPARSE(DOCUMENT '<?xml version="1.0" encoding="UTF-8"?>
	<person>
	  <name>John Doe</name>
	  <age>35</age>
	  <city>San Francisco</city>
	</person>')
);
```

	1. `DOCUMENT` - Indicates that the input string is a complete XML document starting with XML declaration
	2. `XMLPARSE` - Function that converts string into an XML document
3. To insert multiple rows

```sql
INSERT INTO person (info)
VALUES
(
    XMLPARSE(DOCUMENT '<?xml version="1.0" encoding="UTF-8"?>
    <person>
        <name>Jane Doe</name>
        <age>30</age>
        <city>San Francisco</city>
    </person>')
),
(
    XMLPARSE(DOCUMENT '<?xml version="1.0" encoding="UTF-8"?>
    <person>
        <name>John Smith</name>
        <age>40</age>
        <city>New York</city>
    </person>')
),
(
    XMLPARSE(DOCUMENT '<?xml version="1.0" encoding="UTF-8"?>
    <person>
        <name>Alice Johnson</name>
        <age>30</age>
        <city>Los Angeles</city>
    </person>')
);
```

4. Retrieve names of persons from XML document:

```sql
SELECT xpath('/person/name/text()', info) AS name
FROM person;
```

	1. Each row is an array of XML values representing person names.
		1. Each array has only one element in this case.
5. Retrieve name as text:

```sql
SELECT (xpath('/person/name/text()', info))[1]::text AS name
FROM person;
```

	1. First XPath `/person/name/text()` returns text of name node of the XML document.
		1. It returns an array that includes all matching values
	2. `[1]` - returns the first element of the array
	3. `::text` - casts the XML value to text
6. Retrieve ages of persons:

```sql
SELECT (xpath('/person/age/text()', info))[1]::text::integer AS age
FROM person;
```

	1. We cannot caste XML directly to integer
7. Retrieve name, age, and city:

```sql
SELECT
  (xpath('/person/name/text()', info))[1]::text AS name,
  (xpath('/person/age/text()', info))[1]::text::integer AS age,
  (xpath('/person/city/text()', info))[1]::text AS city 
FROM
  person;
```

8. Find a person with the name 'Jane Doe':

```sql
SELECT *
FROM person
WHERE (xpath('/person/name/text()', info))[1]::text = 'Jane Doe';
```

### Constructing Indexes for XML data ###
1. If the `person` table has many rows, finding the person by name will be slow.
	1. Solution: An expression index for the XML documents to improve the query performance
2. Index expression that extracts the name of a person as an array of text:

```sql
CREATE INDEX person_name
ON person USING BTREE
  (cast(xpath('/person/name', info) AS TEXT[]));
```

3. Inserting 1000 rows for testing:

```sql
CREATE OR REPLACE FUNCTION generate_persons()
RETURNS void
AS
$$
BEGIN
  INSERT INTO person (info)
  SELECT
    XMLPARSE(DOCUMENT '<?xml version="1.0" encoding="UTF-8"?>
	  <person>
	    <name>' || 'Person' || generate_series || '</name>
        <age>' || (generate_series % 80 + 18) || '</age>
        <city>' || CASE WHEN generate_series % 3 = 0 THEN 'New York'
                        WHEN generate_series % 3 = 1 THEN 'Los Angeles'
                        ELSE 'San Francisco' END || '</city>
	  </person>')
  FROM generate_series(1, 1000);
END;
$$
LANGUAGE plpgsql;
```

4. Call `generate_persons()` to insert 1000 rows into the `person` table:

```sql
SELECT generate_persons();
```

5. Find a person with the name `Jane Doe`:

```sql
EXPLAIN ANALYZE
SELECT *
FROM person
WHERE cast(xpath('/person/name', info) AS TEXT[]) = '{<name>Jane Doe</name>}';
```

	1. Query utilizes the index expression of the `person` table

### Summary ###
1. `XML` data type - to store XML documents in DB.
2. `xpath()` - function to retrieve a value from XML documents.

## PostgreSQL BYTEA Data Type ##
1. Summary: How to store binary strings in the database.

### Introduction to the PostgreSQL BYTEA data type ###
1. `BYTEA` - can be used to store binary strings or byte sequences
	1. Binary array
2. Definition:

```sql
column_name BYTEA
```

	1. Max size: 1 GB
		1. But storing large amount of binary data in a `BYTEA` column is not efficient
			1. Solution: If files are larger than a few MB, store them externally and save paths to the files in db.
3. Examples:
	1. [Storing files in a BYTEA column using PHP.](https://neon.com/postgresql/postgresql-php/postgresql-blob)
	2. [Storing images in a BYTEA column using Python.](https://neon.com/postgresql/postgresql-python/blob)

### PostgreSQL BYTEA data type example ###
1. Table to store binary strings:

```sql
CREATE TABLE binary_data (
  id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
  data BYTEA
);
```

2. Insert a binary string:

```sql
INSERT INTO binary_data (data)
VALUES ('\x012345');
```

3. Retrieve data from the column:

```sql
SELECT * FROM binary_data;
```

### Summary ###
1. Use-case: To store small binary data in database

## PostgreSQL Composite Types ##
1. Summary: Allows us to define custom data types with multiple fields.
	1. Fields can be built-in or user-defined types (including other composite types)

### Defining PostgreSQL Composite Types ###
1. Use `CREATE TYPE` and a list of fields:

```sql
CREATE TYPE type_name AS (
  field1 data_type1,
  field2 data_type2,
  ...
);
```

2. Example:

```sql
CREATE TYPE address_type AS (
  street TEXT,
  city TEXT,
  state TEXT,
  zip_code INTEGER,
  country TEXT
);
```

3. Use it as a data type of a table column:

```sql
CREATE TABLE contacts (
  id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
  name VARCHAR (255) NOT NULL,
  address address_type
);
```

	1. When a table is created, PostgreSQL constructs an implicit composite type. Example, `contacts`

### Inserting values into a composite column ###
1. `ROW` - used to construct a composite value:

```sql
ROW (value1, value2, ...)
```

2. `ROW` is optional:

```sql
(value1, value2, ...)
```

3. `NULL`:

```sql
(value1, NULL, value3, ...)
```

4, `NULL` can be omitted:

```sql
(value1,, value3, ...)
```

5. Example:

```sql
INSERT INTO contacts (name, address)
VALUES (
  'John Smith',
  ROW ('123 St', 'Houston', 'TX', 77001, 'USA')
);
```

6. To insert values into individual fields in the in the address column:

```sql
INSERT INTO contacts (
  name,
  address.street,
  address.city,
  address.state,
  address.zip_code
)
VALUES
  ('Jane Doe', '4000 N. 1st Street', 'San Jose', 'CA', 95134);
```

	1. `column_name.field_name`

### Querying composite values ###
1. Retrieving all rows from `contacts` table:

```sql
SELECT * FROM contacts;
```

2. To query individual fields of a composite type, use the following syntax:

```sql
(column_name).field_name
```

3. Example:

```sql
SELECT
  id,
  name,
  (address).city,
  (address).state,
  (address).zip_code
FROM
  contacts;
```

4. To get all fields from a composite value:

```sql
SELECT
  id,
  name,
  (address).*
FROM 
  contacts;
```

### Updating composite values ###
1. To update the country of the contact id 2 to `USA`

```sql
UPDATE contacts
SET
  address.country = 'USA'
WHERE
  id = 2
RETURNING *;
```

	1. No parantheses around the column name.

### Summary ###
1. Custom data types with multiple fields.

## How to Compare Two Tables in PostgreSQL ##
Summary: Various ways to compare two tables in PostgreSQL. Two commonly used techniques to compare the data.

### Comparing two tables using EXCEPT and UNION operators ###
1. Tables `foo` and `bar`. Insert sample data.

```sql
CREATE TABLE foo (
  id INT PRIMARY KEY,
  name VARCHAR (50)
);

CREATE TABLE bar (
  id INT PRIMARY KEY,
  name VARCHAR (50)
);

INSERT INTO foo (id, name)
VALUES
  (1, 'a'),
  (2, 'b');
  
INSERT INTO bar (id, name)
VALUES
  (1, 'a'),
  (2, 'b');
```

2. Update one row in the `bar` table:

```sql
UPDATE
  bar
SET
  name = 'c'
WHERE
  id = 2;
```

3. Find out rows in the `foo` table but not in the `bar` table:

```sql
SELECT
  id,
  name,
  'not in bar' AS note
FROM
  foo
EXCEPT
SELECT
  id,
  name,
  'not in bar' AS note
FROM
  bar;
```

4. `UNION` operator to combine results of both queries (finding rows in `foo` that are not in `bar` and vice versa):

```sql
SELECT
  id,
  name,
  'not in bar' AS note
FROM
  foo
EXCEPT
SELECT
  id,
  name,
  'not in bar' AS note
FROM
  bar
UNION
SELECT
  id,
  name,
  'not in foo' AS note
FROM
  bar
EXCEPT
SELECT
  id,
  name,
  'not in foo' AS note
FROM
  foo;
```

### Comparing two tables using an outer join ###
1. Example:

```sql
SELECT
  id,
  name
FROM
  foo FULL
  OUTER JOIN bar USING (id, name)
WHERE
  foo.id IS NULL
  OR bar.id IS NULL;
```

2. Find number of rows in `foo` table that are not in the `bar` table.

```sql
SELECT
  count (*)
FROM
  foo FULL
  OUTER JOIN bar USING (id, name)
WHERE
  foo.id IS NULL
  OR bar.id IS NULL;  
```

### Summary ###

## How to Generate a Random Number in a Range ##
1. Summary: How to develop a user-defined function that generates a random number between two numbers.
2. `random()` - function that returns number between 0 and 1.

```sql
SELECT random();
```

3. Generate a number between 1 and 11:

```sql
SELECT random() * 10 + 1 AS RAND_11;
```

4. Generate a random number as an integer:

```sql
SELECT floor(random() * 10 + 1)::int;
```

5. Generate a random number as an integer between `low` and `high`:

```sql
SELECT floor(random() * (high - low + 1) + low)::int;
```

6. Define a user-defined function to return a random number between two numbers `low` and `high`:

```sql
CREATE OR REPLACE FUNCTION random_between(low INT, high INT)
RETURNS INT AS
$$
BEGIN
RETURN floor(random() * (high - low + 1) + low)::int;
END;
$$
LANGUAGE 'plpgsql' STRICT;
```

7. Call the function `random_between()` to generate a random number between 1 and 100:

```sql
SELECT random_between(1, 100);
```

8. Generate multiple random numbers between two integers:

```sql
SELECT random_between(1, 100)
FROM generate_series(1, 5);
```

## How to Delete Duplicate Rows in PostgreSQL ##
1. Summary: Techniques to delete duplicate rows.

### Preparing sample data ###
1. New table: `basket`

```sql
CREATE TABLE basket (
  id SERIAL PRIMARY KEY,
  fruit VARCHAR (50) NOT NULL
);
```

2. Insert some fruits:

```sql
INSERT INTO basket (fruit)
VALUES
  ('apple'),
  ('apple'),
  ('orange'),
  ('orange'),
  ('orange'),
  ('banana');
```

3. Query data:

```sql
SELECT 
  id,
  fruit
FROM
  basket;
```

### Finding duplicate rows ###

```sql
SELECT
  fruit,
  COUNT (fruit)
FROM
  basket
GROUP BY
  fruit
HAVING
  COUNT (fruit) > 1
ORDER BY
  fruit;
```

### Deleting duplicate rows using DELETE USING statement ###
1. `DELETE USING`

```sql
DELETE FROM
  basket a
  USING basket b
WHERE
  a.id < b.id
  AND
  a.fruit = b.fruit;
```

2. Verify:

```sql
SELECT
  id,
  fruit
FROM
  basket;
```

3. Flip the sign to delete duplicates with higher ids

### Deleting duplicate rows using subquery ###
1. Example:

```sql
DELETE FROM basket
WHERE id IN
  (
    SELECT id
	FROM
	  (
	    SELECT 
		  id,
		  ROW_NUMBER() OVER(PARTITION BY fruit ORDER BY id) AS row_num
		FROM
		  basket
	  ) t
	  WHERE t.row_num > 1
  );
```

2. Template to delete duplicates based on values of multiple columns:

```sql
DELETE FROM table_name
WHERE id IN
  (
    SELECT
	  id
	FROM
      ( 
	    SELECT 
	      id,
	      ROW_NUMBER() OVER(PARTITION BY column_1, column 2 ORDER BY id) AS row_num
	    FROM
	      table_name
      ) t
	WHERE
	  t.row_num > 1
  );
```

### Deleting duplicate rows using an immediate table ###
1. Steps:
	1. A new table with the same structure as the one whose duplicate rows should be removed.
	2. Insert distinct rows from the source table to the immediate table.
	3. Drop the source table.
	4. Rename the immediate table to the name of the source table.
2. Illustration:

```
-- step 1
CREATE TABLE basket_temp (LIKE basket);

-- step 2
INSERT INTO basket_temp (fruit, id)
SELECT
  DISTINCT ON (fruit) fruit,
  id
FROM basket;

-- step 3
DROP table basket;

-- step 4
ALTER TABLE basket_temp
RENAME TO basket;
```

## PostgreSQL CASE ##
1. Summary: Using PostgreSQL CASE conditional expression for conditional queries
2. `CASE` is the same as `IF/ELSE` in programming languages.
	1. `IF/ELSE` logic to query to form a powerful query
3. `CASE` is an expression
	1. It can be used in any place where we would use `SELECT`, `WHERE`, `GROUP BY`, and `HAVING` clauses.
4. `CASE` expression has two forms
	1. General
	2. Simple

### General PostgreSQL CASE expression ###
1. General form:

```sql
CASE
  WHEN concition_1 THEN result_1
  WHEN condition_2 THEN result_2
  [WHEN ...]
  [ELSE else_result]
END
```

	1. `condition_1`, `condition_2`, etc are boolean expressions that return either `true` or `false`
		1. When a `condition_i` evaluates to `false`, the next condition from top is evaluated, until we find a condition that evaluates to `true`
		2. If a condition evaluates to true, the `CASE` expression returns the corresponding result that follows the condition
			1. It immediately stops evaluating the remaining expressions
		3. If all conditions are false, `CASE` expression returns the result `else_result` that follows the `ELSE` keyword
		4. If you ommit the `ELSE` clause, the `CASE` expression returns `NULL`

#### The general CASE example ####
1. Example: `film` table
	1. To label the films by their lengths based on the following logic:
		1. If the length is less than 50 minutes, the film is short
		2. If the length is greater than 50 minutes and less than or equal to 120 minutes, the film is medium
		3. If the length is greater than 120 minutes, the film is long
	2. Implementation:
	
	```sql
	SELECT
	  title,
	  length,
	  CASE
	    WHEN length <= 50 THEN 'Short"
		WHEN length <= 120 THEN 'Medium'
		WHEN length > 120 THEN 'Long'
	  END duration
	FROM
	  film
	ORDER BY
	  title;
	```

#### Using CASE with an aggregate function example ####
1. To assign price segments to films with the following logic:
	1. If the rental rate is 0.99, the film is economic
	2. If the reantal rate is 1.99, the film is mass
	3. If the rental rate is 4.99, the film is premium
2. We want to know the number of films that belong to economy, mass, and premium
3. Solution:

```sql
SELECT
  SUM (
    CASE WHEN rental_rate = 0.99 THEN 1 ELSE 0 END
  ) AS "Economy",
  SUM (
    CASE WHEN rental_rate = 2.99 THEN 1 ELSE 0 END
  ) AS "Mass",
  SUM (
    CASE WHEN rental_rate = 4.99 THEN 1 ELSE 0 END
  ) AS "Premium"
FROM
  film;
```

### Simple PostgreSQL CASE expression ###
1. Simple form:

```sql
CASE expression
  WHEN value_1 THEN result_1
  WHEN value_2 THEN result_2
  [WHEN ...]
ELSE 
  else_result
END
```

	1. `CASE` first evaluates the expression and compares the result with each value (`value_1`, `value_2`, ...) in the `WHEN` clauses sequentially until it finds the match.
	2. If `CASE` does not find any matches, it returns `else_result` that follows the `ELSE` or `NULL` value if `ELSE` is not available

#### Simple PostgreSQL CASE expression example ####
1. Adding rating description to the output:

```sql
SELECT
  title,
  rating,
  CASE rating
    WHEN 'G' THEN 'General Audiences'
	WHEN 'PG' THEN 'Parental Guidance Suggested'
	WHEN 'PG-13' THEN 'Parents Strongly Cautioned'
	WHEN 'R' THEN 'Restricted'
	WHEN 'NC-17' THEN 'Adults Only'
  END rating_description
FROM
  film
ORDER BY
  title;
```

#### Using simple PostgreSQL CASE expression with aggregate function example ####
1. Calculating the number of films with each rating

```sql
SELECT
  SUM(
    CASE rating
	  WHEN 'G' THEN 1
	  ELSE 0
	END
  ) "General Audience",
  SUM(
    CASE rating
	  WHEN 'PG' THEN 1
	  ELSE 0
	END
  ) "Parental Guidance Suggested",
  SUM(
    CASE rating
	  WHEN 'PG-13' THEN 1
	  ELSE 0
	END
  ) "Parental Strongly Cautioned",
  SUM(
    CASE rating
	  WHEN 'R' THEN 1
	  ELSE 0
	END
  ) "Restricted",
    SUM(
    CASE rating
	  WHEN 'NC-17' THEN 1
	  ELSE 0
	END
  ) "Adults Only"
FROM
  film;
```

## PostgreSQL COALESCE ##
1. Summary: `COALESCE()` function that returns a non-null argument.

### PostgreSQL COALESCE function syntax ###
1. `COALESCE()` function accepts a list of arguments and returns the first non-null argument.
2. Basic syntax:

```sql
COALESCE (argument_1, argument_2, ...);
```

	1. If all arguments are `null`, then it returns `null`
	2. It evaluates from left to right
	3. It is the same as `NVL` (Oracle) or `IFNULL` (MySQL) provided by SQL standard

### PostgreSQL COALESCE function examples ###
#### Basic PostgreSQL COALESCE() function examples ####
1. Example:

```sql
SELECT COALESCE (1, 2);
SELECT COALESCE (NULL, 2, 1);
```

2. Use-case: To substitube a default value for null when querying data from nullable columns.
	1. Example: To display excerpt from a blog post but excerpt is not provided, then use the first 150 chars of the content
	
	```sql
	SELECT
	  COALESCE (
	    excerpt,
		LEFT(content, 150)
	  )
	FROM
	  posts;
	```

#### Using the COALESCE() function with table data ####
1. Example: Items table

```sql
CREATE TABLE items (
  id SERIAL PRIMARY KEY,
  product VARCHAR (100) NOT NULL,
  price NUMERIC NOT NULL,
  discount NUMERIC
);
```

	1. `items` table has four columns:
		1. `id`: Primary key that identifies the item in the `items` table
		2. `product`: the product name
		3. `price`: the price of the product
		4. `discount`: discount on the product
2. Insert rows:

```sql
INSERT INTO items (product, price, discount)
VALUES
  ('A', 1000, 10),
  ('B', 1500, 20),
  ('C', 800, 5),
  ('D', 500, NULL);
```

3. Retrieve the net prices of the products from the `items` table:

```sql
SELECT
  product,
  (price - discount) as net_price
FROM
  items;
```

	1. net price of `D` is null because the discount is null
	2. Solution:
	
	```sql
	SELECT
	  product,
	  (price - COALESCE(discount, 0)) AS net_price
	FROM
	  items;
	```
	
	3. Solution: Using `CASE` expression
	
	```sql
	SELECT
	  product,
	  (price - CASE WHEN discount IS NULL THEN 0 ELSE discount END) AS net_price
	FROM
	  items;
	```
	
	4. In terms of performance, `COELESCE` and `CASE` are the same.
	5. `COELESCE` makes the query shorter and easier to read.

### Summary ###
1. Use `COELESCE` function to substitute null values in the query.

## PostgreSQL ISNULL ##
1. `ISNULL` - SQL Server supports it
	1. It is a function that replaces `NULL` with a specified replacement value.
	
	```sql
	ISNULL(expression, replacement)
	```
	
		1. If `expression` is `null`, `replacement` is returned else, `expression` is returned.
2. PostgreSQL does not have `ISNULL`
	1. Alternative: `COELESCE` function
	
	```sql
	COELESCE(expression, replacement)
	```
	
3. Alternative: Case expression

```sql
SELECT
  CASE
    WHEN expression IS NULL THEN replacement
	ELSE expression
  END AS column_alias;
```

## PostgreSQL NULLIF ##
1. Summary: `NULLIF` to handle `null` values

### Introduction to PostgreSQL NULLIF function ###
1. A common conditional expression
2. Syntax:

```sql
NULLIF(argument_1, argument_2);
```

	1. If `argument_1` is equal to `argument_2`, `NULLIF` returns `NULL`
	2. Otherwise, `NULLIF` returns `argument_1`

### PostgreSQL NULLIF function examples ###
#### Basic PostgreSQL NULLIF examples ####
1. Illustration:

```sql
SELECT NULLIF (1, 1); -- returns NULL
```

2. Returning first argument if two arguments are not equal

```sql
SELECT NULLIF (1, 0); -- returns 1
```

3. With text arguments:

```sql
SELECT NULLIF ('A', 'B');
```

#### Using the NULLIF function with table data ####
1. `posts` table:

```sql 
CREATE TABLE posts (
  id SERIAL PRIMARY KEY,
  title VARCHAR (255) NOT NULL,
  excerpt VARCHAR (150),
  body TEXT,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP
);
```

2. Insert data:

```sql
INSERT INTO posts (title, excerpt, body)
VALUES
  ('test post 1','test post excerpt 1','test post body 1'),
  ('test post 2','','test post body 2'),
  ('test post 3', null ,'test post body 3')
RETURNING *;
```

3. Retrieving data for displaying them on the post overview page that includes the title and excerpt of each post.
	1. Use first 40 characters of the post body as the excerpt.
	2. Use `COALESCE` function to handle `NULL` in the body column:
	
	```sql
	SELECT
	  id,
	  title,
	  COALESCE(
	    excerpt,
		LEFT(body, 40)
	  )
	FROM
	  posts;
	```

	1. There is a mix between null value and '' (empty) in the excerpt column. Use `NULLIF` to address the issue.
	
	```sql
	SELECT
	  id,
	  title,
	  COALESCE(
	    NULLIF(excerpt, ''),
		LEFT(body, 40)
	  )
	FROM
	  posts;
	```
	
		1. If the `excerpt` is empty, it returns `null` otherwise the `excerpt`

### Using NULLIF() function to prevent division-by-zero ###
1. New table: `memebers`

```sql
CREATE TABLE members (
  id serial PRIMARY KEY,
  first_name VARCHAR (50) NOT NULL,
  last_name VARCHAR (50) NOT NULL,
  gender SMALLINT NOT NULL -- 1: male, 2 female
);
```

2. Insert rows:

```sql
INSERT INTO members (first_name, last_name, gender)
VALUES
  ('John', 'Doe', 1),
  ('David', 'Dave', 1),
  ('Bush', 'Lily', 2)
RETURNING *;
```

3. Calculate the ratio between male and female members:

```sql
SELECT
  SUM (
    CASE
	  WHEN gender = 1 THEN 1 
	  ELSE 0
	END
  )
  /
  SUM (
    CASE
	  WHEN gender = 2 THEN 1
	  ELSE 0
	END
  )
  * 100 AS "Male/Female ratio"
FROM
  members;
```

4. Delete all female members:

```sql
DELETE FROM memebers
WHERE gender = 2;
```

	1. `ERROR: division by zero`
5. Use `NULLIF` to prevent division by zero:

```sql
SELECT
  (
    SUM (
	  CASE
	    WHEN gender = 1 THEN 1
		ELSE 0
	  END
	)
	/
	NULLIF (
	  SUM (
	    CASE
		  WHEN gender = 2 THEN 1
		  ELSE 0
		END
	  ),
	  0
	)
  ) * 100 AS "Male/Female ratio"
FROM
  members;
```

	1. Anything divided by `NULL` is `NULL`

### Summary ###
1. `NULLIF` is used to substitute `NULL` and prvent division by zero.

## PostgreSQL CAST: Convert a value of One Type to Another ##
1. Summary: `CAST()` function and operator `::` to convert a value of one type to another.

### Introduction to PostgreSQL CAST() function and cast operator (::) ###
1. `CAST()` function and `::` are available.

### PostgreSQL CAST() function ###
1. Syntax:

```sql
CAST(value AS target_type);
```

	1. `value` can be a
		1. Constant
		2. Table column
		3. Expression
	2. `target_type` - target data type to convert to
2. `CAST` returns a value after it has been cast to the specified data type.
	1. It it cannot be cast, an error message is returned.

### PostgreSQL cast operator (::) ###
1. `::` operator is used to convert a value from one type to another.
2. Syntax:

```sql
value::target_type
```

	1. `::` returns a value after casting the `value` to the `target_type` or raise an error if the cast fails.
	2. It is PostgreSQL specific and does not confirm to the SQL standard.

### PostgreSQL CAST() function and cast operator (::) examples ###
#### Cast a string to an integer example ####
1. To convert a string to an integer:

```sql
SELECT CAST('23' AS INTEGER);
```

2. If it cannot be converted, PostgreSQL will raise an error:

```sql
SELECT CAST('10c' AS INTEGER);
```

#### Cast a string to a date example ####
1. Example:

```sql
SELECT
  CAST ('2026-01-01' AS DATE),
  CAST ('01-OCT-2025' AS DATE);
```

#### Cast a string to a double example ####
1. Example: Cast '10.2' to double:

```sql
SELECT CAST ('10.2' AS DOUBLE);
```

	1. Throws an error.
		1. Fix: Use `DOUBLE PRECISION`
2. Example:

```sql
SELECT CAST ('10.2' AS DOUBLE PRECISION);
```

#### Cast a string to a boolean example ####
1. Example:

```sql
SELECT
  CAST ('true' AS BOOLEAN),
  CAST ('false' AS BOOLEAN),
  CAST ('T' AS BOOLEAN),
  CAST ('F' AS BOOLEAN);
```

#### Cast a string to a timestamp example ####
1. Using `::`

```sql
SELECT '2019-06-15 14:30:20'::TIMESTAMP;
```

#### Cast a string to an interval example ####
1. Using `::`

```sql
SELECT
  '15 minute'::INTERVAL,
  '2 hour'::INTERVAL,
  '1 day'::INTERVAL,
  '2 week'::INTERVAL,
  '3 month'::INTERVAL;
```

#### Cast a timestamp to a date example ####
1. Using `CAST()`:

```sql
SELECT CAST('2019-06-15 14:30:20'::TIMESTAMP AS DATE);
```

#### Cast an interval to text ####
1. Using `CAST()`:

```sql
SELECT CAST('30 days'::INTERVAL AS TEXT);
```

#### Cast a JSON to a JSONB ####
1. Using `CAST()`:

```sql
SELECT CAST('{"name": "John"}'::JSON AS JSONB);
```

#### Cast a double precision to an integer ####
1. Using `CAST()`:

```sql
SELECT CAST(9.99 AS INTEGER);
```

```sql
SELECT 9.99::INTEGER;
```

#### Cast an array to a text ####
1. Using `CAST()`:

```sql
SELECT CAST(ARRAY [1, 2, 3] AS TEXT);
```

#### Cast text to an array ####
1. Using `::`:

```sql
SELECT '{1, 2, 3}'::INTEGER[] AS result_array;
```

#### Using CAST with table data example ####
1. `ratings` table:

```sql
CREATE TABLE ratings (
  id SERIAL PRIMARY KEY,
  rating VARCHAR (1) NOT NULL
);
```

2. Insert some data:

```sql
INSERT INTO ratings (rating)
VALUES
  ('A'),
  ('B'),
  ('C');
```

3. We need to change `ratings` table to store ratings as numbers 1, 2, and 3

```sql
INSERT INTO ratings (rating)
VALUES
  (1), 
  (2),
  (3);
```

4. Show:

```sql
SELECT * FROM ratings;
```

5. Convert all values into integers or make them 0 if they are not integers

```sql
SELECT
  id,
  CASE WHEN rating~E'^\\d+$' THEN rating::INTEGER ELSE 0 END as rating
FROM
  ratings;
```

	1. `E` - escape string

## PostgreSQL EXPLAIN ##
1. Summary: `EXPLAIN` is used to display the execution plan of a statement.

### Introduction to PostgreSQL EXPLAIN statement ###
1. `EXPLAIN` returns the execution plan which PostgreSQL planner generates for a given statement.
2. `EXPLAIN` shows how tables involved in a statement will be scanned by index scan or sequential scan, etc.
	1. If multiple tables are used, what kind of join algorithm will be used.
3. Most important statement returns start-cost before the first row can be returned and the total cost to return the complete result set.
4. Syntax:

```sql
EXPLAIN [ ( option [, ...] ) ] sql_statement;
```

	1. `option` can be:
		1. `ANALYZE [ boolean ]`
		2. `VERBOSE [ boolean ]`
		3. `COSTS [ boolean ]`
		4. `BUFFERS [ boolean ]`
		5. `TIMING [ boolean ]`
		6. `SUMMARY [ boolean ]`
		7. `FORMAT { TEXT | XML | JSON | YAML }`
	2. `boolean` - specifies whether the option should be turned on or off.
		1. `TRUE`, `ON`, `1` can be used to enable the option
		2. `FALSE`, `OFF`, `0` can be used to disable the option
	3. If we omit the boolean, `ON` will be used

#### ANALYZE ####
1. `ANALYZE` causes `sql_statement` to be executed first and then run-time statistics in the returned info including 
	1. Total elapsed time expended within each plan node.
	2. The number of rows it returned.
2. It executes the SQL statement and discards the output info
	1. To analyze `INSERT`, `UPDATE`, and `DELETE` without affecting the data:
		1. Wrap the `EXPLAIN ANALYZE` in a transaction as follows:

		```sql
		BEGING;
		  EXPLAIN ANALYZE sql_statement;
		ROLLBACK;
		```

#### VERBOSE ####
1. `VERBOSE` - allows us to show additional info about the plan.
	1. `FALSE` by default

#### COSTS ####
1. Estimated startup and total costs of each plan node & estimated number of rows & estimated width of each row in the query plan
	1. `TRUE` by default

#### BUFFERS ####
1. Buffer usage information
	1. Used only when `ANALYZE` is enabled
	2. `FALSE` by default

#### TIMING ####
1. Actual startup time and time spend in each node in the output.
	1.`TRUE` by default
	2. Used only when `ANALYZE` is enabled

#### SUMMARY ####
1. Adds summary info such as total timing after the query plan
	1. Included by default when `ANALYZE` option is enabled.

#### FORMAT ####
1. Output format of the query plan:
	1. `TEXT` - default
	2. `XML`
	3. `JSON`
	4. `YAML`

### PostgreSQL EXPLAIN examples ###
1. Example:

```sql
EXPLAIN SELECT * FROM film;
```

```sql
EXPLAIN SELECT * FROM film WHERE film_id = 100;
```

	1. `film_id` is indexed
		1. The planner used index scan instead of sequential scan on the `film` table
	2. To suppress the cost:
	
	```sql
	EXPLAIN (COSTS FALSE) SELECT
	  *
	FROM
	  film
	WHERE
	  film_id = 100;
	```
	
2. Plan for query that uses aggregate function:

```sql
EXPLAIN
SELECT
  count(*)
FROM
  film;
```

3. Plan for a statement that joins multiple tables:

```sql
EXPLAIN
SELECT
  f.film_id,
  title,
  name category_name
FROM
  film f
  INNER JOIN film_category fc
    ON fc.film_id = f.film_id
  INNER JOIN category c
    ON c.category_id = fc.category_id
ORDER BY
  title;
```

4. To add runtime statistics to the output:

```sql
EXPLAIN ANALYZE
SELECT
  f.film_id,
  title,
  name category_name
FROM
  film f
  INNER JOIN film_category fc
    ON fc.film_id = f.film_id
  INNER JOIN category c
    ON c.category_id = fc.category_id
ORDER BY
  title;
```

## PostgreSQL DISTINCT ON ##
1. Summary: To retrieve distinct rows based on a specific column

### Introduction to the PostgreSQL DISTINCT ON clause ###
1. `DISTINCT ON` allows us to retrieve unique rows based on specified columns.

```sql
SELECT
  DISTINCT ON (column1, column2, ...) column1,
  column2,
  ...
FROM
  table_name 
ORDER BY
  column1,
  column2,
  ...;
```

	1. 

### PostgreSQL DISTINCT ON example ###
### Summary ###

## PostgreSQL vs MySQL ##

## PostgreSQL generate_series() Function ##

---

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
## PL/pgSQL Function Overloading ##
## How to Develop a PL/pgSQL Function That Returns a Table ##
## PL/pgSQL Returns SetOf ##
## PostgreSQL Drop Function ##
## PostgreSQL CREATE PROCEDURE ##
## PostgreSQL DROP PROCEDURE Statement ##
## PostgreSQL Stored Procedure with INOUT Parameters ##
## PL/pgSQL Cursor ##

---

## PostgreSQL Triggers - (4 days) ##
1. PostgreSQL trigger is a database object that automatically executes a function in response to an event such as
	1. insert
	2. delete
	3. update
	4. truncate
	
### Section 1: Basic PostgreSQL Triggers ###
1. Intro to PostgreSQL trigger
	1. A brief overview of PostgreSQL triggers
	2. Why you should use triggers and when to use them
2. Creation of triggers
3. Drop trigger
4. Alter trigger
	1. Rename a trigger

### Section 2: INSERT triggers ###
1. BEFORE INSERT triggers
	1. Trigger that is activated automatically before an INSERT event occurs on the associated table.
2. ALTER INSERT triggers
	1. Trigger that is activated automatically after an INSERT event occurs on the associated table.

### Section 3: UPDATE triggers ###
1. BEFORE UPDATE triggers
2. AFTER UPDATE triggers

### Section 4: DELETE triggers ###
1. BEFORE DELETE triggers
2. AFTER DELETE triggers

### Section 5: INSTEAD OF triggers ###
1. INSTEAD OF triggers
	1. To customize the behavior of the INSERT, UPDATE, and DELETE operations on a view.

### Section 6: TRUNCATE triggers ###
1. BEFORE TRUNCATE trigger
	1. To respond before a TRUNCATE event occurs

### Section 7: Enabling & Disabling triggers ###
1. Disable trigger
2. Enable triggers

### Sectino 8: Listing triggers ###
1. Listing triggers

### Section 9: Advanced triggers ###
1. Event trigger
	1. Event trigger that fires when an event related to a DDL statement occurs.
2. Conditional trigger
	1. Fires only when a condition is satisfied.

## Introduction to PostgreSQL Trigger ##
1. Summary: PostgreSQL triggers
	1. Why use triggers.
	2. When to use triggers.

### What are PostgreSQL triggers ###
1. PostgreSQL trigger is a function invoked automatically whenever an event associated with a table occurs.
	1. Event could be:
		1. INSERT
		2. UPDATE
		3. DELETE
		4. TRUNCATE
2. A trigger is a special user-defined function associated with a table.
3. Steps:
	1. Define a new trigger function.
	2. Bind the trigger function to a table.
4. A trigger is automatically invoked when a triggering event occurs.

### PostgreSQL trigger types ###
1. PostgreSQL provides two main types of triggers
	1. Row-level triggers
	2. Statement-level triggers
2. The difference between the two types is how many times the trigger is invoked and at what time.
	1. Example:
		1. If we issue an `UPDATE` statement that modifies 20 rows, the row-level trigger will be invoked 20 times, but statement-level trigger will be invoked 1 time.
3. We can specify whether the trigger is invoked before or after an event.
	1. If a trigger is invoked before an event, it can skip the operatioon for the current row or even change the row being updated or deleted.
	2. If a trigger is invoked after an event, all changes are available to the trigger.

### When to use triggers ###
1. If database is accessed by various applications & we want to keep the cross-functionality within the database that runs automatically whenever the data of the table is modified.
	1. Example: If we want to keep the history of data without requiring the application to have logic to check for every evnt such as `INSERT` or `UPDATE`
2. We can use triggers to maintain complex data integrity rules which we cannot implement elsewhere except at the database level
	1. Example: When a new row is added into the `customer` table, other rows must be also created in the table of banks and credits
3. Drawback of using triggers
	1. We must know that the trigger exists and understand its logic to figure out the effects when data changes.

### PostgreSQL triggers vs SQL standard triggers ###
1. Triggers in PostgreSQL has some specific features
	1. PostgreSQL fires trigger for the `TRUNCATE` event.
	2. PostgreSQL allows you to define the statement-level trigger on views.
	3. PostgreSQL requires you to define a user-defined function as the action of a trigger, while the SQL standard allows you to use any SQL commands.

### Summary ###
1. Trigger is a function invoked automatically when an `INSERT`, `UPDATE`, `DELETE`, or `TRUNCATE` occurs on a table.
2. PostgreSQL supports row-level and statement-level triggers.

## PostgreSQL CREATE TRIGGER Statement ##
1. Summary: `CREATE TRIGGER`
	1. Steps:
		1. New trigger function using `CREATE FUNCTION` statement.
			1. Refer to PL/pgSQL
		2. Bind tirgger function to a table using `CREATE TRIGGER` statement.

### Create trigger function syntax ###
### Introduction to PostgreSQL CREATE TRIGGER statement ###
### PostgreSQL CREATE TRIGGER example ###
### Summary ###

## PostgreSQL DROP TRIGGER Statement ##

## PostgreSQL ALTER TRIGGER Statement ##
1. Summary: `ALTER TRIGGER` statement to rename a trigger.

### Introduction to PostgreSQL ALTER TRIGGER Statement ###
1. The `ALTER TRIGGER` allows us to rename a trigger
2. Syntax:

```sql
ALTER TRIGGER trigger_name
ON table_name
RENAME TO new_trigger_name;
```

	1. `ON` - required to specify the table associated with the trigger.
	2. `new_trigger_name` - new name of the trigger
3. Pre-requisite: We need to be the owner of the table.

### PostgreSQL ALTER TRIGGER Example ###
1. New table:

```sql
DRP TABLE IF EXISTS employees;

CREATE TABLE employees (
  employee_id INT GENERATED ALWAYS AS IDENTITY,
  first_name VARCHAR (50) NOT NULL,
  last_name VARCHAR (50) NOT NULL,
  salary DECIMAL (11. 2) NOT NULL DEFAULT 0,
  PRIMARY KEY (employee_id)
);
```

2. A function that raises an exception if the new salary is greater than the old on by 100%.

```sql
CREATE OR REPLACE TRIGGER check_salary()
  RETURNS TRIGGER
  LANGUAGE PLPGSQL
AS
$$
BEGIN
  IF (NEW.salary - OLD.salary) / OLD.salary >= 1 THEN
    RAISE 'The salary increment cannot be that high.';
  END IF;
END;
$$;
```

3. Before-update trigger that executes `check_salary()`

```sql
CREATE TRIGGER before_update_salary
  BEFORE UPDATE
  ON employees 
  FOR EACH ROW
    EXECUTE PROCEDURE check_salary();
```

4. Insert a new row:

```sql
INSERT INTO employees (first_name, last_name, salary)
VALUES ('John', 'Doe', 100000);
```

5. Update the salary with Id = 1:

```sql
UPDATE employees
SET salary = 20000
WHERE employee_id = 1;
```

	1. Trigger gets fired
6. Rename the trigger:

```sql
ALTER TRIGGER before_update_salary
ON employees
RENAME TO salary_before_update;
```

7. View all triggers:

```
\dS employees
```

### Replacing Triggers ###
1. `OR REPLACE` - Allows usto modify the trigger definition.
	1. Example: Changing function to be executed.
2. Example:

```sql
CREATE OR REPLACE TRIGGER salary_before_update
  BEFORE UPDATE
  ON employees
  FOR EACH ROW
  EXECUTE PROCEDURE validate_salary();
```

3. If PostgreSQL < 14. `DROP` and `CREATE` trigger.

```sql
BEGIN;
  DROP TRIGGER IF EXISTS salary_before_update
  ON employees;
  
  CREATE TRIGGER salary_before_update
    BEFORE UPDATE
	ON employees
	FOR EACH ROW
	EXECUTE PROCEDURE validate_salary();
COMMIT;
```

### Summary ###
1. `ALTER TRIGGER` - to rename a trigger
2. `CREATE OR REPLACE TRIGGER` - New versions of PostgreSQL to replace a trigger with a new
	1. `DROP TRIGGER` and `CREATE TRIGGER` in older versions.

## PostgreSQL BEFORE INSERT Trigger ##
1. Summary: `BEFORE INSERT` trigger.

## PostgreSQL AFTER INSERT Trigger ##
1. Steps:
	1. Define a trigger function that will execute before the `INSERT` event:
	
	```sql
	CREATE OR REPLACE FUNCTION trigger_function()
	  RETURNS TRIGGER
	  LANGUAGE PLPGSQL
	AS
	$$
	BEGIN
	  -- trigger logic
	  -- ...
	  RETURN NEW;
	END;
	$$;
	```
	
		1. Need to place `RETURN NEW` in the trigger function.
2. `BEFORE INSERT` trigger:

```sql
CREATE TRIGGER trigger_name
BEFORE INSERT
ON table_name
FOR EACH { ROW | STATEMENT }
EXECUTE FUNCTION trigger_function();
```

## PostgreSQL BEFORE UPDATE Trigger ##
1. New `inventory` table:

```sql
CREATE TABLE inventory (
  product_id INT PRIMARY KEY,
  quantity INT NOT NULL DEFAULT 0
);
```

2. New `inventory_stat` table:

```sql
CREATE TABLE inventory_stat (
  total_qty INT
);
```

3. A function that increases total quantity in `inventory_stat` before a row is inserted into the `inventory` table.

```sql
CREATE OR REPLACE FUNCTION update_total_qty()
  RETURNS TRIGGER
  LANGUAGE PLPGSQL
AS
$$
DECLARE
  p_row_count INT;
BEGIN
  SELECT COUNT(*) FROM inventory_stat
  INTO p_row_count;
  
  IF p_row_count > 0 THEN
    UPDATE inventory_stat
	SET total_qty = total_qty + NEW.quantity;
  ELSE
    INSERT INTO inventory_stat (total_qty)
	VALUES (NEW.quantity);
  END IF;
  RETURN NEW;
END;
$$;
```

4. `BEFORE INSERT` trigger:

```sql
CREATE TRIGGER inventory_before_insert
BEFORE INSERT
ON inventory
FOR EACH ROW
EXECUTE FUNCTION update_total_qty();
```

5. Insert a row into the `inventory` table:

```sql
INSERT INTO inventory (product_id, quantity)
VALUES (1, 100)
RETURNING *;
```

6. Retrieve data from `inventory_stat` table:

```sql
SELECT * FROM inventory_stat;
```

7. Insert another row:

```sql
INSERT INTO inventory(product_id, quantity)
VALUES(2, 200)
RETURNING *;
```

8. Retrieve data:

```sql
SELECT * FROM inventory_stat;
```

### Summary ###
1. `BEFORE INSERT` is triggered before an `INSERT` event occurs on a table.

## PostgreSQL AFTER INSERT Trigger ##
1. Summary: 

### Introduction to the PostgreSQL AFTER INSERT Trigger ###
### PostgreSQL AFTER INSERT Trigger Example ###
### Summary ###

## PostgreSQL BEFORE UPDATE Trigger ##
1. Summary: `BEFORE UPDATE` trigger executes a trigger before an update event occurs.

### Introduction to the PostgreSQL BEFORE UPDATE Trigger ###
1. Use-cases:
	1. Modify data before an update occurs
	2. Enforce certain conditions
2. Following variables can be accessed:
	1. `OLD` - Record variable. It allows us to access the row before the update
	2. `NEW` - Record variable. It allows us to access the row after the update
	3. `TG_NAME` - trigger name
	4. `TG_OP` - Operation that activates the trigger
		1. `UPDATE` for `BEFORE UPDATE` triggers.
	5. `TG_WHEN` - Trigger timing
		1. `BEFORE` for `BEFORE UPDATE` triggers.
3. Steps:

```sql
CREATE OR REPLACE FUNCTION trigger_function()
  RETURNS TRIGGER
  LANGUAGE PLPGSQL
AS
$$
BEGIN
  -- trigger logic
  -- ...
  RETURN NEW;
END;
$$;
```

```sql
CREATE TRIGGER trigger_name
BEFORE UPDATE
ON table_name
FOR EACH { ROW | STATEMENT }
EXECUTE PROCEDURE trigger_function();
```

### PostgreSQL BEFORE UPDATE Trigger Example ###
1. New table:

```sql
CREATE TABLE employees (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    salary NUMERIC NOT NULL
);
```

2. Trigger function that raises an exception if a new salary is lower than the current salary. The trigger will prevent the update when the exception occurs.

```sql
CREATE OR REPLACE FUNCTION fn_before_update_salary()
  RETURNS TRIGGER
  LANGUAGE PLPGSQL
AS
$$
BEGIN
  IF NEW.salary < OLD.salary THEN
    RAISE EXCEPTION 'New salary cannot be less than current salary';
  END IF;
  RETURN NEW;
END;
$$;
```

3. `BEFORE UPDATE` trigger:

```sql
CREATE TRIGGER before_update_salary_trigger
BEFORE UPDATE OF salary
ON employees
FOR EACH ROW
EXECUTE FUNCTION fn_before_update_salary();
```

4. Insert rows:

```sql
INSERT INTO employees(name, salary)
VALUES
   ('John Doe', 70000),
   ('Jane Doe', 80000)
RETURNING *;
```

5. Attempt to decrease the salary:

```sql
UPDATE employees
SET salary = salary * 0.9
WHERE id = 1;
```

```
ERROR:  New salary cannot be less than current salary
CONTEXT:  PL/pgSQL function fn_before_update_salary() line 4 at RAISE 
```

### Summary ###

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

---

## PostgreSQL Views - (2 days) ##
1. View is a named query stored in the PostgreSQL database server.
	1. It is defined based on one or more tables which are known as base tables.
	2. Query that defines the view is referred to as a defining query
2. After a view is created, we can query data from it as we would from a regular table.
	1. Behind the scenes, PostgreSQL will rewrite the query against the view and its defining query, and executing it to retrieve data from the base tables.
3. View does not store data
	1. Materialized view stores data
		1. They store data physically and periodically refresh it from the base tables
		2. They are handy in many scenarios
			1. Faster data access to remote server
			2. Effective caching mechanism

### Advantages of PostgreSQL views ###
1. Views offer many advantages.

#### Simplifying complex queries ####
1. Views help simplify complex queries
	1. Instead of dealing with joins, aggregations, or filtering conditions, we can query from views as if they were regular tables.
		1. Construct views based on complex queries and store them in the database
		2. Use simple queries based on views instead of using complex queries

#### Security and access control ####
1. Views enable find-grained control over data access
	1. We can construct views that expose subsets of data in the base tables, hiding sensitive info
		1. Use-case: applications that require access to distinct portions of the data

#### Logical data independence ####
1. We can freely modify the structure of the base tables.
	1. Views are a layer of abstraction over the underlying tables.

### Section 1. Basic PostgreSQL views ###
1. New views
2. Removing existing views
3. Following operations:
	1. Construct view
	2. Drop view

### Section 2. Updatable views ###
1. Views that allow us to modify data through them.
2. How to enforce data modification using the `WITH CHECK OPTION` clause.
3. Operations:
	1. Construct updatable views
	2. `WITH CHECK OPTION` - Guides us on how to enforce the data modification through a view based on a condition of the defining query

### Section 3. Materialized views ###
1. Materialized view
	1. Steps of constructing and refreshing data for materialized views

### Section 4. Recursive views ###
1. Constructing recursive views

### Section 5. Managing views ###
1. Management of PostgreSQL views
	1. Alterning views
		1. Renamve view
		2. Modify the check option
		3. Change a column
		4. Set a new schema for a view
	2. Listing views
		1. `\dv` - Listing views in current database
		2. `information_schema.views`

## PostgreSQL CREATE VIEW ##
1. Summary: `CREATE VIEW` - for creation of view in database

### PostgreSQL CREATE VIEW statement ###
1. A view is a named query stored in the database server.
2. Syntax:

```sql
CREATE VIEW view_name
AS
  query;
```

	1. `SELECT` statement that defines view
	2. The query is referred to as defining query of the view

### PostgreSQL CREATE VIEW statement examples ###
1. Using `customer` table

#### Basic CREATE VIEW statement example ####
1. Example:

```sql
CREATE VIEW contact
AS
  SELECT
    first_name,
	last_name,
	email
  FROM
    customer;
```

2. To query from `contact` view:

```sql
SELECT * FROM contact;
```

#### Using the CREATE VIEW statement to construct a view based on a complex query ####
1. Example:

```sql
CREATE VIEW customer_info 
AS
  SELECT
    first_name,
	last_name,
	email,
	phone,
	city,
	postal_code,
	country 
  FROM
    customer
	ENNER JOIN address USING (address_id)
	INNER JOIN city USING (city_id)
	INNER JOIN country USING (country_id);
```

2. Query:

```sql
SELECT * FROM customer_info;
```

#### Constructing a view based on another view ####
1. `customer_usa` view based on `customer_info` view

```sql
CREATE VIEW customer_usa
AS
  SELECT 
    *
  FROM
    customer_info
  WHERE
    country = 'United States';
```

2. Retrieving data from `customer_usa`

```sql
SELECT * FROM customer_usa;
```

### Replacing a view ###
1. To change the defining query of a view, we use `CREATE OR REPLACE VIEW` statement:

```sql
CREATE OR REPLACE VIEW view_name
AS 
  query;
```

	1. If the view already exists, the statement replaces the existing view
	2. If the view does not exist, it generates a new one
2. Example: Changing the defining query of `contact` view to include `phone` info from `address` table

```sql
CREATE OR REPLACE VIEW contact AS
SELECT
  first_name,
  last_name,
  email,
  phone
FROM
  customer
INNER JOIN address USING (address_id);
```

### Display a view on psql ###
1. Select the current database: `\c dvdrental` **(M)**
2. Display the view info using `d+ view_name` **(M)**

```sql
\d+ contact;
```

### Summary ###
1. `\d+` in psql to display the info of a view.

## PostgreSQL Drop View ##
1. Summary: `DROP VIEW` to delete a view from the database.

### Introduction to PostgreSQL DROP VIEW statement ###
1. `DROP VIEW` allows us to remove a view from the database.
2. Syntax:

```sql 
DROP VIEW [IF EXISTS] view_name
[CASCADE | RESTRICT];
```

	1. `IF EXISTS` - to prevent an error if view does not exist.
		1. PostgreSQL will issue a notice instead of an error when we attempt to remove a non-existing view.
	2. `CASCADE` - to remove dependent objects along with the view or `RESTRICT` option to reject the removal of the view if other objects depend on the view.
		1. `RESTRICT` - default.

### Dropping multiple views ###
1. Specify multiple views simultaneously.

```sql
DROP VIEW [IF EXISTS] view_name1, view_name2, ...
[CASCADE | RESTRICT];
```

#### Permissions ####
1. For `DROP VIEW` we need to be owner or have `DROP` privilege.

### PostgreSQL DROP VIEW statement examples ###
1. Using `film`, `film_category`, and `category`

#### Constructing views for practicing ####
1. A new view:

```sql
CREATE VIEW film_info AS
SELECT
  film_id,
  title,
  release_year,
  length,
  name category
FROM
  film
  INNER JOIN film_category USING (film_id)
  INNER JOIN category USING (category_id);
```

2. A `horror_film` view:

```sql
CREATE VIEW horror_film AS
SELECT
  film_id,
  title,
  release_year,
  length
FROM
  film_info
WHERE
  category = 'Horror';
```

3. A `comedy_film` view:

```sql
CREATE VIEW comedy_film AS
SELECT
  film_id,
  title,
  release_year,
  length
FROM
  film_info
WHERE
  category = 'Comedy';
```

4. `film_category_stat` - number of films by category:

```sql
CREATE VIEW film_category_stat
AS
  SELECT
    name,
	COUNT(film_id)
  FROM
    category
	INNER JOIN film_category USING (category_id)
	INNER JOIN film USING (film_id)
  GROUP BY
    name;
```

5. `film_length_stat` - total length of films for each category:

```sql
CREATE VIEW film_length_stat AS
SELECT
  name,
  SUM (length) film_length
FROM
  category
  INNER JOIN film_category USING (category_id)
  INNER JOIN film USING (film_id)
GROUP BY
  name;
```

#### Using the DROP VIEW statement to drop one view example ####
1. Drop `comedy_film` view:

```sql
DROP VIEW comedy_film;
```

#### Using the DROP VIEW statement to drop a view that has dependent objects ####
1. Drop `film_info` view:

```sql
DROP VIEW film_info;
```

	1. Throws an error:
	
	```
	ERROR:  cannot drop view film_info because other objects depend on it view horror_film depends on view film_info 
	```

```sql
DROP VIEW film_info CASCADE;
```

	1. `NOTICE:  drop cascades to view horror_film`

#### Using the DROP VIEW statement to drop mulitiple views ####
1. Single `DROP` statement to drop multiple views:

```sql
DROP VIEW film_length_stat, film_category_stat;
```

### Summary ###
1. `DROP VIEW` to remove one or more views from the database.
2. `IF EXISTS` to remove a view if it exists.
3. `CASCADE` to remove a view and its dependent objects recursively.

## Create PostgreSQL Updatable Views ##
1. Summary: PostgreSQL updatable views for modifying data in the underlying table.

### Introduction to PostgreSQL updatable views ###
1. A view is a named query stored in the database server.
2. Updatable view is possible if the following conditions are met:
	1. We can insert, update or delete data from the underlying tables via the view
3. Conditions for updatable view:
	1. Defining query of the view must have exactly one entry in the `FROM` clause
		1. It can be a table or another updatable view.
	2. Defining query must not contain one of the following clauses at the top level:
		1. GROUP BY
		2. HAVING
		3. LIMIT
		4. OFFSET FETCH
		5. DISTINCT
		6. WITH
		7. UNION
		8. INTERSECT
		9. EXCEPT
	3. Selection list of the defining query must not contain any
		1. WIndow functions
		2. Set-returning functions
		3. Aggregate functions
4. An updatable view can contain both updatable and non-updatable columns
	1. If we attempt to modify a non-updatable column, PostgreSQL will raise an error
5. When we execute a modification statement such as INSERT, UPDATE, or DELETE ot updatable view, PostgreSQL will convert it into the corresponding statement of the underlying table.
6. If we have a where condition in the defining query of a view, we still can update or delete the rows that are not visible through the view.
	1. To avoid it, we can use `WITH CHECK OPTION` to define the view.

### PostgreSQL updatable views example ###
#### Setting up a sample table ####
1. `cities` table:

```sql
CREATE TABLE cities (
    id SERIAL PRIMARY KEY ,
    name VARCHAR(255),
    population INT,
    country VARCHAR(50)
);

INSERT INTO cities (name, population, country)
VALUES
    ('New York', 8419600, 'US'),
    ('Los Angeles', 3999759, 'US'),
    ('Chicago', 2716000, 'US'),
    ('Houston', 2323000, 'US'),
    ('London', 8982000, 'UK'),
    ('Manchester', 547627, 'UK'),
    ('Birmingham', 1141816, 'UK'),
    ('Glasgow', 633120, 'UK'),
    ('San Francisco', 884363, 'US'),
    ('Seattle', 744955, 'US'),
    ('Liverpool', 498042, 'UK'),
    ('Leeds', 789194, 'UK'),
    ('Austin', 978908, 'US'),
    ('Boston', 694583, 'US'),
    ('Manchester', 547627, 'UK'),
    ('Sheffield', 584853, 'UK'),
    ('Philadelphia', 1584138, 'US'),
    ('Phoenix', 1680992, 'US'),
    ('Bristol', 463377, 'UK'),
    ('Detroit', 673104, 'US');
	
SELECT * FROM cities;
```

#### Constructing an updatable view ####
1. `city_us` - includes cities in the US only:

```sql
CREATE VIEW city_us
AS
SELECT
  *
FROM
  cities
WHERE
  country = 'US';
```

2. Insert a new row into the `cities` table via the `city_us` view:

```sql
INSERT INTO city_us (name, population, country)
VALUES ('San Jose', 983459, 'US');
```

3. Review data from `cities` table:

```sql
SELECT * FROM cities
WHERE name = 'San Jose';
```

4. Update data in cities table via `city_us` view:

```sql
UPDATE city_us
SET population = 100000
WHERE name = 'New York';
```

5. Verify the update:

```sql
SELECT * FROM cities 
WHERE name = 'New York';
```

6. Delete a row from `cities` via the `city_us` view:

```sql
DELETE FROM city_us
WHERE id = 21;
```

### Summary ###
1. View can be updatable when its defining query meets certain conditions.

## PostgreSQL WITH CHECK OPTION ##
1. Summary: Updatable view using `WITH CHECK OPTION` clause to ensure that the changes to the base tables through the view satisfy the view-defining condition.

### Introduction to the PostgreSQL WITH CHECK OPTION clause ###
1. To ensure that data modification made through a view adheres to certain conditions in view's definition, use `WITH CHECK OPTION` clause.
2. Specified in `CREATE VIEW`

```sql
CREATE VIEW view_name AS 
query
WITH CHECK OPTION;
```

3. `WITCH CHECK OPTION` ensures that we can only modify data of the view that satisfies the condition in the view's defining query.

#### Scope of check ####
1. We can specify a scope of check.
	1. `LOCAL`
	2. `CASCADED`
2. `LOCAL` scope restricts the check option enforcement to the current view only.
	1. It does not enforce the check to the views that the current view is based on.
	2. Syntax:
	
	```sql
	CREATE VIEW view_name AS
	query
	WITH LOCAL CHECK OPTION;
	```
	
3. `CASCADED` scope extends the check optoin enforcement to all underlying views of the current view.
	1. Syntax:
	
	```sql
	CREATE VIEW view_name AS
	query
	WITH CASCADED CHECK OPTION;
	```
	
		1. Use `ALTER VIEW` to change the scope of check for an existing view.

### PostgreSQL WITH CHECK OPTION examples ###
#### Setting up a sample table ####
1. New table `employees`

```sql
CREATE TABLE employees (
    id SERIAL PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    department_id INT,
    employee_type VARCHAR(20)
       CHECK (employee_type IN ('FTE', 'Contractor'))
);

INSERT INTO employees (first_name, last_name, department_id, employee_type)
VALUES
    ('John', 'Doe', 1, 'FTE'),
    ('Jane', 'Smith', 2, 'FTE'),
    ('Bob', 'Johnson', 1, 'Contractor'),
    ('Alice', 'Williams', 3, 'FTE'),
    ('Charlie', 'Brown', 2, 'Contractor'),
    ('Eva', 'Jones', 1, 'FTE'),
    ('Frank', 'Miller', 3, 'FTE'),
    ('Grace', 'Davis', 2, 'Contractor'),
    ('Henry', 'Clark', 1, 'FTE'),
    ('Ivy', 'Moore', 3, 'Contractor');
```

#### Basic PostgreSQL WITH CHECK OPTION example ####
1. Define a view called `fte` that retreives the employees with the type `FTE` from the `employees` table:

```sql
CREATE VIEW fte
AS
  SELECT
    id,
	first_name,
	last_name,
	department_id,
	employee_type
  FROM 
    employees
  WHERE
    employee_type = 'FTE';
```

2. Retrieve data from the `fte` view:

```sql
SELECT * FROM fte;
```

3. Insert a new row into the `employees` table via the `fte` view:

```sql
INSERT INTO fte (first_name, last_name, department_id, employee_type)
VALUES ('John', 'Smith', 1, 'Contractor');
```

	1. It succeeds
		1. We can insert an employee with the type `Contractor` into the `employee` table view the view that exposes the employee to the type of `FTE`
			1. Fix: Use `WITH CHECK OPTION`
			
			```sql
			CREATE OR REPLACE VIEW fte
			AS
			  SELECT
				id,
				first_name,
				last_name,
				department_id,
				employee_type
			  FROM 
				employees
			  WHERE
				employee_type = 'FTE'
			WITH CHECK OPTION;
			```
			
				1. If we insert, delete on `employees` table that satisfies the `WHERE` clause in defining query of the view
					1. The following insert will fail with an error:
					
					```sql
					INSERT INTO fte (first_name, last_name, department_id, employee_type)
					VALUES ('John', 'Snow', 1, 'Contractor');
					```
					
					```
					ERROR:  new row violates check option for view "fte"
					Failing row contains (12, John, Smith, 1, Contractor). 
					```
					
						1. `Contractor` does not satisfy the condition `employee_type = 'FTE'`
4. Change the last name of employee to `Doe`

```sql
UPDATE fte
SET last_name = 'Doe'
WHERE id = 2;
```

	1. It works

#### Using WITH LOCAL CHECK OPTION example ####
1. Re-instantiate `fte` view without the `WITH CHECK OPTION`

```sql
CREATE OR REPLACE VIEW fte AS
SELECT
  id,
  first_name,
  last_name,
  department_id,
  employee_type
FROM
  employees
WHERE
  employee_type = 'FTE';
```

2. New view `fte_1` based on `fte` that returns the `employees` of department `1`, with the `WITH LOCAL CHECK OPTION`:

```sql
CREATE OR REPLACE VIEW fte_1
AS
  SELECT
    id,
	first_name,
	last_name,
	department_id,
	employee_type
  FROM
    fte
  WHERE
    department_id = 1
WITH LOCAL CHECK OPTION;
```

3. Retrieve data from the `fte_1` view:

```sql
SELECT * FROM fte_1;
```

	1. If we modify data via `fte_1` view, PostgreSQL only checks the condition in `fte_1` view.
	
	```sql
	INSERT INTO fte_1 (first_name, last_name, department_id, employee_type)
	VALUES ('Miller', 'Jackson', 1, 'Contractor');
	```
	
		1. Succeeds, because only `department_id = 1` is checked.
4. Query data from `employees` table:

```sql
SELECT
  *
FROM
  employees
WHERE
  first_name = 'Miller'
  AND last_name = 'Jackson';
```

#### Using WITH CASCADED CHECK OPTION example ####
1. Regenerate the view `fte_1` with the `WITH CASCADED CHECK OPTION`

```sql
CREATE OR REPLACE VIEW fte_1
AS
  SELECT
    id,
	first_name,
	last_name,
	department_id,
	employee_type
  FROM
    fte
  WHERE
    department_id = 1
WITH CASCADED CHECK OPTION;
```

2. Insert a new row into `employees` table via the `fte_1` view:

```sql
INSERT INTO fte_1 (first_name, last_name, department_id, employee_type)
VALUES ('Peter', 'Tailor', 1, 'Contractor');
```

```
ERROR:  new row violates check option for view "fte"
Failing row contains (14, Peter, Tailor, 1, Contractor). 
```

3. `WITH CASCADED CHECK OPTION` instructs PostgreSQL to check the constraint on `fte_1` view and also its base view which is `fte`.

### Summary ###
1. Use `WITH CHECK OPTION` to enforce constraints on data modifications through views and ensure that only valid data can be changed.

## PostgreSQL ALTER VIEW Statement ##
1. Summary: `ALTER VIEW` to change the properties of a viwe.

### Introduction to the PostgreSQL ALTER VIEW statement ###
1. `ALTER VIEW` allows us to change various properties of a view.
	1. To change a view's defining query, use `CREATE OR REPLACE VIEW`
2. Syntax:

```sql
ALTER VIEW [IF EXISTS] view_name
action;
```

	1. `IF EXISTS` - otherwise throws error if a non-existing view is attempted to be altered.
		1. The statement issues a notice instead.
	2. `action` - The action we want to do with the view.
		1. Renaming the view
		2. Setting view option
		3. ...

#### Renaming a view ####
1. Syntax:

```sql
ALTER VIEW [ IF EXISTS ] view_name
RENAME TO new_view_name;
```

2. New view:

```sql
CREATE VIEW film_type
AS
SELECT title, rating
FROM film;
```

3. Change the view name:

```sql
ALTER VIEW film_type RENAME TO film_rating;
```

#### Changing the view option ####
1. Syntax:

```sql
ALTER VIEW [ IF EXISTS ] view_name
SET ( view_option_name [= view_option_value] [, ... ] );
```

	1. `view_option_name`
		1. `check_option`: Change the check option. Valid value is `local` or `cascaded`
		2. `security_barrier`: Change the security-barrier property of a view. Valid value is `true` or `false`
		3. `security_invoker`: Change the security invoker of a view. The valid value is `true` or `false`
2. Changing the check option of the `film_rating` view to `local`:

```sql
ALTER VIEW film_rating
SET (check_option = local);
```

3. Use `\d+`

```psql
\d+ film_rating
```

#### Changing the view column ####
1. Change column name of a view to a new one:

```sql
ALTER VIEW [ IF EXISTS ] view_name
RENAME [ COLUMN ] column_name TO new_column_name;
```

2. Changing `title` column of the `film_rating` view to `film_title`:

```sql
ALTER VIEW film_rating
RENAME title TO film_title;
```

3. `\d+ film_rating`

#### Setting the new schema ####
1. Syntax:

```sql
ALTER VIEW [ IF EXISTS ] view_name
SET SCHEMA new_schema;
```

2. Example:

```sql
CREATE SCHEMA web;
```

```sql
ALTER VIEW IF EXISTS film_rating
SET SCHEMA web;
```

3. `\d+ web.film_rating`

### Summary ###
1. `ALTER VIEW ... RENAME TO` to rename a view.
2. `ALTER VIEW ... (SET check_option)` to change the check option of a view.
3. `ALTER VIEW ... SET SCHEMA` to change the schema of a view.

## PostgreSQL Materialized Views ##
1. Summary: Materialized views store the result of a query physically and refresh the data from base tables periodically.

### Introduction to the PostgreSQL materialized views ###
1. Materialized views cache the result set of an expensive query and allow you to refresh data periodically.
2. Use-case: For fast data access.
	1. Data warehouses.
	2. Business intelligence applications.

#### Constructing materialized views ####
1. `CREATE MATERIALIZED VIEW` statement:

```sql
CREATE MATERIALIZED VIEW [ IF NOT EXISTS ] view_name
AS 
query
WITH [NO] DATA;
```

	1. `WITH DATA` - to load data into materialized view at the creation time.
	2. `WITH NO DATA` - Unreadable (cannot query) until we load data into it.

#### Refreshing data for materialized views ####
1. `REFRESH MATERIALIZED VIEW` statement:

```sql
REFRESH MATERIALIZED VIEW view_name;
```

	1. PostgreSQL locks the underlying tables when refreshing data in materialized view.
		1. We will not be able to retrieve data from underlying tables while data is loading into the view.
			1. Solution: `CONCURRENTLY` option
			
			```sql
			REFRESH MATERIALIZED VIEW CONCURRENTLY view_name;
			```
			
				1. PostgreSQL generates a temporarily updated version of the materialized view, compares two version, and performs `INSERT` and `UPDATE` only the differences.
				2. PostgreSQL allows us to retrieve data from a materialized view while it is being updated.
				3. Requirement: `CONCURRENTLY` option needs `UNIQUE` index
				4. Available in PostgreSQL 9.4 onwards.

#### Removing materailized views ####
1. `DROP MATERIALIZED VIEW` statement:

```sql
DROP MATERIALIZED VIEW view_name;
```

### PostgreSQL materialized views example ###
1. Materialized view `rental_by_category` using the `CREATE MATERIALIZED VIEW` statement:

```sql
CREATE MATERIALIZED VIEW rental_by_category
AS
  SELECT c.name AS category,
      sum(p.amount) AS total_sales
    FROM (((((payment p
	  JOIN rental r ON ((p.rental_id = r.rental_id)))
	  JOIN inventory i ON ((r.inventory_id = i.inventory_id)))
	  JOIN film f ON ((i.film_id = f.film_id)))
	  JOIN film_category fc ON ((f.film_id = fc.film_id)))
	  JOIN category c ON ((fc.category_id = c.category_id)))
    GROUP BY c.name
	ORDER BY sum(p.amount) DESC
WITH NO DATA;
```

2. If you attempt to query, you will get an error:

```sql
SELECT * FROM rental_by_category;
```

```
ERROR:  materialized view "rental_by_category" has not been populated
HINT:  Use the REFRESH MATERIALIZED VIEW command. 
```

3. Load data:

```sql
REFRESH MATERIALIZED VIEW rental_by_category;
```

4. Re-run the query.
5. To refresh with `CONCURRENTLY` option, define `UNIQUE` index for the view first.

```sql
CREATE UNIQUE INDEX rental_category
ON rental_by_category (category);
```

```sql
REFRESH MATERIALIZED VIEW CONCURRENTLY rental_by_category;
```

### Summary ###
1. Materialized view is a view that stores data that comes from the base tables.
2. Use `CREATE MATERIALIZED VIEW` for creation.
3. Use `REFRESH MATERIALIZED VIEW` to load data from the base tables into the view.
4. Use `DROP MATERIALIZED VIEW` to drop a materialized view.

## PostgreSQL Recursive View ##
1. Summary: `CREATE RECURSIVE VIEW` statement **(M)**

### Introduction to the PostgreSQL recursive view ###
1. A recursive view is a view whose defining query references the view name itself.
2. Use-cases:
	1. Performing hierarchical queries
	2. Performing recursive queries on hierarchical data structures stored in the db.
3. `CREATE REcURSIVE VIEW` is a syntactic sugar for a standard recursive query.

```
CREATE RECURSIVE VIEW view_name (columns)
AS
query;
```

	1. We can add optional schema to the name of the view.
	2. `SELECT` statement references the `view_name` to make the view recursive.
4. It is equivalent to the following statement:

```sql
CREATE VIEW view_name
AS
  WITH RECURSIVE cte_name (columns) AS (
    SELECT ...)
  SELECT columns AS cte_name;
```

### Constructing a recursive view example ###
1. Using `employees` table.
2. Recursive query to return employees and their managers including the CEO using a common table expression (CTE).

```sql
WITH RECURSIVE reporting_line AS (
  SELECT
    employee_id,
	full_name AS suportidates
  FROM
    employees
  WHERE
    manager_id IS NULL
  UNION ALL
  SELECT
    e.employee_id,
	(
	  rl.subordinates || ' > ' || e.full_name
	) AS subordinates
  FROM
    employees e
    INNER JOIN reporting_line rl ON e.manager_id = rl.employee_id
)
SELECT
  employee_id,
  subordinates
FROM
  reporting_line
ORDER BY
  employee_id;
```

3. `CREATE RECURSIVE VIEW` example:

```sql
CREATE RECURSIVE VIEW reporting_line (employee_id, subordinates) AS
SELECT
  employee_id,
  full_name AS subordinates
FROM
  employees
WHERE
  manager_id IS NULL
UNION ALL
SELECT
  e.employee_id,
  (
    rl.subordinates || ' > ' || e.full_name
  ) AS subordinates
FROM 
  employees e
  INNER JOIN reporting_line rl ON e.manager_id = rl.employee_id;
```

4. To view reporting line of employee id 10:

```sql
SELECT
  subordinates
FROM
  reporting_line
WHERE
  employee_id = 10;
```

### Summary ###
1. A recursive view is a view whose defining query references the view name.
2. Use the `CREATE RECURSIVE VIEW` statement to construct a recursive view.

### Explanation ###

This SQL statement creates a **recursive view** that builds an **organizational reporting hierarchy** (manager → employee → employee…) as a readable path.

Let’s break it down step by step.

---

## 1️⃣ What this statement does (high level)

```sql
CREATE RECURSIVE VIEW reporting_line (employee_id, subordinates) AS ...
```

* Creates a **view** named `reporting_line`
* Uses **recursion** to walk through a manager–employee relationship
* Produces:

  * `employee_id` → the current employee
  * `subordinates` → a **string path** showing the chain from the top-level manager down to that employee

Example output:

```
1 | Alice
2 | Alice > Bob
3 | Alice > Bob > Charlie
```

---

## 2️⃣ The base (anchor) query – starting point

```sql
SELECT
  employee_id,
  full_name AS subordinates
FROM
  employees
WHERE
  manager_id IS NULL
```

### What this means

* Selects **top-level employees** (e.g., CEO, founders)
* `manager_id IS NULL` ⇒ no one above them
* Initializes the reporting path

### Example

If `employees` contains:

| employee_id | full_name | manager_id |
| ----------- | --------- | ---------- |
| 1           | Alice     | NULL       |

Result of base query:

| employee_id | subordinates |
| ----------- | ------------ |
| 1           | Alice        |

This is the **root of the hierarchy**.

---

## 3️⃣ `UNION ALL` – combining base + recursive results

```sql
UNION ALL
```

* Combines:

  * The **base rows** (top managers)
  * The **recursive rows** (their subordinates, and so on)
* `UNION ALL` is required for recursion (not `UNION`)

---

## 4️⃣ The recursive query – expanding the hierarchy

```sql
SELECT
  e.employee_id,
  (rl.subordinates || ' > ' || e.full_name) AS subordinates
FROM 
  employees e
  INNER JOIN reporting_line rl
    ON e.manager_id = rl.employee_id;
```

### What happens here

* Joins:

  * `employees e` → current employee
  * `reporting_line rl` → their manager’s row from the previous iteration
* For each employee:

  * Finds their manager in `reporting_line`
  * Appends their name to the existing path

### String concatenation

```sql
rl.subordinates || ' > ' || e.full_name
```

Builds a readable chain like:

```
Alice > Bob > Charlie
```

---

## 5️⃣ How recursion unfolds (iteration by iteration)

### Iteration 1 (base)

```
Alice
```

### Iteration 2

```
Alice > Bob
Alice > Carol
```

### Iteration 3

```
Alice > Bob > David
```

And so on… until no more employees match.

---

## 6️⃣ Why this works

* `CREATE RECURSIVE VIEW` allows the view to **reference itself**
* Each iteration:

  * Takes the previous level (`reporting_line`)
  * Finds employees who report to it
* Stops automatically when no new rows are produced

---

## 7️⃣ Final result of the view

The `reporting_line` view contains **one row per employee**, with:

* Their `employee_id`
* Their **full reporting path from the top**

Example:

| employee_id | subordinates        |
| ----------- | ------------------- |
| 1           | Alice               |
| 2           | Alice > Bob         |
| 3           | Alice > Carol       |
| 4           | Alice > Bob > David |

---

## 8️⃣ Common use cases

* Org charts
* Manager–employee hierarchies
* Category trees
* Folder structures
* Dependency chains

---

## 9️⃣ Key takeaways

* **Anchor query**: defines the starting rows
* **Recursive query**: expands the hierarchy
* **Self-join**: walks the tree
* **String concatenation**: builds human-readable paths

If you want, I can also:

* Convert this to a **CTE (`WITH RECURSIVE`)**
* Add **depth/level**
* Detect **cycles**
* Optimize it for PostgreSQL specifically

## PostgreSQL List Views ##
1. Summary: Using `psql` command to list views.
	1. Views are named queries stored directly in the server
2. We can use `\dv` or query `information_schema.views` and `pg_matviews`

### Listing views using psql ###
1. Change current database to `dvdrental`

```psql
\c dvdrental
```

2. List views in db using `\dv` command

```psql
\dv
```

	1. Display Views
	2. Output has 4 columns:
		1. Schema: Schema of the view. `public` is the default schema
		2. Name: Name of the view
		3. Type: Type of the object. `view` in this case.
		4. Owner: User account the instantiated the view.

### Listing view using SQL statement ###
1. PostgreSQL has many database views that contain info about objects defined in the current db through the information schema
2. Execute the following SQL statement:

```sql
SELECT
  table_schema,
  table_name
FROM
  information_schema.views
WHERE
  table_schema NOT IN (
    'information_schema', 'pg_catalog'
  )
ORDER BY
  table_schema,
  table_name;
```

### Listing materialized views ###
1. Query them from `pg_matviews` view.

```sql
SELECT * FROM pg_matviews;
```

2. To get only the names:

```sql
SELECT
  matviewname AS materialized_view_name
FROM
  pg_matviews
ORDER BY
  materialized_view_name;
```

### Summary ###
1. `\dv` - to list all ivews of a database.
2. `information_scheams.views` to retrieve info about views.
3. `pg_matviews` view to obtain materialized views. 

---

## PostgreSQL Indexes - (3 days) ##
1. Summary: PostgreSQL indexes to enhance the data retrieval speed.
	1. Various index types

### Introduction to PostgreSQL indexes ###
1. An index is a data structure that speeds up data retrieval.
	1. It gives PostgreSQL a quick way to locate rows inside a table without scanning the entire table.
		1. It is like an index pages of a book.
			1. We can check the index for a topic, which points directly to the page we need.
2. Example: `contacts` table:

```sql
CREATE TABLE contacts (
  id INT PRIMARY KEY,
  name VARCHAR (255) NOT NULL,
  phone VARCHAR (10) NOT NULL
);
```

3. To find a contact by name:

```sql
SELECT * FROM contacts
WHERE name = 'John Doe';
```

	1. Without the index, PostgreSQL must scan the entire table to find "John Doe"
		1. It is slow if the table contains many rows. (like reading a whole book to find a single line)
		2. Solution: With index on the name column, PostgreSQL can locate matching rows much faster
		
		```sql
		CREATE INDEX contacts_name
		ON contacts (name);
		```
		
			1. Generates an index with the name `contacts_name` on the `name` column of the `contacts` table.
			2. PostgreSQL extracts all values from the `name` column and stores them in the index data structure.
				1. The process may take some time if table contains many rows.
					1. PostgreSQL allows `SELECT` while constructing the index, but blocks `INSERT`, `UPDATE`, and `DELETE` operations.
						1. `CREATE INDEX CONCURRENTLY` - allows `INSERT`, `UPDATE`, and `DELETE` but it is slower.
			3. `SELECT` uses the `contacts_name` index to quickly find the matching rows:
			
			```sql
			SELECT * FROM contacts
			WHERE name = 'John Doe';
			```
			
			4. After the index is created, PostgreSQL must keep the index synchronized with the table
				1. Inserting, deleting, and updating the table forces PostgreSQL to update the index to keep it accurate.
					1. **Indexes inprove read speed, but add a big of overhead to write operations**

### Types of PostgreSQL indexes ###
1. PostgreSQL offers different index types to cater to specific data scenarios and query patterns
	1. Helps enhance query performance more effectively.

#### B-tree index ####
1. B-tree - default index type in PostgreSQL
	1. Balanced tree.
	2. They maintain sorted values, making them efficient for exact matches and range queries.

#### Hash index ####
1. Maintains 32-bit hash code created from values of th indexed columns
	1. They handle only simple equality comparisons (`=`).

#### GIN index ####
1. Inverted indexes.
2. For composite values such as:
	1. Arrays
	2. JSONB data
	3. Full-text search
3. GIN maintains separate entry for each component
	1. It checks for existence of a specific component.

#### GiST index ####
1. It supports a wide range of data types
	1. Data types
		1. Geometric
		2. Full-text data
2. It allows different search strategies such as
	1. Nearest-neighbor
	2. Partial match
3. For specialized applications

#### SP-GiST index ####
1. SP-GiST indexes
	1. Useful for indexing data with hierarchical structures or complex data types
	2. They partition index space into non-overlapping regions
		1. They offer efficient search capabilities for specialized data structures

#### BRIN (Block Range Index) index ####
1. Designed for very large tables where indexing every row is impractical
	1. BRIN indexes divides table into ranges of pages and stores summarized info about each range
		1. Efficient for range queries on large datasets while using minimal space

#### PostgreSQL indexes tutorials ####
1. Create index - Defining new index for a table
2. Unique index - Steps for defining unique indexes
3. Index on expression - Index based on expressions
4. Partial index - Partial indexes that include a subset of rows of the indexed columns
5. Multicolumn indexes - How to define indexes that include multiple table columns
6. Reindex - How to rebuild indexes
7. List indexes - How to list all indexes in a table or database
8. Drop index - How to delete an index
9. Index types - Various PostgreSQL index types in detail
10. Full text search - Shows us how to use the GIN index to enable full-text search in PostgreSQL
11. JSON index - How to index a JSONB column for enhanced query performance

## PostgreSQL CREATE INDEX Statement ##
1. Summary: `CREATE INDEX` - to define a new index for a table.

### Introduction to PostgreSQL CREATE INDEX statement ###
1. Index is a separate data structure that enhances speed of data retrieval from a table at the cost of additional writes and storage required to maintain it.
2. Index allows us to improve query performance when using it appropriately (on large tables especially)
3. Syntax:

```sql
CREATE INDEX [IF NOT EXISTS] index_name
ON table_name (column1, column2, ...);
```

	1. Specify index name
	2. `IF NOT EXISTS` - prevents an error if an index already exists
	3. `table_name` to which the index belongs
	4. `(...)` indexed columns
4. It generates a B-tree index by default

### PostgreSQL CREATE INDEX statement example ###
1. `address` table.
2. Connect to `dvdrental` database
3. Execute the following query to find the address whose phone number is 223664661973.

```sql
SELECT
  address_id,
  address,
  district,
  phone
FROM
  address
WHERE
  phone = '223664661973';
```

4. Show the query plan:

```sql
EXPLAIN
SELECT
  address_id,
  address,
  district,
  phone
FROM
  address
WHERE
  phone = '223664661973';
```

	1. Seq Scan on address (..)
5. Define index for `phone` table.

```sql
CREATE INDEX idx_address_phone
ON address (phone);
```

	1. PostgreSQL scans `address` table
	2. Extracts data from the `phone` column
	3. Inserts the value into the index `idx_address_phone`
6. Show indexes that belong to the `address` table from the `pg_indexes`

```sql
SELECT
  indexname,
  indexdef
FROM
  pg_indexes
WHERE
  tablename = 'address';
```

	1. `idx_address_phone` was created successfully
	2. `address_pkey` and `idx_fk_city_id` were created implicitly when the `address` table was created
		1. `address_pkey` - for the primary key columns `address_id`
		2. `idx_fk_city_id` - for foreign key `city_id` column.
7. Execute the following query again:

```sql
EXPLAIN
SELECT
  address_id,
  address,
  district,
  phone
FROM
  address
WHERE
  phone = '223664661973';
```

	1. `Index Scan using idx_address_phone on address`

### Summary ###
1. `CREATE INDEX` for index creation
2. `EXPLAIN` for explaining a query

## PostgreSQL UNIQUE Index ##
1. Summary: Unique index ensures the uniqueness of values in one ore more columns.

### Introduction to PostgreSQL UNIQUE index ###
1. PostgreSQL unique index enforces the uniqueness of values in one or multiple columns.
2. Syntax:

```sql
CREATE UNIQUE INDEX index_name
ON table_name (column [, ...])
[NULL [ NOT ] DISTINCT ];
```

	1. Table name along with columns
	2. `NULL NOT DISTINCT` - treats nulls as equal
	3. `NULL DISTINCT` - treats nulls as distinct values
		1. Default
			1. Indexed column may contain multiple nulls
3. Only B-tree index type supports unique indexes
4. If two or more columns are used for unique index, the combined values in the columns cannot be duplicated in multiple rows
5. When we defined a primary key or unique constraint, PostgreSQL automatically generates a unique index

### PostgreSQL UNIQUE index examples ###
#### Unique indexes for a primary key column and a column with a unique constraint ####
1. `employees` table:

```sql
CREATE TABLE employees (
  employee_id SERIAL PRIMARY KEY,
  first_name VARCHAR (255) NOT NULL,
  last_name VARCHAR (255) NOT NULL,
  email VARCHAR (255) UNIQUE
);
```

	1. PostgreSQL generates two unique indexes
		1. One for the primary key
		2. One for the column with `UNIQUE` constraint
2. Show the indexes of the `employee` table:

```sql
SELECT
  tablename,
  indexname,
  indexdef
FROM
  pg_indexes
WHERE
  tablename = 'employee';
```

#### Using PostgreSQL UNIQUE index for single column example ####
1. Add `mobile_phone` column to `employees` table:

```sql
ALTER TABLE employees
ADD mobile_phone VARCHAR (2);
```

2. Define a unique index to ensure that the mobile phones are distinct for all employees:

```sql
CREATE UNIQUE INDEX idx_employees_mobile_phone
ON employees (mobile_phone);
```

3. Insert a new row:

```sql
INSERT INTO employees(first_name, last_name, email, mobile_phone)
VALUES ('John','Doe','john.doe@example.com', '(408)-555-1234');
```

4. Attempt to insert another row with the same phone number:

```sql
INSERT INTO employees(first_name, last_name, email, mobile_phone)
VALUES ('Jane','Doe','jane.doe@example.com', '(408)-555-1234');
```

	1. duplicate key value violates unique constraint "idx_employees_mobile_phone"

#### Using PostgreSQL UNIQUE index for multiple columns ####
1. Two new columns: `work_phone`, and `extension`

```sql
ALTER TABLE employees
ADD work_phone VARCHAR (20),
ADD extension VARCHAR (5);
```

	1. Multiple employees can share the work phone number but not the extension number.
2. Unique index on both:

```sql
CREATE UNIQUE INDEX idx_employees_work_phone_extension
ON employees (work_phone, extension);
```

3. Insert a row into the `employees` table:

```sql
INSERT INTO employees(first_name, last_name, work_phone, extension)
VALUES('Lily', 'Bush', '(408)-333-1234','1212');
```

4. Insert another row with the same work phone but different extension

```sql
INSERT INTO employees(first_name, last_name, work_phone, extension)
VALUES('Joan', 'Doe', '(408)-333-1234','1211');
```

5. Attempt to insert a row with both work phone and extension the same

#### Summary ####
1. Unique index is used to enforce uniqueness of values in a column or a set of columns
2. A unique index is created for PK and column with unique constraint

## PostgreSQL Index on Expression ##
1. Summary: How to leverage PostgreSQL index on expression to improve the performance of queries that involve expressions.

### Introduction to PostgreSQL index on expression ###
1. PostgreSQL also allows us to construct an index based on an expression involving table columns.
	1. It is called index on expression
	2. Aka functional indexes
2. Syntax:

```sql
CREATE INDEX index_name
ON table_name (expression);
```

	1. `expression` - Involves table columns of `table_name` in the `ON` clause
3. PostgreSQL will consider using the index when the expression appears in the `WHERE` clause or in `ORDER BY` clause.
4. Maintaining indexes on expressions incurs additional costs
	1. PostgreSQL uses result of insertion or updation for building index
		1. Use indexes when prioritizing retrieval speed over insertion and update speed.
		
### PostgreSQL index on expression example ###
1. `customer` table.
	1. It has a B-tree index defined for the `last_name` column
2. Retrieve customers with the last names 'Purdy'

```sql
SELECT
  customer_id,
  first_name,
  last_name
FROM
  customer
WHERE
  last_name = 'Purdy';
```

3. Get the query plan:

```sql
EXPLAIN
SELECT
  customer_id,
  first_name,
  last_name
FROM
  customer
WHERE
  last_name = 'Purdy';
```

4. Find customers whose last name is 'purdy'

```sql
EXPLAIN
SELECT
  customer_id,
  first_name,
  last_name
FROM
  customer
WHERE
  LOWER(last_name) = 'purdy';
```

	1. Sequential scan
		1. Solution: Define index on expression
		
		```sql
		CREATE INDEX idx_customer_lower_last_name
		ON customer (LOWER(last_name));
		```
		
		2. Run explain query:
			1. Index on the expression is used.

### Summary ###

## PostgreSQL Partial Index ##
1. Summary: PostgreSQL partial index is used to construct an index based on a subset of rows in a table based on specified conditions

### Introduction to PostgreSQL partial index ###
1. Sometimes, we may want to include only some values from the indexed column in the index.
	1. Solution: Partial index
		1. It is an index built on a subset of data of the indexed columns
			1. Subset of data is defined using a predicate
				1. PostgreSQL will build an index for rows that satisfy the predicate
2. Partial index can enhance query performance while reducing the index size
	1. It can improve table updates because PostgreSQL does not need to maintain the index in all cases.
3. `CREATE INDEX` with a `WHERE` clause

```sql
CREATE [IF NOT EXISTS] INDEX index_name
ON table_name (column1, column2, ...)
WHERE predicate;
```

	1. `WHERE` clause specifies the condition for rows to be included in the index

### PostgreSQL partial index example ###
1. `customer` table
	1. The `active` column has two values:
		1. `0`: inactive
		2. `1`: active
2. When querying from the db, we often work with inactive customers (not active ones)
	1. Example: To follow up with customers to get them order more films
	2. Implementation:
	
	```sql
	CREATE INDEX customer_active
	ON customer (active)
	WHERE active = 0;
	```
	
3. Show the query plan:

```sql
EXPLAIN
SELECT
  *
FROM
  customer
WHERE
  active = 0;
```

	1. Includes only the rows that are often searched.

### Summary ###
1. PostgreSQL partial index includes a subset of rows in a table specified by a condition.

## PostgreSQL Multicolumn Indexes ##
1. Summary: Multicolumn indexes (indexes on two or more columns)

### Introduction to PostgreSQL multicolumn indexes ###
1. When indexes are created on two or more columns on a table, it is a multi-column index
	1. Aka composite index
	2. Aks combined index
	3. Aka concatenated index
2. Max 32 columns
	1. `pg_config_manual.h` can be modified to adjust the limit and rebuild from source-code
3. The following index types support multicolumn indexes
	1. B-tree
	2. GIST
	3. BIN
	4. BRIN
4. Syntax:

```sql
CREATE INDEX [IF NOT EXISTS] index_name
ON table_name (column1, column2, ...);
```

5. Place the columns that are frequently used in the `WHERE` clause at the beginning of the column list followed by the columns that are less frequently used.
6. If we have `(column1, column2, column3, ...)`, it will be considered for queries such as:

```sql
WHERE column1 = v1 AND column2 = v2 AND column3 = v3;
```

```sql
WHERE column1 = v1 AND column2 = v2;
```

```sql
WHERE column1 = v1;
```

	1. Helps to efficiently narrow down the portion of the index.
7. If the query does not constrain the first column of the index, PostgreSQL must evaluate whether a full index scan on this index is more efficient than alternative indexes or table scan.
	1. Example:
	
	```sql
	WHERE column3 = v3;
	```
	
	```sql
	WHERE column2 = v2 and column3 = v3;
	```

		1. PostgreSQL will consider using the index, but scanning the whole index may have a higher cost than other options
			1. Planner evaluates different execution paths
				1. If index scan is not the most efficient, it may choose a sequential scan
8. We can use `WHERE` clause to define a partial multicolumn index
	1. Index on multiple columns that only includes rows satisfying a given condition

### PostgreSQL Multicolumn Index Example ###
1. New `people` table:

```sql
CREATE TABLE people (
  id INT GENERATED BY DEFAULT AS IDENTITY,
  first_name VARCHAR (50) NOT NULL,
  last_name VARCHAR (50) NOT NULL
);
```

2. Execute [script with 10000 rows](https://neon.com/postgresqltutorial/Script-to-load-10000-names.txt)
3. Show the query plan that finds the person whose last name is `Adams`:

```sql
EXPLAIN
SELECT
  id,
  first_name,
  last_name
FROM
  people
WHERE
  last_name = 'Adams';
```

	1. Performs sequential scan because there is no index.
4. Multi-column index:

```sql
CREATE INDEX idx_people_names
ON people (last_name, first_name);
```

5. Show the plan again:

```sql
EXPLAIN
SELECT
  id,
  first_name,
  last_name
FROM
  people
WHERE
  last_name = 'Adams';
```

	1. Uses `idx_people_names`
6. Find a person whose first name is `Lou` and last name is `Adams`:

```sql
EXPLAIN
SELECT
  id,
  first_name,
  last_name
FROM
  people
WHERE
  last_name = 'Adams'
  AND first_name = 'Lou';
```

	1. Uses `idx_people_names`
		1. Because both are includes in the index
7. Search for a person whose first name is `Lou`:

```sql
EXPLAIN
SELECT
  id,
  first_name,
  last_name
FROM
  people
WHERE
  first_name = 'Lou';
```

	1. Seq scan
		1. First column is not constrained
			1. Using the index would require scanning all the entries, so planner determined that seq scan on table was more efficient.

### Summary ###
1. Multicolumn index to define an index involving two or mroe columns from a table.
2. Place the columns that are frequently used in the `WHERE` clause at the beginning of the column list of the multicolumn index.

## PostgreSQL REINDEX ##
1. Summary: `REINDEX` is used to rebuild one or more indexes.

### Introduction to PostgreSQL REINDEX statement ###
1. Index may become corrupted and no longer contain valid data due to hardware failures or software bugs.
2. If we don't use `CONCURRENTLY` option, the index may be invalid if the index build fails.
3. If an index gets corrupted, we can rebuild the index using `REINDEX`

```sql
REINDEX [ (option, ...) ]
{ INDEX | TABLE | SCHEMA | DATABASE | SYSTEM }
name;
```

	1. `option` can be
		1. `VERBOSE [boolean]` - Show the progress as each index is reindexed
		2. `TABLESPACE new_tablespace` - specify the new tablespace on which the indexes will be rebuilt
		3. `CONCURRENTLY` - rebuild the index without taking any locks
			1. If not use, reindex will lock out writes but not reads on the table until it is completed
4. To rebuild a single index:

```sql
REINDEX INDEX index_name;
```

5. To rebuild all the indexes of a table, use `TABLE` keyword and specify the name of the table:

```sql
REINDEX TABLE table_name;
```

6. To rebuild all indexes in a specific schema, use `SCHEMA` keyword followed by schema name:

```sql
REINDEX SCHEMA schema_name;
```

7. To rebuild all indexes in a specific database, specify database name after `REINDEX DATABASE`:

```sql
REINDEX DATABASE database_name;
```

8. To re-generate all indexes on system catelogs in a specific database:

```sql
REINDEX SYSTEM database_name;
```

### PostgreSQL REINDEX example ###
1. Rebuild all indexes in the `film` table of `dvdrental` databse using the `REINDEX` statement:

```sql
REINDEX (VERBOSE, CONCURRENTLY)
TABLE film;
```

	1. Displays progress report after an index is rebuilt successfully
	2. `CONCURRENTLY` - do not use any locks while rebuilding the index
2. Rebuild all indexes in the `dvdrental` database using the `REINDEX` statement:

```sql
REINDEX DATABASE dvdrental;
```

### REINDEX vs. DROP INDEX & CREATE INDEX ###
1. `REINDEX` rebuilds the index from scratch
	1. Similar effect as dropping and reconstructing the index
		1. But, the locking mechanisms between them are different.
2. `REINDEX`
	1. Lock write but not read from the table to which the index belongs
	2. Take an exclusive lock on the index that is being processed
		1. Blocks the read that attempts to use the index
3. `DROP INDEX`, and `CREATE INDEX`
	1. `DROP INDEX` locks both writes and reads of the table to which the index belongs by acquring an exclusive lock on the table
	2. `CREATE INDEX` locks out writes but not reads from the index's parent table
		1. Reads may be expensive during the creation of the index

### Summary ###
1. `REINDEX` - to drop and recreate one or more indexes.

## PostgreSQL DROP INDEX ##
1. Summary: `DROP INDEX` - to remove an existing index

### Introduction to PostgreSQL DROP INDEX statement ###
1. Syntax:

```sql
DROP INDEX [ CONCURRENTLY ] [ IF EXISTS ] index_name
[ CASCADE | RESTRICT ];
```

	1. `IF EXISTS` - attempting to remove a non-existing index will result in an error
		1. If index doesn't exist, PostgreSQL will issue a notice instead.
	2. `CASCADE` - If index has dependent objects, use `CASCADE` option to automatically drop the objects and all objects that depend on the objects.
	3. `RESTRICT` - Instructs PostgreSQL to refuse to drop the index if any objects depend on it.
		1. Default
2. Syntax to drop multiple indexes:

```sql
DROP INDEX index_name, index_name2, ...;
```

#### CONCURRENTLY ####
1. By default, `DROP INDEX` forces PostgreSQL to acquire an exclusive lock on the table and blocks other accesses until the index removal is complete.
	1. To force the command to wait until conflicting transaction completes before removing the index, use `CONCURRENTLY` option
	2. Limitations:
		1. `CASCADE` option is not supported
		2. Executing in a transaction block is not supported

### PostgreSQL DROP INDEX example ###
1. `actor` table:
2. New index:

```sql
CREATE INDEX idx_actor_first_name
ON actor (first_name);
```

3. Sometime query optimizer does not use the index
	1. Example:
	
	```sql
	SELECT * FROM actor
	WHERE first_name = 'John";
	```
	
4. Explain:

```sql
EXPLAIN
SELECT * FROM actor
WHERE first_name = 'John";
```

	1. Reason: The query optimizer thinks that it is more optimal to just scan the entire table to locate the row.
		1. The index can be dropped
		
		```sql
		DROP INDEX idx_actor_first_name;
		```

### Summary ###

## PostgreSQL List Indexes ##
1. Summary: Listing indexes using `pg_indexes` view or `psql` command.
	1. No `SHOW INDEXES`
2. `psql` - `\d` **(M)** to view all indexes.

### PostgreSQL List Indexes using pg_indexes View ###
1. `pg_indexes` view allows us to access useful info on each index in the PostgreSQL database.
	1. It has five columns:
		1. `schemaname`: Stores name of schema that contains tables and indexes
		2. `tablename`: Names of tables to which index belongs
		3. `indexname`: represents the name of the index
		4. `tablespace`: Name of the tablespace that contains indexes
		5. `indexdef`: Index definition command in the form of `CREATE INDEX`
2. Displaying all indexes of schema `public`

```sql
SELECT
  tablename,
  indexname,
  indexdef
FROM
  pg_indexes
WHERE
  schemaname = 'public'
ORDER BY
  tablename,
  indexname;
```

3. To show all indexes of a table:

```sql
SELECT
  indexname,
  indexdef
FROM
  pg_indexes
WHERE
  tablename = 'table_name';
```

4. Example:

```sql
SELECT
  indexname,
  indexdef
FROM
  pg_indexes
WHERE
  tablename = 'customer';
```

5. TO get a list of indexes for tables whose names start with the letter `c`:

```sql
SELECT
  tablename,
  indexname,
  indexdef
FROM
  pg_indexes
WHERE
  tablename LIKE 'c%'
ORDER BY
  tablename,
  indexname;
```

### PostgreSQL List Indexes using psql command ###
1. `\d` command:

```sql
\d table_name
```

	1. All info about the table including
		1. Table's structure
		2. Indexes
		3. Constraints
		4. Triggers
		
2. Example: `\d customer`

### Summary ###

## PostgreSQL Index Types ##
1. Summary: Various PostgreSQL index types and how to use them
2. Types:
	1. B-tree
	2. Hash
	3. GiST
	4. SP-GiST
	5. GIN
	6. BRIN
3. Each index type uses a different storage structure and algorithm to cope with different kinds of queries
	1. B-tree index type is the default
		1. It is the best fit for most common queries

### B-tree indexes ###
1. B-tree is a self-balancing tree that maintains sorted data and allows searches, insertions, deletions, and sequential access in logarithmic time.
2. Query planner will consider using B-tree index when index columns are involved in a comparison that uses one of the following:

```
<
<=
=
>=
BETWEEN
IN
IS NULL
IS NOT NULL
```

3. Additionally, query planner can use B-tree index for queries that involve a pattern-matching operator `LIKE` and `~`, if the pattern is a constant and is anchor at the beginning of the pattern:

```sql
column_name LIKE 'foo%'
column_name LIKE 'bar%'
column_name ~ '^foo'
```

4. B-tree is considered for `ILIKE` and `~*` if patterns starts with non-alphabtic character (characters not affected by upper/lower case conversion)

### Hash indexes ###
1. Hash indexes can handle only simple equality comparison (`=`)
	1. Whenever an indexed column is involved in a comparison using the `=` operator, query planner will consider using a hash index
2. Syntax:

```sql
CREATE INDEX index_name
ON table_name USING HASH (indexed_column);
```

### GIN indexes ###
1. GIN: Generalized inverted indexes
2. Useful when we have multiple values stored in a single column
	1. `hstore`
	2. `array`
	3. `jsonb`
	4. Range types

### BRIN ###
1. Block Range Indexes
	1. Much smaller
	2. Less costly to maintain (as compared to B-tree)
2. Allows using index on a very large table that would be impractical with a B-tree without horizontal partioning
3. Usually used on a column that has a linear sort order
	1. created date column or sales order table

### GiST Indexes ###
1. Generalized Search Tree
	1. General tree structures
		1. Useful for geometric data types
		2. Useful for full-text search

### SP-GiST Indexes ###
1. Space-Partitioned GiST
	1. Supports partitioned search trees
		1. Facilitate the development of a wide range of different non-balanced data structures
2. For data that has a natural clustering element to it & not an equally balanced tree
	1. Example:
		1. GIS
		2. Multimedia
		3. Phone routing
		4. IP routing

## PostgreSQL Full Text Search ##
1. Summary: Full text search. How to use it to perform complex searches on text stored in the database.

### Introduction to the PostgreSQL full-text search ###
1. It is a built-in feature that allows us to perform complex searches on text stored in the database.
	1. It enables efficient searching of documents, articles, or any form of text-based content by indexing their words and phrases.
		1. Overview of how it works:
			1. Indexing: We can construct indexes on columns with `tsvector` data type
				1. PostgreSQL analyzes text data and generates a specifialized data structure calls `tsvector`, which represents the indexed document in a format optimized for searches.
			2. Text analysis: Text analysis process involves tokenizing text into individual words or tokens, removing stop words (like `the`, `and`, ...), applying stemming (or lemmatization) to reduce words to their root form, and performing other lingquistic transformations to prepare the text for indexing.
			3. Querying: After PostgreSQL generates a full text index, you can perform full-text search queries using dedicatd full text search functiosn and operators.
				1. Example: Searching for specific words or phrases
				2. Example: Apply boolean operators to combine terms
				3. ...
			4. Ranking: Allows us to rank the search results based on their relevance to the query
				1. `ts_rank()` - function to calculate a rank score for each document based on its similarity to the search query.
					1. The ranking feature can be used to sort the search results based on relevance
			5. Highlighting: PostgreSQL can generate snippets or summaries of documents containing the matching words from the search query.
2. Use-cases: For fast searches on a large volumne of text
	1. Content management systems (CMS)
	2. Document management systems
	3. ...

### PostgreSQL full text search data types ###
1. Two data types:
	1. `txvector`
	2. `tsquery`

#### tsvector ####
1. `tsvector` - data type that allows us to store preprocessed documents in a format optimized for efficient searching and retrieval of text.
	1. It contains a sorted list of lexemes (words) and their positions and weight within a document.
		1. Lexemes are words without the variation created by suffixes
			1. Example: `watch` for `watches`, `watched`, and `watching`
				1. To convert to `tsvector`
				
				```sql
				SELECT 
				  to_tsvector('watches'),
				  to_tsvector('watched'),
				  to_tsvector('watching');
				```
				
				```
				'watch':1 | 'watch':1 | 'watch':1
				```
				
			2. Example: Convert a string to a `tsvector` value:
			
			```sql
			SELECT to_tsvector('The quick brown fox jumps over the lazy dog.');
			```
			
			```
			"'brown':3 'dog':9 'fox':4 'jump':5 'lazi':8 'quick':2"
			```
			
				1. Each entry is a word (lexeme) & its position within the string (or document)
				2. Words are sorted in alphabetical order
				3. Articles and stop words are omitted like `The`, and `over`

#### tsquery ####
1. A data type that represents search queries in full-text searches
2. It allows us to specify search conditions containing the indexed document's words or phrases
3. It can also include search operators to refine the search conditions
	1. Boolean operators - Used to combine search terms and define logical relationships between them
		1. AND (&)
		2. OR (|)
		3. NOT (!)
	2. Phrase search - "" indicates that the enclosed words must appear together in the index document in the specified order
	3. Prefix search - : after a word indicates that the serach term should match words with the same prefix
	4. Negation - `-` excludes specific terms from the search results
	5. Grouping: `()` group terms and operators to define flexible search conditions
4. Example: `'quick' & 'brown' | 'fox'`
	1. The `tsquery` searches for docuemnts that contain the words 'quick' and 'brown' together (in any order), or the word 'fox'
5. `to_tsquery()` converts a string to a `tsquery`

```sql
SELECT to_tsquery('jumping');
``` 

	1. `jump`

### The match operator (@@) ###
1. `@@` - Evaluates the similarity between the text in a document (`tsvector`) and the terms specified in the search query (`tsquery`) and returns true if there is a match or false otherwise
2. Syntax:

```sql
tsvector @@ tsquery
```

3. Example:

```sql
SELECT
  to_tsvector(
    'The quick brown fox jumps over the lazy dog.'
  ) @@ to_tsquery('jumping') result;
```

	1. `tsvector` contains `jump`

### Using PostgreSQL full-text search index with table data ###
#### Setting up a sample table ####
1. `posts` table:

```sql
CREATE TABLE posts (
  id SERIAL PRIMARY KEY,
  title TEXT NOT NULL,
  body TEXT,
  body_search TSVECTOR
    GENERATED ALWAYS AS (to_tsvector('english', body)) STORED
);
```

	1. `body_search` is a generated column with data type `tsvector`
	2. Whenever we change `body`, PostgreSQL will convert it to a `tsvector` using the `to_tsvector()` function and store it in `body_search` column
2. Insert some rows:

```sql
INSERT INTO posts (title, body)
VALUES
  ('Introduction to PostgreSQL', 'This is an introductory post about PostgreSQL. It covers basic concepts and features.'),
  ('Advanced PostgresSQL Techniques', 'In this post, we delve into advanced PostgreSQL techniques for efficient querying and data manipulation.'),
  ('PostgreSQL Optimization Strategies', 'This post explores various strategies for optimizing PostgreSQL database performance and efficiency.');
```

3. Retrieve the data:

```sql
SELECT
  id,
  body_search
FROM
  posts;
```

#### Simple full-text search ####
1. Use `@@` operator to search for posts whose `body` contains the word `'PostgreSQL'`

```sql
SELECT
  id,
  body
FROM
  posts
WHERE
  body_search @@ to_tsquery('PostgreSQL');
```

#### Full-text search with AND operator ####
1. `&` to search for posts whose body contains both words 'PostgreSQL' and 'techniques' that can appear in any order:

```sql
SELECT
  id,
  body
FROM
  posts
WHERE
  body_search @@ to_tsquery('PostgreSQL & techniques');
```

#### Full-text search with OR operator ####
1. `|` to search for posts whose body contains either `'efficient'` or `'optimization'`:

```sql
SELECT
  id,
  body
FROM
  posts
WHERE
  body_search @@ to_tsquery('efficient | optimizations');
```

#### Full-text search with phrase ####
1. Searches posts whose body contains the phrase `'PostgreSQL technique'`:

```sql
SELECT
  id,
  body
FROM
  posts
WHERE
  body_search @@ to_tsquery('''PostgreSQL technique''');
```

#### FUll-text search with negation ####
1. Searching for posts whose body does not contain the word 'efficient':

```sql
SELECT
  id,
  body
FROM
  posts
WHERE
  NOT body_search @@ to_tsquery('efficient');
```

### Full text search using GIN indexes ###
1. GIN: Generalized Inverted Index
	1. It is optimized for full-text search vectors (`tsvector`)
2. Drop the `posts` table and re-generate using the following statement:

```sql
DROP TABLE IF EXISTS posts;

CREATE TABLE posts (
  id SERIAL PRIMARY KEY,
  title TEXT NOT NULL,
  body TEXT
);
```

3. Insert rows;

```sql
INSERT INTO posts (title, body)
VALUES
    ('Introduction to PostgreSQL', 'This is an introductory post about PostgreSQL. It covers basic concepts and features.'),
    ('Advanced PostgresSQL Techniques', 'In this post, we delve into advanced PostgreSQL techniques for efficient querying and data manipulation.'),
    ('PostgreSQL Optimization Strategies', 'This post explores various strategies for optimizing PostgreSQL database performance and efficiency.');
```

4. Generate GIN index on the `body` column:

```sql
CREATE INDEX body_fts
ON posts
USING GIN (to_tsvector('english', body));
```

5. Search for `posts` whose body contains either the word `basic` or `advanced`:

```sql
SELECT
  id,
  body
FROM
  posts
WHERE
  to_tsvector('english', body) @@ to_tsquery('basic | advanced');
```

### Summary ###
1. Full text search for complex searches on text stored in the db.
2. `tsvector` and `tsquery` data types for full text searchs
3. Use `@@` to check if documents match a query
4. Use generated column with `tsvector` type to store the tsvector data for full text searches
5. Use GIN indexes for full-text search vectors (`tsvector`)

## PostgreSQL JSON Index ##
1. Summary: How to construct JSON index for a JSONB column to improve query performance.

### Introduction to PostgreSQL JSON index ###
1. JSONB - Binary JSON 
	1. Allows us to store JSON data and query it efficiently.
2. Usecase - When a JSON column has a complex JSON structure, utilizing an index can significantly improve query performance
	1. GIN index type is used for JSONB data type
		1. GIN can be used for `tsvector` or array columns.
3. Creation of GIN index for JSONB column:

```sql
CREATE INDEX index_name
ON table_name
USING GIN (jsonb_column);
```

	1. GIN index is suitable for general-purpose queries on JSONB data
4. Operator class determines how PostgreSQL builds the index and how it optimizes the queries on the indexed column
	1. Example: Using `jsonb_path_ops` operator class
	
	```sql
	CREATE INDEX index_name
	ON table_name
	USING GIN (jsonb_column, jsonb_path_ops);
	```
	
		1. Index is optimized for queries that use `@>` (contains), `?` (exists), and `@@` JSONB operators.
			1. Useful for searches involving keys and values within JSONB documents.
5. GIN operator classes:
	1. `array_ops`
		1. `&& (anyarray, anyarray)` - indexable operator 
		2. `@> (anyarray, aryarray)`
		3. `<@ (anyarray, aryarray)`
		4. `= (anyarray, anyarray)`
	2. `jsonb_ops`
		1. `@> (jsonb, jsonb)`
		2. `@? (jsonb, jsonpath)`
		3. `@@ (jsonb, jsonpath)`
		4. `? (jsonb, text)`
		5. `?| (jsonb, text[])`
		6. `?@ (jsonb, text[])`
	3. `jsonb_path_ops`
		1. `@> (jsonb, jsonb)`
		2. `@? (jsonb, jsonpath)`
		3. `@@ (jsonb, jsonpath)`
	4. `tsvector_ops`
		1. `@@ (tsvector, tsquery)`
6. `json_ops` operator is default
	1. Suitable for most cases
7. GIN index can be created for specific field in JSON documents

```sql
CREATE INDEX index_name
ON table_name
USING GIN ((data->'field_name') jsonb_path_ops);
```

### PostgreSQL JSON index examples ###
#### Setting up a sample table ####
1. New `customer_json` table:

```sql
CREATE TABLE customer_json (
  id SERIAL PRIMARY KEY,
  data JSONB NOT NULL
);
```

2. Insert data from `customer`, `address`, `city`, and `country` tables into `customer_json` table:

```sql
WITH json_cte AS (
  SELECT
    jsonb_build_object(
	  'first_name', first_name,
	  'last_name', last_name,
	  'email', email,
	  'phone', phone,
	  'address',
	  jsonb_build_object(
	    'address', a.address,
		'city', i.city,
		'postal_code', a.postal_code,
		'district', a.district,
		'country', o.country
	  )
	)::jsonb AS data
  FROM
    customer c
	INNER JOIN address a ON a.address_id = c.address_id
	INNER JOIN city i ON i.city_id = a.city_id
	INNER JOIN country o ON o.country_id = i.country_id
)
INSERT INTO customer_json (data)
SELECT
  data 
FROM
  json_cte;
```

3. Retrieve email of the customer whose first name is 'John':

```sql
SELECT
  data ->> 'first_name' first_name,
  data ->> 'last_name' last_name,
  data ->> 'phone' phone
FROM
  customer_json
WHERE
  data @> '{"first_name": "John"}';
```

4. Explain:

```sql
EXPLAIN ANALYZE
SELECT
  data ->> 'first_name' first_name,
  data ->> 'last_name' last_name,
  data ->> 'phone' phone
FROM
  customer_json
WHERE
  data @> '{"first_name": "John"}';
```

#### Constructing an index on the JSONB column ####
1. Sequential scan of the entire customer_json table
	1. Solution: GIN index on the `data` column:
	
	```sql
	CREATE INDEX idx_customer_json_data
	ON customer_json
	USING GIN (data);
	```
	
2. Re-execute the query:
	1. Bitmap Heap Scan on customer_json

#### Constructing an index on the JSONB column with the GIN operator class ####
1. Drop the GIN index

```sql
DROP INDEX idx_customer_json_data;
```

2. GIN index with an operator class:

```sql
CREATE INDEX idx_customer_json_data 
ON customer_json
USING GIN (data jsonb_path_ops);
```

3. Explain:
	1. Improved performance
4. Explain the query that search for the customer where the vlaue in `first_name` is `=` `John':

```sql
EXPLAIN ANALYZE
SELECT * FROM customer_json
WHERE data->>'first_name' = 'John';
```

	1. Query cannot fully utilize GIN index.
		1. Query does not use JSONB operators `@`, `@?`, and `@@` that `jsonb_path_ops` operator class is optimized for.

#### Constructing an index on a specific field of a JSONB column ####
1. Drop the existing index:

```sql
DROP INDEX idx_customer_json_data;
```

2. GIN index on the `first_name` field of `customer_json` table using `GIN` operator class:

```sql
CREATE INDEX idx_customer_json_data
ON customer_json
USING GIN ((data->'first_name'));
```

3. Explain the query that finds rows where `first_name` field in the `data` JSONB column contains the value `John`:

```sql
EXPLAIN ANALYZE
SELECT
  data ->> 'first_name' first_name,
  data ->> 'last_name' last_name,
  data ->> 'phone' phone
FROM
  customer_json
WHERE
  data->'first_name' @> '"John"';
```

### Summary ####

---

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

---

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