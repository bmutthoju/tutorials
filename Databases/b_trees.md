# B-Trees #
## How is a B-Tree used for indexing? ##
A B-tree (Balanced Tree) is **a data structure commonly used for indexing in database systems and file systems**. It is designed **to provide efficient searching, insertion, and deletion of keys, making it well-suited for applications that require fast data retrieval based on key values, such as database indexes**. Here's how a B-tree is used for indexing:

1. **Ordered Data Structure**: A **B-tree is a self-balancing, ordered tree structure**. Each node of the tree contains a certain number of keys and pointers to child nodes. The keys in a B-tree are stored in a sorted order within each node.

2. **Balanced Structure**: The key feature of a B-tree is its balance. This means that the depth (or height) of the tree is kept relatively small and consistent, ensuring that operations like search, insertion, and deletion have predictable and efficient time complexities.

3. **Root Node**: The top-level node of the B-tree is called the root node. It contains a set of keys that divide the range of possible values into intervals, and it has pointers to child nodes corresponding to those intervals.

4. **Intermediate Nodes**: Intermediate nodes in the B-tree also contain keys and pointers to child nodes, allowing the tree to be traversed efficiently. These nodes help narrow down the search path towards the desired key.

5. **Leaf Nodes**: The bottom-level nodes of the B-tree are the leaf nodes. These nodes contain actual data entries or references to data in the indexed structure. Leaf nodes are typically linked together in a doubly-linked list to facilitate range queries.

Here's how a B-tree is used for indexing in a database system:

1. **Efficient Search**: When you perform a search operation in a B-tree index, the tree structure allows for efficient traversal. Starting from the root node, the search proceeds down the tree following the appropriate child node based on comparisons with the keys until it reaches a leaf node that contains the desired key or a reference to the data.

2. **Insertion and Deletion**: B-trees efficiently support insertion and deletion of keys while maintaining the balance of the tree. When inserting a new key, the B-tree ensures that the tree remains balanced by redistributing keys or splitting nodes as needed.

3. **Range Queries**: B-trees are particularly useful for range queries. Since keys are sorted within each node, it's easy to find a range of keys by traversing the tree from the start key to the end key, visiting the leaf nodes along the way.

4. **Bulk Loading**: When initially populating an index, B-trees can be efficiently constructed through a process called bulk loading, which minimizes the number of node splits and ensures balanced trees.

5. **Disk I/O Optimization**: B-trees are designed with disk I/O efficiency in mind. Since they are relatively shallow and balanced, they minimize the number of disk reads required to access data.

6. **Concurrency and Transaction Support**: B-tree indexes in database systems often support concurrency control and transactions to ensure data integrity in multi-user environments.

Overall, B-trees are a versatile and widely used data structure for indexing in database systems due to their efficiency, balanced structure, and support for various operations, making them a fundamental component of database management systems.

## Trees and B+ Trees. How They are Useful in Databases ##
### Topics ###
1. Disk structure
	1. How disk looks like
2. How data is stored on disk
3. What is indexing
	1. Used for faster searching
4. What is multilevel indexing
5. M-Way search trees
6. B-Trees
7. Insertion & deletion - B-Trees
8. B+-Trees

### Disk Structure ###
1. Platter with logical concentric cricles
	1. Track: Circles are called tracks
	2. Sector: Pieces of tracks
	3. Blocks: Interstions between track and sector
2. Addressing:
	1. Block address: (track_no, sector_no)
		1. (1, 0)
	2. Block size: 512 Bytes (typically)
		1. Depends on manufacturer of disk
	3. We always read and write in terms of blocks
		1. Offset: Each byte inside a block has an address called offset
			1. The offets are in the range `[0, 512)`
	4. Byte address: (track_no, sector_no, offset)
3. How positions are changed:
	1. Disk rotation changes sector
	2. Head movement changes tracks
4. Main memory:
	1. Data from disk need to be brought from disk to memory for processig
	2. Data from memory need to be stored on disk for persistence
	3. Data structure: Data used by program that is in the main memory
	4. DBMS: Organizing data efficiently on the disk so that it is easily utilized
		1. Study of the methods or approaches used for storing data in an efficient way (design, organizing)
5. How is data organized on the disk?
	1. Tables:
		1. Row size: 128 Bytes
			1. eid - 10 Bytes
			2. name - 50 Bytes
			3. Dept - 10 Bytes
			4. Section - 8 Bytes
			5. Add - 50 Bytes
		2. No or records / block: 512 / 128 = 4 rows
			1. First 4 rows are stored in first Block
			2. Second 4 rows are stored in the next Block
			3. ...
		3. Assuming 100 records (rows) in the table
			1. 100 / 4 = 25 Blocks are required to store the table
		4. Selection:
			1. If we are searching for a particular record, we need to search all the 25 blocks in the worst case (O(B))
				1. We don't know where the record is
	2. How to reduce the time?
		1. Solution: Index
