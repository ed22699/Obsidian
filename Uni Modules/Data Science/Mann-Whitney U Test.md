---
tags:
  - data_exploration
---
- commonly used and powerful non-parametric version of the independent [[student's t-test]]
- tests for: $H_0$ "samples A & B are from the same population"
- like the t-test, it compares measures of central tendency
- unlike the t-test, it considers medians instead of means
- doesn't assume your samples are normal with similar variance
- does assume that they "share a similar shape" of some kind
- **Method**:
	- combine datasets A and B into one list and sort it
	- rank the values - awarding any tied values their average rank
	- sum the ranks for A and B, separately, to get $R_A$ and $R_B$
	- if $H_0$ is true, $R_A$ and $R_B$ should be similar
	- compute $U = min(U_A, U_B)$ where:
		- $U_A = n_An_B + \frac {(n_A(n_A+1))}{2} - R_A$
		- $U_B = n_An_B+\frac{(n_B(n_B+1))} 2 -R_B$
	- lookup the critical value $U^*$ (for $n_A, n_B, \alpha$) in a lookup table
	- if $U < U^*$ then reject $H_0$ (else accept it)
![[Screenshot 2025-02-24 at 12.10.39.png|500]]
![[Screenshot 2025-02-24 at 12.10.54.png|500]]
![[Screenshot 2025-02-24 at 12.11.14.png|500]]

## Multiple Comparisons
- WMW-U-Test is for pairwise tests ("is A the same as B?")
	- avoid doing multiple pairwise tests: high risk of false positives
- *Kruskal-Wallis*: extents the U test to allow multiple comparisons
	- a generalised U test for multiple groups ("Are A, B, C, and D the same?"), is a non-parametric version of the ANOVA
	- calculate mean ranks for each group's entries in the sorted union list
	- then compute a statistic H from the mean rank and no. observations
	- finally, use a Chi-squared test to determine whether H is significant
