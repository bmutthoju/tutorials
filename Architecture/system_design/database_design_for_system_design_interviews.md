1. For a system design interview, it is important to have a good understanding of the following database concepts:
	1. **Relational databases:** It is important to have a good understanding of the **relational model**, including **tables**, **rows**, **columns**, **primary keys**, **foreign keys**, and **normalization**.
	2. **SQL:** Knowledge of SQL, the standard language for interacting with relational databases, is crucial. You should be familiar with basic **SQL** commands such as **SELECT**, **INSERT**, **UPDATE**, **DELETE**, **JOIN**, and **GROUP BY**.
	3. **Database Design:** Understanding how to design a relational database, including the **process of normalization** to reduce **data redundancy** and improve **data integrity**.
	4. **Indexing:** Understanding how indexing works and the **trade-offs between different types of indexes**, such as **B-trees**, **hash tables**, and **inverted indexes**.
	5. **ACID Properties:** Understanding the **ACID** (**Atomicity**, **Consistency**, **Isolation**, **Durability**) properties of **transactions** in relational databases, and **how they ensure data consistency and reliability**.
	6. **Data Sharding:** Understanding how to **horizontally scale a database** by **sharding data across multiple machines**.
	7. **NoSQL databases:** Familiarity with NoSQL databases, such as **MongoDB** and **Cassandra**, and the **differences between relational and NoSQL databases.
	8. **Caching:** Understanding how to improve database performance by **caching frequently accessed data**.
	9. **Distributed systems:** Understanding the basics of distributed systems and how they relate to databases, such as **consistency models**, **distributed transactions**, and **distributed locks**.
2. These are the key database concepts that you should be familiar with for a system design interview. Of course, the specific requirements and expectations may vary depending on the company and the role you are interviewing for.

## What caching techniques exist to improve database performance? ##
1. There are several caching techniques that can be used to improve the performance of a database:
	1. **Query caching:** Query caching is a technique where the results of a query are stored in memory and reused for subsequent requests. This reduces the overhead of executing the same query multiple times.
	2. **Page caching:** Page caching is a technique where the data of frequently accessed pages is stored in memory. This reduces the overhead of reading the same data from disk multiple times.
	3. **Object caching:** Object caching is a technique where frequently used objects are stored in memory. This reduces the overhead of instantiating the same objects multiple times.
	4. **Full-page caching:** Full-page caching is a technique where entire pages are cached in memory, reducing the overhead of executing the logic to generate the pages from scratch.
	5. **In-memory databases:** In-memory databases store all data in RAM, providing fast access times and low latency. This can significantly improve the performance of a database compared to traditional disk-based databases.
	6. **Distributed caching:** Distributed caching is a technique where the cache is **spread across multiple nodes**, allowing for improved scalability and availability.
	7. **Materialized views:** Materialized views are precomputed aggregates, summaries, or other transformations of data that can be stored and used to speed up queries.
2. Each of these techniques has its own trade-offs and benefits, and the most appropriate caching technique to use will depend on the specific requirements and constraints of your database application.

## What approach to follow to normalize a relational database? ##
1. Normalizing a relational database involves organizing the data into separate tables **to minimize data redundancy** and **dependency**. Here is a general approach to follow when normalizing a database:
	1. **Identify the entities:** The first step is to identify the **entities** that the database will store data about. These entities can be **people**, **products**, **orders**, etc. Each entity will become a table in the database.
	2. **Identify the attributes:** For each entity, identify the **attributes** that describe it. These attributes will become the columns in the corresponding table.
	3. **Construct the initial table:** Create a table for each entity, including the columns for each attribute.
	4. **Remove repeating groups:** If there is a repeating group of data in any of the tables, extract the **repeating group** into a separate table.
	5. **Remove partial dependencies:** If a **non-key attribute** depends on only a **part of the primary key**, extract the non-key attribute into a separate table.
	6. **Remove transitive dependencies:** If a **non-key attribute** depends on another non-key attribute, extract the dependent attribute into a separate table.
	7. **Normalize to third normal form (3NF):** Repeat the process of removing **repeating groups**, **partial dependencies**, and **transitive dependencies** until the database is in **third normal form (3NF)**.
	8. **Test the design:** After normalizing the database, test the design to ensure that it meets the requirements and constraints of the application.
	9. **Refine the design:** If necessary, refine the design based on the results of the testing.
