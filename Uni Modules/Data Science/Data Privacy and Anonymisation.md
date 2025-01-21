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
## Techniques for tables
### Non-perturbative
![[Non-perturbative]]
### Perturbative
![[Perturbative]]
## Techniques for Databases
### Query perturbation
![[Query perturbation]]
### Query restriction
![[Query restriction]]
### Camouflage
![[Camouflage]]
# Differential Privacy
- A learner implements a summary statistic called $\mathcal{A}$ 
- Adversary proposes two datasets $S$ and $S'$ that differ by only one row or example, and a test set $Q$
- **Differential Privacy**:
	- A is called epsilon-differentially private iff $|\log{(\frac{P(\mathcal{A}(S)\in Q)}{P(\mathcal{A}(S')\in Q)})}| \leq \epsilon$ 
	- differential privacy is a condition on the release mechanism and not on the database itself
	- presence or absence of an individual will not affect the final output
# $k$-anonymity
![[k-anonymity]]
# Other approaches to data privacy
- **PPDM**: Privacy-preserving data ining seeks the data owner's privacy when several owners wish to co-operate without giving away their data to each other
- **PIR**: Private information retrieval seeks user privacy to allow the user of a database to retrieve some information item without the database knowing which item was recovered
# Anonymisation tools
- [ARX](http://arx.deidentifier.org/): $k$-anonymity, $\mathscr{l}$-diversity, $t$-closeness implementation in Java
- [Argus](http://neon.vb.cbs.nl/casc): software designed to create safe microdata files
- [SdcMicro](http://cran.r-project.org/package=sdcMicro): Disclosure control methods for anonymisation and risk estimation
