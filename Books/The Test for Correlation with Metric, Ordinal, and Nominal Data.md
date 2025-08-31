---
tags:
  - statistics_excel
---
## The Test for a Correlation with Metric Data
- assume that there is a correlation between two variables without specifying the direction
- assume a positive correlation
- it is possible that we think that there is a negative correlation between the variables
- in the first case, we test non-directional
	- $H_0: There \; is \; no \; relationship \; between \; variable \; X \; and \; variable \; Y$
	- $H_A: There \; is \; a \; relationship \; between \; variable \; X \; and \; variable \; Y$
	- $H_0: r=0$
	- $H_A: r \neq 0$
- in the second case we assume there is a positive relationship in the population 	
	- $H_0: There \; is \; a \; negative \; or \; no\; relationship \; between \; variable \; X \; and \; variable \; Y$
	- $H_A: There \; is \; a \; positive\; relationship \; between \; variable \; X \; and \; variable \; Y$
	- $H_0: r\leq 0$
	- $H_A: r > 0$
- in the third case 
	- $H_0: There \; is \; a \; positive \; or \; no\; relationship \; between \; variable \; X \; and \; variable \; Y$
	- $H_A: There \; is \; a \; negative\; relationship \; between \; variable \; X \; and \; variable \; Y$
	- $H_0: r\geq 0$
	- $H_A: r < 0$
### The Test Statistic and the Test Distribution
- we test for correlation with metric data using Bravais-Pearson
$$
r = \frac{\sum (x_i - \bar x)(y_i - \bar y)}{\sqrt{\sum (x_i - \bar x)^2 \sum(y_i - \bar y)^2}}
$$
- we calculate the correlation coefficient with the sample data and insert it into the following test statistic
$$
t = \frac {r \times \sqrt{n-2}}{\sqrt{1-r^2}}
$$
- where 
	- $r$ is the correlation coefficient of Bravais-Pearson
	- $n$ is equal to the number of observations
## The Test for a Correlation with Ordinal Data
- same are metric, only difference is that we do not use Bravais-Pearson's correlation coefficient, but Spearman's correlation coefficient
$$
r_{Sp} = \frac{\sum (R_{x_i} - \bar R_x)(R_{y_i} - \bar R _y)}{\sqrt{\sum (R_{x_i} - \bar R_x)^2 \sum(R_{y_i} - \bar R_y)^2}}
$$
### The Test Statistic and the Test Distribution
- the test statistic used to perform the test is t-distributed with $df = n-2$ degrees of freedom 
$$
t = \frac{r_{Sp}}{\sqrt{\frac{1-r_{Sp}^2}{n-2}}}
$$
- where 
	- $r_{Sp}$ is the correlation coefficient of Spearman
	- $n$ is the number of observations
## The Test for Correlation with Nominal Data
- two situations
	- nominal variables with two characteristics each
		- $H_0: r_\Phi = 0$
		- $H_A: r_\Phi \neq 0$
	- nominal variables with more than two characteristics 
		- $H_0: C = 0$
		- $H_A: C > 0$
- in both cases the correlation coefficient says nothing about the direction of the relationship
	- due to this both test procedures are often called tests of independence, if the variables are not correlated then they are independent 
### Test of Independence for Nominal Variables with Two Characteristics
$$
r_{\Phi} = \frac{a \times d - b \times c}{\sqrt{S_1 \times S_2 \times S_3 \times S_4}}
$$
- where
	- $a,b,c,d$ are the fields of a 2x2 matrix
	- $S_1, S_2, S_3,S_4$ are the row sums and column sums
![[Screenshot 2025-08-31 at 00.20.58.png|400]]
- $\chi ^2 = n \times r_\Phi ^2$
### Test of Independence for Nominal Variables with More Than Two Characteristics
$$
C = \sqrt{\frac U {U+n}}
$$
- $U$ is the sum of the deviations between the observed and theoretically expected values
$$
U = \sum \sum \frac{(f_{jk} - e_{jk})^2}{e_{jk}}
$$
- where
	- $f_{jk}$ are the observed frequencies
	- $e_{jk}$ are the theoretically expected frequencies
## Calculating Correlation Tests with Excel
- no command available to calculate the tests of correlation for metric and ordinal data
	- calculate the correlation coefficients and then test using the procedure described above
- for nominal variable we have the CHIQU.TEST it gives back the probability of no correlation between the variables when we put in the observed frequencies and theoretically expected frequencies