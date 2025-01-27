---
tags:
  - Lesson
  - data_management
---
## Typical Data Architecture
- Two layers: management and analytics
- Decoupled so reporting data science does not interfere with operational processes
- Connect to a read-only replica to obtain data
- complete----------------
## Storage and Database Technologies

| Type             | Description                                                                        | When To Use                                                                                                                                                 |
| ---------------- | ---------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [[Blob Storage]] | Allows unstructured data to be stored and accessed at massive scale in block blobs | You want to support streaming/random-access. You wan to access application data from anywhere. You want to build an enterprise data lake.                   |
| [[Disk Storage]] | Data is stored persistently and accessed via an attached virtual hard disk         | You want to lift and shift applications that use native file system APIs to read/write data to persistent disks. Access from outside the VM is not required |
| [[File Storage]] | Cloud data accessed via SMB and mounted as a local file system in your VMs         | You want to "lift and shift" to the cloud an application that already uses the native file system APIs to share data with other applications                |
- complete -------------
## Relational vs Non-Relational Databases
- complete ---------
Database technologies sit on top of that
- Store data in a prescribed structure, exploiting the design to access the data in neat ways
- [[ACID]]
- non-relational DBs we do not prescribe a structure upon creation to gain performance and the expense of [[ACID]] to some degree (typically [[BASE]] instead of [[ACID]])
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
## Database Classifications
### Data Model
![[Key-Value Stores]]
![[Document Stores]]
![[Column Stores]]
![[Graph Databases]]
#### Choosing Between Database Technologies
### Consistency/Availability Trade-Off