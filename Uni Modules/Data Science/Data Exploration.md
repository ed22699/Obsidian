---
tags:
  - Lesson
  - data_exploration
---
## Old Millennium Statistics
- data collection was slow difficult
- data sets were small
- data processing was manual
- used *null hypothesis testing*
	- addresses 1 specific question at a time
	- data is collected for that specific question
	- assumes data is well behaved
## New Millennium Statistics
- data collection is easy and very fast
- data sets are massive
- data processing is automated
- additional thinking is needed
	- addressing many vague questions
	- data collection may be complicated
	- data itself may be badly behaved
## Parametric vs Non-Parametric
- **Parametric**:
	- approaches make assumptions about the data
	- typically considered to be more *powerful*: better at detecting patterns in your data
	- exploring: [[Box-and-whisker]]
		- may be preferable measures of central tendency + spread when you have:
			- skewed data; bounded data; lots of outliers; non-normal data
	- investigating: Student's t-test
- **Non-Parametric**:
	- approaches make fewer assumptions
	- typically considered to be more *robust*: make fewer assumptions about your data
	- exploring: [[Mean and Std dev]]
		- presumes that they are both good metrics with which to summarise your data
	- investigating: [[Mann-Whitney U Test]]
- statistical significance
	- [[p-values]], practical significance and effect size
	- multiplicity, fishing and $p$-hacking
	- model building and AIC
	![[Screenshot 2025-02-24 at 12.03.02.png|400]]
> [!Warning]
> every visualisation and test gives a partial view (the map is not the territory)