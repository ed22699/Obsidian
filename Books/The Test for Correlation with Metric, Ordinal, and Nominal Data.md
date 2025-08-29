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