---
tags:
  - statistics_excel
---
- correlation does not tell us the direction of the relationship or about causality
![[Screenshot 2025-08-23 at 17.04.56.png|500]]
## The Correlation Coefficient of Bravais-Pearson for Metric Variables
- used to determine the strength of a linear relationship between two metric variables
$$
r = \frac{\sum{(x_i - \bar x)(y_i - \bar y)}}{\sqrt{\sum{(x_i - \bar x)^2} \sum{ (y_i -\bar y)^2}}}
$$
- the correlation coefficient of Bravais-Pearson is defined in the range between -1 and 1
	- -1: perfect negative correlation
	- 1: perfect positive correlation
![[Screenshot 2025-08-23 at 17.10.50.png|300]]
- can be calculated with the CORREL command or under the Data tab with the Data Analysis command under correlation 
## The Scatterplot
- graphical representation of correlation
## The Correlation Coefficient of Spearman for Ordinal Variables
$$
r_{Sp} = \frac{\sum{(R_{x_i} - \bar R_x)(R_{y_i}-\bar R_y)}}{\sqrt{\sum{(R_{x_i} - \bar R_x)^2} \sum(R_{y_i} - \bar R _y)^2}}
$$
- $R_{x_i}$ and $R_{y_i}$ are the ranks of the observed $x$-values and $y$-values
- $\bar R_x$ and $\bar R_y$ are the mean values of the respective ranks

- typically we give the largest value of a variable the rank of one and the smallest value the highest rank
- if values occur more than once, we assign the middle rank of the values and then continue with the rank at which we would be without multiple occurrences
- there is no function to calculate Spearman's rank correlation coefficient in excel, can be used to determine the ranks, using RANK.AVG
## The Phi Coefficient for Nominal Variables with Two Characteristics
- e.g. the variable gender
$$
r_\phi = \frac{a \times d - b \times c}{\sqrt{S_1 \times S_2 \times S_3 \times S_4}}
$$
- $r_\phi$ is the phi coefficient
- $a, b, c, d$ are the frequencies of the fields of a 2 x 2 matrix
- $S_1, S_2, S_3, S_4$ are the sums of the rows and columns
![[Screenshot 2025-08-23 at 17.26.11.png|450]]
- for this the sign of the coefficient is meaningless
## The Contingency Coefficient for Nominal Variables
- nominal data with more than two characteristics
$$
C = \sqrt{\frac{U}{U+n}}
$$
- $C$ is the contingency coefficient 
- $n$ is the number of observations
- $U$ is the sum of the deviations between the observed and theoretically expected values:
	$$
	U = \sum{\sum{\frac{(f_{jk} - e_{jk})^2}{e_{jk}}}}
	$$
	- $f_{jk}$ are the observed frequencies in the cells
	- $e_{jk}$ are the theoretically expected frequencies in the cells
	- $j$ are the rows
	- $k$ are the columns
- Defined is the contingency coefficient not between -1 and 1, but in the range from 0 to a maximum: $0 \leq C \leq C_{Maximum}$
	- $C_{Maximum} = \frac 1 2 (\sqrt{\frac{r-1} r } + \sqrt{\frac {c-1} c})$
		- $r$ is equal to the number of rows
		- $c$ is equal to the number of columns
## Correlation, Spurious Correlations, Causality, and More Correlation Coefficients
![[Screenshot 2025-08-23 at 20.01.32.png|400]]
## Calculating Correlation Coefficients with Excel