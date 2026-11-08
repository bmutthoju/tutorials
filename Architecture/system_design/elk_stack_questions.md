What's a terms dictionary?
What's a posting list?
How are doc values used for sorting, aggregations, and field-value access?
What are BKD-tree-based structures? How are they used?
How does segment merging work? Why do we need multiple levels?
How does refresh work internally?
How does vector search work?
Is any data node a coordinating node? How is a coordinating node selected?
Does data go directly from the translog to replicas?
Does the primary generate sequence numbers?
What is a primary term?
What is per-segment caching?
How does BM25 (Okapi Best Matching 25 work?
What is BBQ?
What is search_after?
How does PIT work?
How do the following work?

allocation
read-only transition
shrink
force merge
searchable snapshots
delete

What is NDJSON?
How do parallel producers optimize throughput?
How is worker concurrency implemented for both reads and writes?
What is the difference between a shard and a node?
How does Elastic Agent work?
What is ECS?
Why do we need `parent_span_id`?
How do we establish the relationship between logs <-> traces <-> metrics?
Why do we need Kafka if we have Logstash PQ?
	Kafka has the following features:
		replay
		multiple downstream consumers
		durable distributed buffering
Why does refresh take time?
How does backpressure work in detail?
What is aggregation? Give some examples. Where are the results stored?
Why should we use keyword instead of text for buckets?
What are buckets?
What is HTTP connection pooling?
How to configure RBAC for ELK stack?
How to configure OIDC for ELK stack?
Why do we need snapshots?