# Choosing the Right Database #
1. Key points:
	1. Do we really need a different database?
		1. Is the existing DB breaking at the seems?
		2. Is the p95 latency is through the roof?
		3. Is the working set overflowing the existing memory?
			1. Basic requests go to disk and slow everything down
		4. Tip: No matter the issue it must not be easily solvable
			1. Read the DB manual front to back multiple times
				1. There could be a configuration knob to tweek to give us a breathing room
					1. Breathing room can come handly because migration might take a long time (much longer than we think)
					2. Knobs:
						1. Tuning the working set memory size
						2. Choosing a different compaction strategy
						3. Choosing a different garbage collection behavior
					3. DBs are complex and highly tunable
						1. Understand the architecture of a database
						2. Know a DBs limitations
						3. Reach out to experts in the community
							1. Describe the problem(s)
							2. People can often help in surprising ways
					4. Some fixes to our application architecture can give more breathing room
						1. Can we put a cache in front of it and give us some more runway?
						2. Can we add replicas to offload some read load?
						3. Can we shard the database or partition in some way?
							1. Data might be siloed and sharding might help
		5. We must be sure that there is no way to keep using the current database
	2. Once we run out of all avenues for the current database
		1. Choosing the next one:
			1. With databases, **boring is good**
				1. Prefer databases that have been around for a long time and that have been battle tested
			2. Depending on the industry, choice might be different
				1. Banking & Finance - conservative
					1. There must be experienced administrators and developers
					2. The DB must be used by other big firms for many years
			3. Be weary of the outrageous marketing claims
				1. Infinite, effortless, horizontal scalability comes with a hidden cost
					1. Dig deep to find out where the cost is hiding
						1. **Instead of reading the brochure, read the manual**
							1. Look for a page called **limits**
								1. Here we learn the real limits of the new database
									1. Desgn constraints
									2. Fine prints
							2. Look for FAQ pages (very useful)
				2. **The fancier the claims, the longer the disclaimers in the back**
					1. NoSQL databases promise higher scale as compared to the relational databases
						1. Trade-offs
							1. They limit transactional guarantees
							2. They limit data modeling flexibility
								1. No queries across data entities
								2. Data is highly de-normalized
									1. Same data is stored in many collections to support different data-access patterns
				3. To learn more about any particular DB, join the chat room
					1. As questions
				4. Read the Github issues
					1. Learn as much as possible about the candidate database now since the investment is smaller at this juncture
	3. After we choose the database, define a realistic test bench for the candidate using our own data (with own access pattern)
		1. Get some representative data (better than migrating Production database)
		2. Pay attention to outliers
		3. Measure p99 for everything
		4. Try to replicate real workload and push it further to see where it will break
		5. Try key operational tasks
			1. Failing over a node
			2. Data corruption during network partitions
			3. Up & down sharding
	4. Write out a detailed step by step migration plan
		1. Have the peers review it thorughly
			1. If possible migrate a small service first and learn as much as we can from that
2. Migrating a database in real world could take years