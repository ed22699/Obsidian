---
tags:
  - Lesson
---
- mean: $\bar x = \frac 1 n \sum_{i=1}^n x_i$
- sample variance: $S^2=\frac 1 {n-1} \sum_{i=1}^n(x_i -\bar x)^2$
- percentile: the value below which $p$ percent of the samples in $S$ fall 
	- $25^{th}$ percentile is the value below which $25\%$ of values fall
	- Q1 (25-percentile) = lower quartile
	- Q2 (50-percentile) = median
	- Q3 (75-percentile) = upper quartile
	- $(IQR)=Q3-Q1$
- quantile: 
	- median is the 2-quantile
	- quintile is the 5-quantile
	- quartile is the 4-quantile
		- used for splitting $S$ into four quarters
## Confidence Intervals
- if you have $n$ sets of $k$ samples, you have $n$ estimates of the population mean $\mu$
- can get the bounds $c_1$ and $c_2$ s.t. $P(c_i < \mu < c_2) = 1-\alpha$
- $[c_1,c_2]$ is the confidence interval (CI)
- $\alpha$ is the significance level $0<\alpha <1$ (0.1 is common)
	- smaller significance level is stronger
	- $100(1-\alpha)\%$ confidence level
	- $1-\alpha$ confidence coefficient
![[Screenshot 2025-12-08 at 10.55.46.png|300]]
![[Screenshot 2025-12-08 at 10.56.01.png|300]]
![[Screenshot 2025-12-08 at 10.56.18.png|300]]
## Parametric tests
- assumptions
	- independent observations
	- observations are random draws from a normal/Gaussian distribution
	- observed (dependent) variable is measured on at least an interval scale
		- rank-ordered, equidistant numbers, uniform mean
	- $n \geq 30$ 
	- data drawn from populations with equal variance
	- hypotheses usually about numerical values, especially about the mean
	- often requires:
		- symmetric
		- homoscedasticity
		- equal cell-sizes in the data-table
## Non-parametric tests
- assumptions
	- independent observations
	- few assumptions regarding distribution
	- scale of measurement of dependent variable may be normal or ordinal
	- primary focus is on rank-ordering and/or frequencies of data
	- hypothesis are usually about ranks, medians, or frequencies of data
	- sample size requirements are less stringent than for parametric tests
### Wilcoxon-Mann-Whitney U Test
- non-parametric version of the independent student's t-test
- compares measures of central tendency
- uses medians instead of means (no assumption of normal distribution)
- $H_0$: sample A and sample B come from the same population
- method:
	- combine A and B into one list and sort it
	- rank the list from lowest to highest (award average rank for ties)
	- separate back into two samples and sum the ranks for A and B to get $R_1$ and $R_2$
	- if $H_0$ is true, the two rank-sums should be similar
	- compute $U_1=n_1\cdot n_2 + ((n_1(n_1+1))/2)-R_1$
	- compute $U_2=n_1\cdot n_2 + ((n_2(n_2+1))/2)-R_2$
	- compute $U=\min(U_1,U_2)$
	- compare $U$ to critical value for $U_{n1,n2,\alpha}$ from lookup table
	- if $U<U_{n1,n2, \alpha}$ then reject $H_0$
	![[Pasted image 20251208113453.png|300]]
- assumptions:
	- independent variable has two groups
	- dependent variable's measurement scale is at least ordinal
	- data are randomly selected samples from two independent groups
	- population distributions of the dependent variable for the two groups share a similar shape but have difference in measures of central tendency
- avoid N multiple pairwise tests
	- use Kruskal-Wallis
		- extends U test to allow multiple group comparisons
		- calculates mean ranking for each group's entries in the sorted union list
		- compute a statistic $H$ from the mean rank and the $n$
		- use chi-square test to determine if $H$ is significant
- RRO (Robust rank order) tests are more robust version of U test 
### Box and whisker
![[Pasted image 20251208114935.png|300]]
![[Pasted image 20251208115023.png|300]]
- box and whisker
	- emphasise role of data distribution in determining scale
	- show key statistics
	- allow easy identification of symmetry and skew in distribution
	- increase legibility