2. This approach provides a systematic way to normalize a relational database, reducing data redundancy and increasing data integrity. However, it is important to keep in mind that normalization is not an end in itself, and there may be cases where normalization is not the best approach. It's important to understand the trade-offs between normalization and performance, and to choose the right balance for your specific application.

## Why should we remove transitive dependencies during normalization? ##
1. Removing transitive dependencies during normalization is important because it helps to eliminate redundant data, reduce data anomalies, and ensure data integrity.
2. A transitive dependency occurs when a non-key attribute depends on another non-key attribute. This creates a situation where the value of one attribute determines the value of another attribute, and changes to one attribute can result in changes to another attribute. This creates a situation where data can become inconsistent, which can lead to data anomalies, such as insertion, update, and deletion anomalies.
3. By removing transitive dependencies, you can create separate tables for the dependent attributes, and ensure that each attribute is dependent only on the primary key of its own table. This reduces data redundancy, and eliminates the risk of data anomalies.
4. Additionally, removing transitive dependencies makes it easier to maintain the database over time, as changes to one attribute will not affect another attribute. This improves data integrity, and reduces the risk of data corruption or loss.
5. Overall, removing transitive dependencies during normalization is an important step in ensuring the reliability and integrity of a relational database, and is a key part of the normalization process.

## Give an example of transitive dependency. ##
1. Here is an example of a transitive dependency:
2. Consider a table that stores information about students and the courses they are enrolled in. The table has the following columns:

		student_id, student_name, course_id, course_name, instructor_name

3. In this example, the "instructor_name" attribute is a transitive dependency, as it depends on the "course_name" attribute, which in turn depends on the primary key of the table, "student_id" and "course_id". This creates a situation where changes to the "course_name" attribute can result in changes to the "instructor_name" attribute, which can lead to data anomalies.
4. To remove this transitive dependency, you could create a separate table for the courses, with the following columns:

		course_id, course_name, instructor_name

5. And update the original table to include only the student information:

		student_id, student_name, course_id

6. By doing this, you have separated the attributes into separate tables, eliminating the transitive dependency and reducing the risk of data anomalies.

## What kind of problems can occur due to partial dependencies? ##
1. There are several problems that can occur due to partial dependencies in a database:
	1. **Data redundancy:** Partial dependencies can lead to data redundancy, where the same information is stored in multiple places. This can lead to increased storage requirements and decreased efficiency.
	2. **Data anomalies:** When data is stored redundantly, there is a risk of data anomalies, where different versions of the same data can become inconsistent. For example, if the salary for an employee is stored in two different tables and one of them is updated but the other is not, the data will become inconsistent.
	3. **Decreased data integrity:** With partial dependencies, it is more difficult to ensure the integrity of the data, as changes made to one piece of data can have unintended consequences on other pieces of data.
	4. **Increased complexity:** A database with partial dependencies can become more complex, making it more difficult to understand and maintain.
	5. **Decreased performance:** Queries on a database with partial dependencies can become more complex and take longer to execute, leading to decreased performance.
2. By removing partial dependencies during normalization, you can avoid these problems and ensure that your database is organized, efficient, and easy to maintain.

## Give example of data redundancy occurring due to partial dependencies. ##
1. Consider the following table:

		Orders (order_id, customer_name, product, quantity, price)

