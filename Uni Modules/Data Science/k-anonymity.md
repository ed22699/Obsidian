---
tags:
  - data_privacy
---

- A dataset is said to satisfy $k$-anonymity if each combination of values of the quasi-identifier attributes in it is shared by at least $k$ records
- how to achieve $k$-anonymity:
	- *Suppression* values of the attributes are replaces by an asterisk 
	- *Generalisation* values of attributes are replaced by with a broader category

![[Screenshot 2025-01-21 at 10.51.40.png|500]]
## $k$-anonymity Attacks
- $k$-anonymity does not protect against attribute disclosure in general
	- if the values of a confidential attribute are very similar in a group of $k$ records sharing quasi-identifier values
### Homogeneity Attack
- When all the values for a sensitive value within a set of $k$ records are identical, the sensitive value for the set of $k$ records may be exactly predicted
### Background Knowledge Attack
- Association between one or more quasi-identifier attributes with the sensitive attribute to reduce the set of possible values for the sensitive attribute 
## Extensions of $k$-anonymity: $\mathscr{l}$-diversity
- $\mathscr{l}$-diversity requires that the values of all confidential attributes within a group of $k$ records contain at least $\mathscr{l}$ clearly distinct values
### $\mathscr{l}$-diversity drawbacks
- not every value shows equal sensitivity. A rare positive indicator for a disease may provide more information than a common negative indicator
- While $\mathscr{l}$-diversity ensures diversity of sensitive values in each group, it does not recognise the values may be semantically close
	- An attacker could deduce a stomach disease applies to an individual if a sample containing the individual only listed three different stomach diseases 
## Extensions of $k$-anonymity: $t$-closeness
- $t$-closeness requires that the distribution of the confidential attribute within a group of $k$ records is similar to the distribution of the confidential attribute in the entire data set (at most distance $t$ between both distributions)