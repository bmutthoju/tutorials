# Why a Single-Threaded Redis so Fast? #
1. In-memory database
	1. Rock solid
	2. Easy to use
	3. Fast
2. Reasons:
	1. It is an in-memory database
		1. Memory access is several orders of magnitude faster than random-disk I/O
			1. Pure memory access provides
				1. High read/write throughput
				2. Low latency
			2. Trade-off
				1. Dataset cannot be larger than memory
			3. In-memory databases are much easier to implement than on-disk counterparts
				1. Keeps the code simple & contributes to the Redis's rock solid stability
	3. It is primarily single-threaded