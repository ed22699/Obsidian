---
tags:
  - statistics_excel
---
- a data set is a table which contains information about objects. There are 3 pieces of information in a data set: 
	1. *for whom* do we have information 
	2. *about what* do we have information
	3. the *information itself*
- numbers are generally better and quicker to deal with, for this we may implement a legend which we can use to quickly translate numerical data into its textual counterpart. 
	- for this we will typically require the variable name, variable description, values, missing values and scale
	![[Screenshot 2025-08-21 at 14.40.43.png|500]]
- rows contain the objects of the study, and the columns contain the variables
## Scale
- determines which statistical methods are applicable
- data an be nominal, ordinal, or metric
	- nominal: variable only allows to distinguish between the persons and objects of the study, e.g. sex, religion
	- ordinal: ranking, e.g. how much someone likes something, school grades
	- metric: in addition to distinction and ranking, the distance between two expressions is also defined, e.g. age, income
	![[Screenshot 2025-08-21 at 14.50.15.png|500]]
- ordinal data can be treated like metric data, if enough characteristics are possible and the data is normally distributed. More elegant is the creation of a quasi-metric variable
- the scale level plays a decisive role in determining which statistical method can be used
## Excel, SPSS, R
- excel is Microsoft's spreadsheet program
	- not purely statistical
	- has a variety of functions that can be used to store, organise and analyse data
	- can be operated through a graphical interface
	- it is typically available
	- not all statistical applications are available
- SPSS (Statistical Package for the Social Sciences)
	- professional statistical software
	- works through a graphical interface
	- pricy
- R
	- open source
	- allows the application of most of the known methods of statistics
	- requires programming skills