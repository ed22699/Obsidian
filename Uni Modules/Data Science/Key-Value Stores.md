---
tags:
  - data_management
---
- like dictionaries in python
- key has a strict format, value is opaque (can have any type)
- no operations beyond CRUD (Create, Read, Update, Delete)
- *Schemaless*: assumptions about the structure of the stored data:
	- are not defined explicitly by a data definition language: schema-on-write
	- are encoded implicitly in the applications logic: *schema-on-read*
- Achieves low latency and high throughput