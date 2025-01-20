---
tags:
  - data_ingress
---

- human readable, dict-like format
- very robust language; suits many purposes
- JSON is a syntax for storing and exchanging data
- is text, written with JavaScript object notation standard
- originally designed for javascript
- common serialisation in many languages, APIs, and communication frameworks, e.g. REST APIs
- can convert JSON into objects in memory
	- may need to create specific conversion process
- JSON is a very well defined standard (as its so simple its not expected that the standard will ever change)
### Distinctions between JSON and Python dicts
|                  | dict                | JSON    |
| ---------------- | ------------------- | ------- |
| Missing values   | None                | null    |
| String character | '' or ""            | "" only |
| Dictionary keys  | any hashable object | strings |
- JSON files can become large (due to key repetition)
	- Transposing lists of dictionaries into a dictionary of lists will save space in general e.g.
		```JSON
		[
			{
				"type" : "home",
				"number" : "212 555-123"
			},
			{
				"type" : "mobile",
				"number" : "123 456-7890"
			},
			{
				"type" : "home2",
				"number" : "123 456-3421"
			}
		]
		```
	- can be transformed to this:
		```JSON
		{
			"type": [
				"home",
				"mobile",
				"home2"
			],
			"number": [
				"212 555-1234",
				"123 456-7890",
				"123 456-3421"
			]
		}
		```