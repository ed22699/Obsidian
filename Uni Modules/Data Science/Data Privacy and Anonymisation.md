---
tags:
  - Lesson
  - data_privacy
---
- Privacy: The right of individuals to hold information about themselves in secret, free from the knowledge of others
# Formats
- **Tabular data**: tables with counts or magnitudes
- **Queryable databases**: on-line databases which accept statistical queries (sum, average, max, min)
- **Microdata**: files where each record contains information on an individual
# Privacy
- privacy and functionality are a trade-off
	- statistical databases must provide useful statistical information and must also preserve the privacy of respondents, this is sometimes hard as the more private information has good functionality potential
- **Identifiers**: Attributes that unambiguously identify the respondent
	- passport no, national insurance no, social security no, name-surname, etc
	- *suppressed in anonymised data sets*
- **Quasi-identifier**: Attributes that identify the respondent with some ambiguity, but their combination may lead to unambiguous identification
	- address, gender, age, telephone no, etc
	- *risk*:
		- cannot be suppressed because they often have *high analytical value*
		- can be used to link anonymised records to external non-anonymous databases $\Rightarrow$ *re-identification*
- **Confidential vs non-confidential**: 
	- Confidential attributes contain sensitive respondent information
		- salary, religion, diagnosis, etc
	- Non-confidential attributes contain non-sensitive respondent information
## Disclosure Types
- **Attribute disclosure**: the value of a confidential attribute of an individual can e determined more accurately with access to the released statistics than without 
- **Identity disclosure**: a record is an anonymised data set can be linked with a respondent's identity
- **Membership disclosure**: whether or not data about an individual is contained in a dataset
## Attacks in Tables
### External attack
![[External attack]]
### Internal attack
![[Internal attack]]
### Dominance attack
![[Dominance attack]]