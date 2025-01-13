---
tags:
  - data_ingress
---
- very suited to tabular data, particularly matrices
- a row is stores as a line
- each element in a row is separated by a comma
	- put commas in a CSV file that should be part of the text should be put in quotes, e.g. `this, has, separations, not "," here`
### Loading CSV file with python
- easy to write own parser
- can use pandas python package to load CSV data
	- performs intelligent type conversion and checking
	- provides a powerful DataFrame object
		- this:
			```python
			from pandas import read_csv
			df = read_csv("csv.csv")
			print(df)
			```
		- outputs this (sort of spreadsheet format):
			| x   | 0   | 1   | 2   |
			| --- | --- | --- | --- |
			| 0   | 1   | 2   | 3   |
			| 1   | 4   | 5   | 6   |
			| 2   | 7   | 8   | 9    |
- CSV files can be a very time efficient and space efficient format choice for tabular data	
			
