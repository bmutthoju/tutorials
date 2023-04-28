# 8 Key Data Structures That Power Modern Databases #
1. Skip list
	1. Probabilistic datastructure used to implement a sorted set
	2. It is an aternative to a balanced tree
		1. Supports efficient search, insertion and deletion operations
		2. Allows fast lookups, **range queries**, etc...
	3. Usage
		1. Redis: Used to implement ordered data structures
			1. Sorted set
2. Hash Index (Hash table)
	1. Used to efficiently map keys to values
		1. A hash function is used to generate a hash value for each key
			1. Allows fast lookups, insertions, deletions
	2. Usage
		1. Redis
		2. MySQL
		3. PostgreSQL
3. SSTable
	1. Sorted String Table
		1. It is used to store data in disk in a sorted order
		
				Memtable	Memtable
				SStables	Level 0
							Level 1
							Level 2
							
		2. It is a file based data-structure
		3. It is used to store large amounts of data in a highly compressed and efficient format
	2. Memtable
		1. It is an im-memory data-structure that stores recent writes
	3. SSTable and Memtable work together to handle a high volume of data operations

4. LSM Tree
	1. SSTable is the core component of LSM Tree
	2. It is the back-bone of NoSQL databases
		1. Cassandra
		2. RocksDB
		3. LevelDB

5. B-tree family
	1. It is used to store and retrieve large amounts of data on disk
	2. It is a balanced tree that can have multiple children and keeps data sorted
	3. B+ tree
		1. All data is stored in leaf nodes & internal nodes only hold keys
		2. Usage:
			1. MySQL
			2. PostgreSQL
			3. Oracle

6. Inverted Index
	1. Used to efficiently search and retrieve data from a large collection of text documents
	2. Maps words to documents in which they appear
		1. Inverted because of this mapping
	3. Usage
		1. Document search engines
			1. Elasticsearch
			
7. Suffix Tree
	1. Used in databases for efficient text searching
	2. Quickly searches search terms in a large collection of text documents
	
8. R-Tree
	1. Spacially indexed data structure
		1. Organizes data based on their geometric boundaries (rectangles or polygons)
	2. Used to store and retrieve spacial data in a database
	3. Usage
		1. Fast spacial queries
			1. PostGIS
			2. MongoDB
			3. Elasticsearch