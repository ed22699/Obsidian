---
tags:
  - statistics_excel
---
## The Normal Distribution
- normal distribution is bell-shaped, with a maximum
- it is symmetric around the maximum
- its tails converge asymptotically to the x-axis
- maximum is in the middle of the curve
- the arithmetic mean, median and mode are equal
![[Screenshot 2025-08-25 at 22.52.44.png|400]]
![[Screenshot 2025-08-25 at 22.55.32.png|500]]
$$
f(x) = \frac{1}{\sigma \sqrt{2\pi}}e^{-\frac 1 2(\frac{x - \mu}{\sigma})^2}
$$
- where 
	- $f(x)$ is the function value at the point $x$, i.e. the value on the $y$-axis at the position of the respective $x$-value
	- $\mu$ is the mean of the normal distribution
	- $\sigma$ is the standard deviation of the normal distribution
	- $\pi$ is pi
	- $e$ is Euler's number
- a normally distributed variable can be characterised as follows:
$$
X \sim N(\mu, \sigma)
$$
- increasing the mean causes the normal distribution curve to shift to the right
- increasing the standard deviation causes it to widen
## The $z$-Value and the Standard Normal Distribution
- we can standardise each normal distribution so that they have a mean of 0 and a standard deviation of 1
$$Z = \frac{x-\mu}{\sigma}$$
- where 
	- $z$ is the standardised value (the $z$-value)
	- $x$ is the value of the distribution to be standardised 
	- $\mu$ is the mean value of the distribution
	- $\sigma$ is the standard deviation of the distribution
- this transformation moves the normal distribution to the standard normal distribution i.e. $N(0,1)$ 
![[Screenshot 2025-08-26 at 10.47.08.png|400]]
- with the $z$-value and the standard normal distribution, we can make a statement about likelihood of a certain value or greater
- the standard normal distribution has been tabulated, this is important to test hypothesis
## Normal Distribution, $t$-Distribution, $\chi ^2$-Distribution and $F$-Distribution
- again all these are tabulated
- $t$-distribution is symmetrical like the standard normal distribution with a maximum, a mean of zero and asymptotic towards the $x$-axis. But is slightly wider and flatter, this depends on the degrees of freedom.
	- about 30 degrees of freedom is equal to the standard normal distribution
![[Screenshot 2025-08-26 at 10.57.57.png|400]]
- $\chi ^2$-distribution is useful when testing nominal variables. 
	- depends on degrees of freedom
![[Screenshot 2025-08-26 at 10.58.22.png|400]]
- $F$-distribution, needed for analysis of variance and regression
	- depends on degrees of freedom
![[Screenshot 2025-08-26 at 11.00.30.png|400]]
## Creating Distributions with Excel
### Drawing the normal distribution $N(100,20)$ with Excel
- open empty Excel worksheet and enter the possible $x$-values in the first column
- in the second column, the function NORM.DIST gives the values of the normal distribution
- we enter the $x$-value in the NORM.DIST window for which we want to obtain the function value, further we define the mean and the standard deviation and enter
- draw the graph using Insert tab $\rightarrow$ Line Chart
## Drawing the $t$-Distribution Curve with 15 Degrees of Freedom with Excel