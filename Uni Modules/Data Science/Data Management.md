---
tags:
  - Lesson
  - data_management
---
![[Screenshot 2025-01-28 at 11.17.39.png|400]]
## Typical Data Architecture
![[Screenshot 2025-01-28 at 11.21.01.png|300]]
- Two layers: management and analytics
	- management is supporting the companies business, hot live day to day operations
	- analytics separated section for data mining activity, cold static data
- Decoupled so reporting data science does not interfere with operational processes
- Connect to a read-only replica to obtain data
- everything else hinges on the scale and complexity
## Storage and Database Technologies
### Storage types

| Type             | Description                                                                        | When To Use                                                                                                                                                 |
| ---------------- | ---------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [[Blob Storage]] | Allows unstructured data to be stored and accessed at massive scale in block blobs | You want to support streaming/random-access. You wan to access application data from anywhere. You want to build an enterprise data lake.                   |
| [[Disk Storage]] | Data is stored persistently and accessed via an attached virtual hard disk         | You want to lift and shift applications that use native file system APIs to read/write data to persistent disks. Access from outside the VM is not required |
| [[File Storage]] | Cloud data accessed via SMB and mounted as a local file system in your VMs         | You want to "lift and shift" to the cloud an application that already uses the native file system APIs to share data with other applications                |
- top is most throughput least mediated, bottom is least throughput most mediated
- blob is just access where you don't want to do anything complicated
### Database types
Database technologies sit on top storage
- Store data in a prescribed structure, exploiting the design to access the data in neat ways
#### Relational vs Non-Relational Databases
- relational databases are structured into tables
	- use SQL to query the data
- RDBMS transactions strive to satisfy [[ACID]] constraints
	- can suffer overheads as data scale and complexity increase
- Non-relational databases became popular for big data and real-time web applications
	- known as "NoSQL"
- non-relational DBs we do not prescribe a structure upon creation to gain performance and the expense of [[ACID]] to some degree (typically [[BASE]] instead of [[ACID]])
	- better to overfill a plane and have to give someone money to change flights then say a plane is full when it is not
## Data Warehouses vs Data Lakes

|             | Data Warehouse                                             | Data Lake                                                               |
| ----------- | ---------------------------------------------------------- | ----------------------------------------------------------------------- |
| Type        | Structured and Relational                                  | Structured, Unstructured, Semi-structured; Relational or Non-relational |
| Schema      | Schema on Write                                            | Schema on Read                                                          |
| Format      | Processed, Vetted                                          | Raw, Unfiltered                                                         |
| Sources     | Application, Business, Transactional Data, Batch Reporting | Big Data, IoT, Social Media, Streaming Data                             |
| Scalability | Difficult and Expensive to scale                           | Easy and cheap to scale                                                 |
| Users       | Data Warehouse Professionals, Business Analysts            | Data Scientists, Data Engineers                                         |
| Use cases   | Core Reporting, Business Intelligence                      | ML, Predictive Analytics, Real-time Analytics                           |
- schema on read you just have to know how the database is set up
## Database Classifications
### Data Model
![[Key-Value Stores]]
![[Document Stores]]
![[Column Stores]]
![[Graph Databases]]
#### Choosing Between Database Technologies
![[Screenshot 2025-01-28 at 11.55.31.png|300]]
- the gold standard for complex data is arguably [[Graph Databases]]
- for huge scale, low latency, high throughput, choose [[Key-Value Stores]]
- the default is still Relational
### Consistency/Availability Trade-Off
![[Screenshot 2025-01-28 at 11.57.42.png|500]]
![[Sharding]]
![[Replication]]
## C, A and P
- a good database seeks to achieve three things
	1. *Consistency*: clients should see the same data if they query at the same time
	2. *Availability*: Clients should be able to read and write data at all times
	3. *Partition-tolerance*: The system continues to operate despite network partitions
		- a partition temporarily separates a system into two sub-systems that cannot communicate with each other
### The CAP Theorem
- distributed system cannot provide all three, always a trade off between these three properties
![[Screenshot 2025-01-28 at 12.12.34.png|400]]