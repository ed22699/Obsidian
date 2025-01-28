---
tags:
  - data_management
---
![[Screenshot 2025-01-28 at 12.03.19.png|500]]
- making many copies guards against failure
- replication achieves availability and durability through redundancy, but introduces the problem of synchronisation
## Types of Replication
- When:
	- Asynchronous (lazy):
		- fast writes but data potentially stale
		- DynamoDB, Riak, CouchDB, MondoDB, Redis, Cassandra
	- Synchronous (eager)
		- consistent, but slow (needs coordination in order to write)
		- BigTable, Hbase, Accumulo
- Where:
	- primary copy
		- accepts writes and all other. nodes are read-replicas (single point of failure)
	- update anywhere
		- any node accepts writes and then propagates them. Fast to write but requires coordination