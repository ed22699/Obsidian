---
tags:
  - statistics_excel
---
- $H_0: \mu_1 = \mu_2 = \mu_3$
- $H_A: \mu_i \neq \mu_j$ for at lease one pair of $ij$
- analysis of variance allows to compare more than two groups at the same time
- simplest form of analysis of variance is the one-way analysis of variance, with one test variable and one grouping variable
- one way analysis of variance is also known as one-way ANOVA
## The Basic Idea of the Analysis of Variance
- we call the deviation of the group mean from the global mean the deviation explained by the factor level, as this is the average group deviation from the average of all enterprise founders
- the deviation of the observation from the group mean is the unexplained deviation, it cannot be explained by a factor level
## The Test Statistic
- the test statistic of the analysis of variance is derived from the explained and unexplained variance 
- the higher the proportion of the variance explained by the groups, the lower the unexplained proportion and the more likely the grouping variable contributes to explain the differences found
$$
F = \frac{SS_{explained} / (G-1)}{SS_{unexplained} / (G\times (K-1))}
$$
- where
	- $F$ is the value of the test statistic
	- $SS_{explained}$ is the explained sum of squares
	- $SS_{unexplained}$ is the unexplained sum of squares
	- $G - 1$ are the degrees of freedom of the numerator $df_1$
	- $G\times (K-1)$ are the degrees of freedom of the denominator $df_2$
- the test statistic follows the F-distribution, we can determine the critical value using the F-distribution table
## The F-Value and the Decision
- if we divide the sums of squares by the respective degrees of freedom, we calculate the mean sums of squares
## The Analysis of Variance and Omnibus Test and the Bonferroni Correction
- Omnibus tests are test procedures that test for group differences, but do not specifically test between which groups differences exist (the analysis of variance above belongs to these tests)
- post hoc tests are use to test between which groups there are differences
	- a widely used post hoc test in analysis of variance is the Bonferroni correction
- to determine which groups there are differences we need to compare the groups pairwise
	- can be done using the independent samples t-test, the problem with this is we need to now do multiple tests
	- in each of these tests performed we allow an error equal to the specified significance level, and thus what is called error inflation occurs
	- Bonferroni is suggested to divide the original significance level by the number of tests and then test against this new significance level
$$
\alpha^* = \frac \alpha {G \times (G-1)/2}
$$
- where
	- $\alpha ^*$ is the significance level at which each test is tested
	- $\alpha$ is the significance level at which the analysis of variance was tested
	- $G$ is the number of groups respectively factor levels
	- $G \times (G-1)/2$ is the number of tests to be performed
## The Effect Size
- as with the independent samples t-test and the dependent samples t-test, Bravais-Pearson's  correlation coefficient can be used
$$
r^2 = \frac{SS_{explained}}{SS_{total}}
$$
- we take the root to obtain the correlation coefficient as a measure of the effect size
	- $r$ less than $<0.3$ indicates a small effect
	- $r$ in the range from $0.3$ to $<0.5$ indicates a medium effect
	- $r$ in the range from $0.5$ to $1.0$ indicates a large effect
## The Calculation of the Analysis of Variance with Excel
- data analysis tool in the data tab with the command Anova: Single Factor
- in order to perform the pairwise comparisons following the analysis of variance, we use the commands t-Test: Two-Sample Assuming Equal Variances or t-Test: Two-Sample Assuming Unequal Variances
- it is best first to sort the data according to the groups and arrange them in columns, then click data analysis button in the data tab and select the Anova: Single Factor


- if the test variable is metric but not normally distributed or if the test variable is ordinal the Kruskal-Wallis test is used