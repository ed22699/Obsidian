---
tags:
  - Lesson
  - data_wrangling
---
- getting to know your data
- not a fixed best practice, requirements will be met by different approaches, tools, techniques and methodologies
- to detect, correct, remove or otherwise deal with corrupted, inaccurate or malformed records. Involves:
	- cleaning, validation, debugging, transforming, re-formatting, pre-processing, imputation, correction, plotting, feature extraction, feature engineering...
![[Screenshot 2025-01-28 at 13.23.12.png|400]]
## Iterative Wrangling
![[Screenshot 2025-01-28 at 13.25.16.png|300]]
## Preprocessing
- general strategies
	- type screening: check a date of birth column has the right type, e.g. they are numbers
	- range check: Check months range between 1-12
	- illegal values
	- multi-column validation: date must be in certain range depending on month column
	- check unique/distinct values: if there is a y instead of a yes check that and possibly change that
	- remove duplicates
- robust checks: [regular expressions](www.regexlib.com)
	- phone numbers
	- email addresses
	- dates
## Random Samples
- is your random sample really representative
	- seasonal data, truncated data, biased data, missing data...
	- outliers, black swans, worst cases, imbalanced samples
## Missing data
- data can be missing for many reasons:
	- data may be sensitive and withheld (e.g. salary)
	- data may be deemed irrelevant and skipped (e.g. census)
	- data may be sensitive and censored (e.g. health info)
	- communication link may fail
	- collection may be aborted (fatigue, boredom)
	- data may be corrupted
	- information may simply not be known
- cross reference agains (validated) external information
- impute from nearest neighbour
- mean/median/mode imputation
- model-based imputation approaches
- combine multiple imputation methods
	- assess the variation caused by different imputation methods
- missing data indication feature
[[Neo4J and CASA Wrangling]]