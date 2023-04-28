## LSM Tree ##
1. Log-Structure Merge Tree
	1. Optimized for fast writes
2. How is data stored in relational database
	1. Backed by B-Tree
		1. It is optimized for reads
		2. Updates are relatively expensive
			1. Involves random I/O
			2. Might include updating multiple pages on disk
				1. Limits how fast a B-Tree can injest data
3. LSM Tree data structure
	1. Writes are batched in memory as they arrive in a structure called a memtable
		1. Memtable: Ordered by object key
			1. Usually implemented as a balanced binary tree
			2. Once memtable reaches a certain size, the data is flushed to disk as an SSTable (Immutable Sorted-String Table)
				1. SSTable:
					1. Stores key-value pairs in a sorted sequence
					2. Writes are all sequencial I/O (fast for any storage media)
					3. Recently created SSTable becomes the most recent element of the LSM tree
					4. As more data comes in, more and more SSTables are added to the LSM tree
						1. Each represents a small cronological subset of the incoming changes
					5. Since SSTable is immutable, if there are updates to an existing key, a new entry is stored in the most recent SSTable (this supercedes any entries in the old SSTable)
					6. Delete: A marker is added called as tomstone to the most recently added object key
						1. When we encounter a tomstone during read, we know that the object is deleted
							1. Takes extra space
					7. Read:
						1. Algorithm:
							1. First try to find the key in the memtable
							2. If the key is not available, then look up in the most recent SSTable
							3. If the key is not available, then look up in second-most recent SSTable 
							4. ...
						2. Since SSTable is sorted, lookup can be done efficiently
					8. Issues:
						1. As the number of SSTables grows, it takes an increasingly long time to look up a key
						2. As SSTables accumulate, there are more and more outdated entries as keys that are updated or tomstones added (they take up disk space)
							1. Solution: Periodic merging and compaction process running in the background
								1. Compaction: Merges SSTables and discards outdated or deleted values
									1. Reclaims disk space
									2. Caps the number of SSTables a read has to look through
									3. It is simple and efficient
										1. Since SSTables are sorted, it is similar to the merge phase of the merge sort algorithm
	2. Recap:
		1. LSM Tree buffers incoming writes in memory
		2. When buffer fills up, we sort and flush it to disk as an immutable SSTable
			1. The number of SSTables increase as more and more buffers get flushed to disk
				1. Problem: Reads need to search through more SSTables as SSTables get added
					1. Solution: To cap the number of SSTable lookups, LSM Tree merges SSTables and compacts them in the background
	3. Compaction algorithm:
		1. Two broad strategies:
			1. Size tiered compaction
				1. Optimized for write throughput
			2. Level compaction
				1. Read-optimized
	4. Points to remember:
		1. Compaction keeps the number of SSTables manageable
		2. SSTables are organized into levels
			1. Each SSTable gets larger as SSTables from level above are merged into SSTables to the level below
		3. Compaction consumes a lot of I/O
			1. A mis-tuned compaction could starve the system and slow down both read and write
4. Common optimizations of LSM trees in production systems
	1. They can provide read performance close to the B-Trees
	2. To look up a key, we perform searches of SSTables at every level
		1. Search is fast but consumes a lot of I/O
			1. Solution: Summary table (in memory)
				1. Contains min/max range of each disk block of every level
					1. Allows the system to skip searches on those disk blocks where the key does not fall within the range
						1. Saves a lot of random I/O
		2. Looking up a key that does not exist
			1. Requires going through all the eligible blocks at all the levels
				1. Solution: Bloom filter at each level
					1. It is a space efficient data structure that returns a firm no if a key does not exist but a yes if a key probably exists
						1. Allows the system to skip a level entirely if a key does not exist which reduces random I/O
5. NoSQL DBs backed by an LSM tree can be tuned to support very high write rate
	1. Proper tuning is the key
		1. For LSM Tree compaction tuning is the most critical