6. Index:
	1. Structure:
	
			eid (key) | Pointer
			
		1. Record pointer
		2. We will have an entry in the index for each record
			1. Dense index
	2. Where do we store index?
		1. In the disk
		2. Space taken by index:
			1. eid = 10 Bytes
			2. rec pointer = 6 Bytes
			3. Each entry takes 16 Bytes
			4. Number of entries per block = 512 / 16 = 32
			5. 100 entries need = 100 / 32 ~ 3.2 Blocks ~ 4 Blocks
		3. The maximum number of blocks searched in the worst case is 4 Blocks
			1. Once we get the pointer from the index, we can directly go to the record
				1. Maximum 4 + 1 blocks are required for accessing any table record (we read in blocks)
	3. Multi-level index:
		1. Suppose we have 1000 records
			1. => 250 blocks to store the records
		2. There will be 1000 entries in the index
			1. => 40 blocks are required
		3. Need to search 40 Blocks
			1. Solution: Index over the index
		4. Each entry in the second level index will have a pointer to a block in the previous index (1 entry per 32 entries in the second index)
			1. Keys:
				1. 1 -> 1 - 32
				2. 33 -> 33 - 64
				4. ...
		5. **It is a sparse index**
		6. ~ 2 blocks are required to store
		7. Search:
			1. 2 blocks + 1 Block + 1 Block = 4 Blocks need to be fetched and searched
		8. How does it look like:
		
				[]-->[]
				     []
		             []
				[]-->[]
				     []
					 []
			
			1. We can have multi-level indices which reduces the number of blocks that need to be accessed
		9. It is a tree structure:
			1. How do we maintain this?
				1. We cannot add them manually:
					1. Solution: We want them to get added automatically and deleted automatically
						1. If table size is increasing, we add more levels
						2. If table size is reducing, we delete levels (higher level first)
							1. Self managed multi-level indexing
								1. Gives rise to B-Trees and B+-Trees
7. M-Way Search Trees
	1. B-Trees and B+Trees are originating from M-Way search trees
	2. BST:
		1. Binary Search
			1. Has two children
		2. Smaller keys are on the left and bigger keys are on the other side
	3. Can we have more than two keys in a node?
	
						20 50
			
			10 15		30 35		60 90
			
		1. They are in sorted order
		2. Example: Searching for 30
			1. We can find that 20 < 30 < 50 so we go to the middle child
				1. We can use binary search (O(log(k)) to search in a given node
			2. It takes slightly more time than BST
	4. Structure:
		1. 2 keys
		2. 3 children (max)
			1. 3-way search tree
	5. M-Way search Tree
		1. Each node can have atmost M children
			1. => (M - 1) keys
		2. BST - M-way search tree with a degree of 2
	6. Example: 4-way ST
	
			[ |k1| |k2| |k3| ]
			 |    |    |    |			
			 v    v    v    v
			 cp   cp   cp   cp
			 
		1. If there are M children, M - 1 spaces are required
	7. Using M-Way Search Tree for indices
		1. Example: 4-way ST
		
			[ |k1| | |k2| | |k3| | ]
			 |    | |    | |    | |			
			 v    | v    | v    | v
			 cp   | cp   | cp   | cp (child pointer)
			      |      |      |
				  v      v      v
				  rp     rp     rp (record pointer)
				  
	8. Problems:
		1. Insertion:
			1. Example: 10-way search tree
				1. We can have a node per entry and it becomes a linear search
					1. There is no control on how we insert into an M-Way search tree
				2. Height: N
			2. Creation process has no control and there are no guidelines
		2. B-Trees: M-Way search trees with guidelines

### B-Trees ###
1. B-Trees as M-Way search trees with some rules:
2. Rules:
	1. Every node must be filled at-least 1/2
		1. We can construct a new node if the current node is filled by at least 1/2 it's size: ceil(m/2)
	2. Root can have minimum 2 entries
	3. All leaves at the same level
	4. Creation process is bottom-up
3. Example:
	1. M = 4
		1. Keys: 10, 20, 40, 50
		
				10
				
				10 20
				
				10 20 40
				|
				v
					 40
					/  \
				10,20	50
				
			1. We split when there was no space for the new node
4. Higher level indices are created automatically as the B-Tree grows in size

					 40
					/  \
				10,20	50
					
					 40
					/  \
				10,20	50,60
				
					 40
					/  \
				10,20	50,60,70
				
					 40,70
					/  \
				10,20	50,60   80
				
					     40,70
					/      \       \
				10,20,30	50,60   80
				
					  30,40,70
				  /    |    |     \
				10,20  35  	50,60  80				
				
					  30,40,70
				  /    |    |     \
			 5,10,20  35  	50,60  80

                         40
					  /      \
				  15,30        70
				/   |  \     /    \
			 5,10  20  35  	50,60  80	 
			 
5. Every key will have record pointer for an index

## B+-Tree ##
1. We will not have a record pointer from every node
	1. We will have record pointers only from leaf nodes
		1. What about the record pointers for the non-leaf nodes?
			1. Solution: Every key will have its copy in the leaf node
			
                             40
					  /               \
				   15,30               70
				/    |     \         /      \
			 5,10  15,20  30,35  40,50,60  70,80
			 |  |   |  |   |  |   |  |  |   |  |
			 v  v   v  v   v  v   v  v  v   v  v
			 rp rp  rp rp  rp rp  rp rp rp  rp rp
			 
		1. The leaf nodes are connected like a linked list
			1. The leaf nodes is dense index