2. In this table, the price of a product depends only on the product attribute and not on the order_id. This means that the price of a product will be repeated for every order that includes that product. This leads to data redundancy, as the same information (the price of a product) is stored multiple times in the table.

		order_id | customer_name | product | quantity | price
		---------------------------------------------------
		1        | John Doe      | Apple   | 2        | 1.00
		2        | Jane Doe      | Apple   | 1        | 1.00
		3        | John Doe      | Banana  | 3        | 0.50
		4        | Jane Doe      | Apple   | 4        | 1.00

3. In this example, the price of the product "Apple" is repeated three times in the table, leading to data redundancy. This can become a problem if the price of the product changes, as it would need to be updated in multiple places in the table.
4. To eliminate this redundancy, we can create a separate table for products and their prices:

		Orders (order_id, customer_name, product, quantity)
		Products (product, price)

5. With this approach, the information about the price of a product is stored in a single place, reducing data redundancy and improving the overall efficiency and integrity of the database.

## What is 3NF? ##
1. 3NF, or Third Normal Form, is a level of database normalization that is used to eliminate data redundancy and improve **data integrity**. It builds upon the concepts of First Normal Form (1NF) and Second Normal Form (2NF), which specify that data should be stored in a tabular format and that each non-key attribute should depend on the entire primary key, respectively.
2. The main goal of 3NF is to eliminate transitive dependencies, which occur when an attribute depends on another non-key attribute, rather than the primary key. In other words, 3NF requires that all non-key attributes should depend directly on the primary key.
3. To achieve 3NF, a database must satisfy the following conditions:
	1. The database must already be in 2NF.
	2. There should be no transitive dependencies, meaning that each non-key attribute should depend directly on the primary key.
	3. There should be no redundant data.
4. By following these conditions, 3NF helps to ensure that a database is organized, efficient, and free of data anomalies. This makes it easier to maintain and update the database, and it reduces the risk of data inconsistencies and inaccuracies.

## What is data integrity? ##
1. Data integrity refers to the accuracy, completeness, and consistency of data stored in a database. It is an important aspect of database management, as it ensures that the data stored in the database is reliable and trustworthy.
2. Data integrity can be maintained through various means, including:
	1. **Validation checks:** Validation checks ensure that data entered into the database is in the correct format and meets certain criteria. For example, a database may have a rule that the value of a certain field must be within a certain range.
	2. **Constraints:** Constraints are rules that are enforced by the database management system to maintain the integrity of the data. For example, a database may have a constraint that ensures that a certain field cannot be empty.
	3. **Normalization:** Normalization is the process of organizing data in a database so that it is free from **redundancy** and **anomalies**. By following the normalization rules, a database can maintain its data integrity.
	4. **Transactions:** Transactions allow multiple actions to be grouped together into a single, all-or-nothing operation. This helps to ensure that the data remains consistent, even in the event of a system failure or other error.
3. By maintaining data integrity, a database can ensure that its data is accurate, reliable, and trustworthy. This, in turn, helps to support the decision-making process and other operations that rely on the data stored in the database.

## What is anamoly? ##
1. A person or thing that is different from what is usual, or not in agreement with something else and therefore not satisfactory

## What is data anamoly? ##
1. Data anomaly refers to an inconsistent or unexpected state of data in a database. It can occur when data is inserted, updated, or deleted in an unintended or unexpected way. There are several types of data anomalies that can occur in a database, including:
	1. **Insert Anomaly:** This occurs when it is not possible to insert a new data item into the database without violating the rules of the database. For example, **if a database has a constraint that a certain field must be filled, an insert anomaly would occur if an attempt was made to insert a new data item without a value in that field.**
	2. **Update Anomaly:** This occurs when a change to one piece of data in a database leads to unexpected or unintended changes to other pieces of data. For example, **if a customer's name is changed in one table, but not in another table where the customer's name is also stored, an update anomaly would occur.**
	3. **Delete Anomaly:** This occurs when deleting a piece of data from a database leads to unexpected or unintended consequences. For example, **if a customer is deleted from a database but their orders are not, an delete anomaly would occur.**
