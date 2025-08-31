---
tags:
  - statistics_excel
---
- the test procedures for nominal data are often called $\chi^2$-tests
## $\chi^2$-test with one sample
- $H_0: \pi_1 = \pi_2 = 0.5$
- $H_A: \pi_1 \neq \pi_2 \neq 0.5$
$$
U = \sum \frac{(f_i - e_i)^2}{e_i}
$$
- where
	- $f_i$ are the observed values
	- $e_i$ are the theoretically expected values
	- $\chi^2$-distributed with $df = c-1$ degrees where $c$ is the number of categories that can occur for the variable
## $\chi^2$-test with two independent samples
$$
U = \sum \sum \frac{(f_{jk} - e_{jk})^2}{e_{jk}}
$$
- where $U$ is $\chi^2$-distributed with $df = (j-1) \times (k-1)$ degrees of freedom
## $\chi^2$-test with two dependent samples
$$
e_b = e_c = \frac{f_b + f_c}{2}
$$
$$
U = \sum \frac{(f_i - e_i)^2}{e_i}
$$
## Calculating the Tests with Excel
- we only have the $\chi^2$-test for independence, this can also be used for the two independent samples