# Cache Systems Every Developer Should Know #
1. Why caching?
	1. Enhance system performance
	2. Reduce response time
2. Every layer in a distributed system has caching
	1. Computer hardware
		1. Common caches
			1. L1
				1. In CPU
				2. Smallest and fastest
				3. Stores frequently accessed data and instructions
					1. Avoids fetching data and instructions from slower memory
			2. L2
				1. Slower than L1 cache
				2. Typically located in CPU
				3. Larger than L1 cache
			3. L3
				1. Larger
				2. Slower
				3. Shared between cores
			4. TLB
				1. Stores recently used virtual to physical address translations
					1. Used to quickly translate virtual memory addresses to physical memory addresses
	2. Operating System
		1. Page Cache
			1. Managed by OS
			2. Resides in main memory
			3. Used to store recently accessed disk blocks in memory
				1. When a program requests data from disk, the OS reads the data from memory instead of the disk
		2. File System Caches
		3. Inode Cache
			1. Used to speed up file-system operations by reducing the number of disk accesses required to access files and directories
			2. What is inode cache?
				1. Inode cache, also known as the inode table or inode cache table, is a **data structure used by the file system to keep track of the location and attributes of files and directories on a disk**.
				2. An inode (short for index node) is a data structure used by many Unix-based file systems to store information about a file or directory, such as its ownership, permissions, size, and location on the disk. The inode cache contains a cache of recently used inodes, which can help improve file system performance by reducing the need to read from the disk.
				3. When a file or directory is accessed, the file system first checks the inode cache to see if the inode is already in memory. If it is, the file system can retrieve the file or directory attributes from memory instead of reading them from the disk, which can be much faster. If the inode is not in the cache, the file system must read it from the disk and add it to the cache for future use.
				4. Overall, the inode cache is an important component of a file system's performance and can help improve the speed and responsiveness of file system operations.
			3. What is an inode?
				1. An inode, short for "index node", is a data structure used by many file systems, including Unix-based file systems like ext4 and XFS, to **store information about a file or directory**.
				2. Each file or directory on a file system is represented by an inode, which contains **important information such as the file's ownership, permissions, timestamps, size, and location on the disk**. The inode **also contains pointers to the blocks on the disk where the file's data is stored**.
				3. When a file is created or modified, its inode is updated to reflect the changes. When a file is deleted, its inode is freed up and can be reused by another file.
				4. The use of inodes allows file systems to efficiently store and manage large numbers of files and directories, as each file or directory only requires a small amount of disk space for its inode. Additionally, the use of inodes allows file systems **to perform operations like file renaming and moving without actually copying the file's data, as only the inode needs to be updated**.
				5. Overall, inodes are an essential component of many file systems and play a key role in the efficient management of files and directories on a disk.
			4. Give an example of an inode.
			
					Inode: 12345678
					Mode:  0644
					UID:   1000
					GID:   1000
					Links: 1
					Size:  1024 bytes
					Access time:    Mon Mar 21 10:15:00 2022
					Modify time:    Wed Mar 16 14:30:00 2022
					Change time:    Wed Mar 16 14:30:00 2022
					Block count:    2
					Block pointers: 123, 456

				1. In this example, the inode number is 12345678, and it represents a file with the following properties:
					1. Mode: The file has read and write permissions for the owner and read-only permissions for everyone else (represented by the octal value 0644).
					2. UID and GID: The file is owned by the user with ID 1000 and the group with ID 1000.
					3. Links: The file has one hard link (a reference to the file from another directory).
					4. Size: The file is 1024 bytes in size.
					5. Access time: The file was last accessed on March 21, 2022, at 10:15:00 AM.
					6. Modify time: The file was last modified on March 16, 2022, at 2:30:00 PM.
					7. Change time: The inode was last modified on March 16, 2022, at 2:30:00 PM.
					8. Block count: The file is stored in 2 blocks on the disk.
					9. Block pointers: The first block of the file is stored at block number 123, and the second block is stored at block number 456.
	3. Web front-end
		1. Web-browsers can cache HTTP responses to enable faster retrieval of data
			1. When we request data over HTTP for the first time, it is returned with HTTP policy in the header for the first time
			2. When we request the same data again, it is retrieved from the browser cache if the data is available
		2. CDN
			1. Content Delivery Network
				1. It is used the improve the delivery of static content such as images/videos
					1. Using caching
				2. When user requests content from CDN, CDN looks for the requested content its the cache
					1. If content is not in the cache, the CDN fetches it from the origin server and caches it on the edge servers
					2. If the content is in the cache, the CDN can deliver the content directly from its cache
	4. Load Balancers
		1. Can cache certain resources to reduce loan on the backend servers
			1. When a user requests some content, load balancer caches the responses and serve them directly to future users who request  the same content
				1. Improves response times
				2. Reduces load on backend servers
	5. Message brokers
		1. Use Non-memory caches
		2. Example: Kafka
			1. Caches massive amount of messages on disk
				1. Allows consumers to retrieve messages at their own pace
				2. Messages can be cached for a long period of time based on the retention policy
	6. Distributed caches
		1. Example: Redis
			1. Can store key-value pairs in memory
				1. Provide high read/write performance
	7. Full text search
		1. Example: Elasticsearch
			1. Indexes data for document search & log-search providing quick and efficient access to specific data
	8. Database
		1. Multiple levels of caching
			1. WAL (Write Ahead Log)
				1. Data is first written to the write ahead log before being indexed in a B-Tree
			2. Buffer Pool
				1. Memory area used to cache query results
			3. Materialized views
				1. Can pre-compute query results for faster performance
			4. Transaction logs
				1. Records all transactions and updates to the database
			5. Replication log
				1. Tracks the replication state in a database cluster