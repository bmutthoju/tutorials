# Liquibase #
## What is liquibase? ##
Liquibase is an open-source database migration tool that provides a way to manage database schema changes in a version-controlled and repeatable way. It is widely used in modern software development to manage database schema changes and track their history.

With Liquibase, developers can define database changes using a simple XML, YAML or JSON configuration file, called a changelog, which describes the changes that need to be applied to a database schema. Each change in the changelog is associated with a version number, so that Liquibase can determine which changes have already been applied and which ones still need to be executed.

Liquibase supports a wide range of database systems, including Oracle, MySQL, PostgreSQL, SQL Server, DB2, and many others. It can be integrated with various build and deployment tools, such as Maven, Gradle, Jenkins, and Ant, making it easy to include database migrations as part of your automated build and deployment process.

Some of the key features of Liquibase include:
* A simple and easy-to-understand XML, YAML, or JSON configuration format.
* Support for rollbacks, allowing you to undo changes to a database schema.
* Support for multi-environment deployments, enabling you to manage database schema changes across different environments, such as development, testing, and production.
* Support for preconditions and dependencies, allowing you to specify conditions that must be met before a change can be executed.
* Integration with popular build and deployment tools.

Overall, Liquibase provides an easy and repeatable way to manage database schema changes, reducing the risk of errors and making it easier to maintain and evolve your database schema over time.

## How are new columns updated with data if schema is updated using Liquibase? ##
When you add a new column to an existing table using Liquibase, the new column will be added to the table as a nullable column. This means that by default, the new column will not have any data in it, and its value will be NULL for all existing rows.

If you want to update the new column with some default value or existing data, you can do so by adding another Liquibase changeSet that performs an update statement. Here's an example of how to update a new column with a default value using Liquibase:

		<changeSet id="3" author="johndoe">
		  <addColumn tableName="person">
			<column name="age" type="integer"/>
		  </addColumn>
		  <update tableName="person">
			<column name="age" valueNumeric="18"/>
		  </update>
		</changeSet>
		
In this example, the first changeSet adds a new age column to the person table, while the second changeSet updates the age column with a default value of 18 for all existing rows.

Alternatively, you can also use Liquibase's defaultValue attribute to set a default value for the new column. For example:

		<changeSet id="3" author="johndoe">
		  <addColumn tableName="person">
			<column name="age" type="integer" defaultValue="18"/>
		  </addColumn>
		</changeSet>
		
In this example, the new age column is added with a default value of 18 for all new rows. Existing rows will still have a NULL value for the new column unless you run a separate update statement to populate the column with data.

Overall, how you update new columns with data in a Liquibase migration depends on your specific use case and requirements. Liquibase provides various options and strategies for updating data during schema changes, so you can choose the one that works best for your application.