2. Data anomalies can cause problems in a database, such as decreased data integrity and accuracy, and can lead to incorrect results when data is queried. To avoid data anomalies, it is important to follow good database design practices, such as normalization, and to enforce constraints and validation checks.

## Explain the isolation techniques in detail. ##
1. There are several techniques used to implement the isolation property in a database management system. Here are some of the most common techniques:
	1. **Locking:** Locking is the most basic technique for implementing isolation in a database. It works by allowing only one transaction to access a specific data item at a time, and preventing other transactions from accessing that data item until the first transaction has completed. There are several types of locks, including **shared locks**, **exclusive locks**, and **read locks**, each of which provides a different level of isolation.
	2. **Versioning:** Versioning is a technique that creates multiple versions of a data item, each version representing a different state of the data item. When a transaction modifies a data item, a new version of the data item is created, rather than modifying the existing version. This means that multiple transactions can access different versions of the same data item at the same time, without interfering with each other.
	3. **Multi-Version Concurrency Control (MVCC):** MVCC is a technique that is based on versioning, but provides a more sophisticated way of managing the versions of a data item. In MVCC, each transaction has its own view of the data, based on the version of the data that was current when the transaction started. This means that transactions can access and modify data without blocking each other, even if they are accessing the same data item.
	4. **Serializable Snapshot Isolation (SSI):** SSI is a technique that provides a high level of isolation by executing transactions in a serial order, and allowing each transaction to access a snapshot of the data that was current when the transaction started. This means that transactions cannot interfere with each other, even if they are accessing the same data item, and the results of each transaction are consistent and accurate.
	5. **Read Committed:** Read committed is a level of isolation that ensures that each transaction only sees data that has been committed by other transactions. This means that a transaction will not see any intermediate results that have been modified by other transactions, but have not yet been committed.
2. The choice of isolation technique will depend on the specific needs of the application, the types of transactions being executed, and the desired level of isolation. In general, the more isolation that is required, the greater the impact on performance and scalability, so it is important to choose an isolation technique that provides the required level of isolation, while also providing good performance and scalability.

## How is conflict resolved with versioning technique used to implement isolation in ACID? ##
1. In the context of databases and ACID (Atomicity, Consistency, Isolation, Durability) transactions, versioning can be used to implement isolation and resolve conflicts. The idea behind this approach is to keep multiple versions of a database item, each representing a different state of the item at different points in time.
2. When a transaction modifies a database item, it creates a new version of that item instead of overwriting the existing version. The transaction operates on this new version, and if it successfully commits, the new version becomes the current version of the item. If the transaction fails to commit, the new version is discarded, and the original version remains unchanged.
3. This versioning technique helps to ensure that each transaction operates on its own version of the database items, and that the changes made by one transaction do not interfere with the changes made by another transaction. This way, multiple transactions can run concurrently without any conflicts, and each transaction can operate in complete isolation from the others.
4. When a conflict does arise, the database can use a conflict resolution algorithm to determine which version of the item should be kept as the current version. For example, it might choose the most recent version, the version created by the transaction with the highest priority, or the version created by a transaction that was executed first.
5. In summary, versioning can be used to implement isolation in ACID by creating multiple versions of a database item and ensuring that each transaction operates on its own version. This helps to resolve conflicts and ensure that the database remains consistent and free of errors.

