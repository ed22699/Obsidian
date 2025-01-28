---
tags:
  - data_management
---
![[Screenshot 2025-01-28 at 11.59.05.png|400]]
- Partitioning data across different nodes in the system achieves high scalability in throughput and data volume
## Types of sharding
- Hash- Riak, DynamoDB, Redis, Cassandra, Azure Tables
	- hash of data values determines partition
	- Pro: balanced partitions
	- con: no data locality
- Range Hashing - BigTable, Hbase, MongoDB, RethinkDB, Espresso
	- assigns ranges defined over fields to partitions
	- pro: enables range scans and sorting
	- con: not balanced - repartitioning
- Entity-Group - Cloud SQL Server
	- explicit co-location of data
	- pro: enables real transactions (single node)
	- con: cannot change partitioning