## What conflict resolution algorithms are used to resolve conflicts? ##
1. Conflict resolution algorithms are used to determine the outcome of a conflict in a version control system, a database, or any other system that involves multiple conflicting changes. Some common conflict resolution algorithms include:
	1. **Last Writer Wins (LWW):** In this algorithm, the most recently written version of an item is considered to be the authoritative version, and any conflicting changes are discarded. This algorithm is often used in distributed systems where latency and network issues can cause delays in propagating changes to all nodes.
	2. **First Writer Wins (FWW):** This algorithm is the opposite of LWW, and it considers the first written version of an item to be the authoritative version, discarding any conflicting changes that occur later. This algorithm is often used in systems where data consistency is a higher priority than preserving the latest changes.
	3. **Majority Wins:** In this algorithm, the version of an item that is written by the majority of nodes in a distributed system is considered to be the authoritative version. This algorithm is often used in voting systems or in situations where multiple nodes must reach consensus on the correct version of an item.
	4. **Manual Resolution:** In some cases, conflict resolution must be performed manually, either by a user or by a system administrator. This often involves reviewing the conflicting changes and determining which changes should be kept and which should be discardded.
	5. **Hybrid Approaches:** Some systems use a combination of the above algorithms, applying different algorithms in different situations depending on the nature of the conflict and the priorities of the system.
2. The choice of conflict resolution algorithm depends on the specific requirements and constraints of a system, and it can have a significant impact on the consistency, correctness, and performance of the system. It's important to choose an appropriate algorithm that balances the conflicting goals of preserving the latest changes, ensuring data consistency, and minimizing the risk of data loss or corruption.

## How is shared locks implemented to implement isolation? ##
1. Shared locks are a commonly used mechanism to implement isolation in database management systems. Isolation refers to the property that ensures that each transaction in the database operates on its own isolated view of the data, and that the changes made by one transaction do not interfere with the changes made by another transaction.
2. In a database with shared locks, a shared lock is placed on a database item (such as a row or a page) whenever a transaction wants to read the item. This lock allows multiple transactions to read the same item at the same time, but it prevents any other transaction from modifying the item until the lock is released.
3. When a transaction wants to modify an item, it must first upgrade its shared lock to an exclusive lock. An exclusive lock allows a single transaction to modify an item, and it prevents any other transaction from accessing the item, even for reading.
4. The shared lock mechanism helps to ensure that each transaction operates on its own isolated view of the data, and that the changes made by one transaction do not interfere with the changes made by another transaction. This way, multiple transactions can run concurrently without any conflicts, and each transaction can operate in complete isolation from the others.
5. In summary, shared locks are a mechanism used to implement isolation in database management systems. By placing shared locks on items that are being read and exclusive locks on items that are being modified, the database ensures that each transaction operates on its own isolated view of the data, and that the changes made by one transaction do not interfere with the changes made by another transaction.

## Give example of shared locks used for isolation. ##
1. A **shared lock**, also known as a **read lock**, is used in a multi-threaded environment to provide shared access to a resource for multiple threads, while still maintaining the isolation of the resource from other threads that may want to write to it.
2. An example of a shared lock being used for isolation is in a database management system. When multiple transactions need to read data from a database, a shared lock can be used to ensure that the data remains isolated from concurrent transactions that may want to write to it. This way, the shared lock allows multiple transactions to read the data simultaneously, while ensuring that the data is not modified until the lock is released.
3. Another example is in a file system, where multiple users may need to read a file simultaneously, but only one user can write to it at a time. A shared lock can be used to ensure that the file remains readable by multiple users, while still maintaining its integrity and preventing concurrent writes.
4. In both these examples, the shared lock provides a way to ensure that the resource is accessible to multiple threads while still maintaining its isolation and consistency.

## How to Choose The Right Database? (ByteByteGo.com) ##
1. Points to consider
	1. Use-case: Growng business
	2. Problems:
		1. Do we need a different database?
			1. Is existing db breaking at the seems?
			2. p95 latency is through the roof? (as data grew)
			3. Is working set overflowing the memory?
				1. even basic requests go to disk and slow everything down?
		2. Ensure that the issues are not easily solvable with the existing database
			1. SOlution: Read DB manual of current db system
				1. **We could use configuration knob mentioned to give us some breathing room**
					1. Migration takes longer time than this
		