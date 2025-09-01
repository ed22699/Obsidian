---
tags:
  - statistics_excel
---
- able to simultaneously analyse the impact of several independent variables on a dependent variable
- goal is to describe the impact of a set of independent variables $X_j$ on a dependent variable $Y$ and to determine what happens to $Y$ when a variable $X_j$ is changed
- using the ordinary least squares method, we minimise the squared deviations of the regression function from the observed $y_i$-values
$$
\sum e_i ^2 = \sum (y_i - (b_0 + b_1 x_{1i} + b_2x_{2i}+...+b_jx_{ji}))^2 \rightarrow min!
$$
- we obtain the regression function with the estimated coefficients
$$
\hat Y = b_0 +b_1X_1 + b_2X_2 + ... + b_JX_J
$$
- where
	- $b_0$ is the intercept
	- $b_1 \; to \; b_J$ are the estimated coefficients for the independent variables $X_j$
	- $J$ is the number of independent variables
	- $\hat Y$ are the estimated values using the regression function
$$
\hat G = b_0 + b_1 Mark + b_2Inno +b_3Sec+b_4Age +b_5Exp+b_6Sex
$$
- where
	- $\hat G$ are the growth rates estimated using the regression model
	- $Mark$ is the marketing effect
	- $Inno$ is the effort for innovations
## F-Test, t-Test and Adjusted-$R^2$
- $H_0: The \; regression \; model \; does \; not \; explain \; the \; dependent \; variable$
- $H_A: The \; regression \; model \; explains \; the \; dependent \; variable$
$$
F = \frac{R^2 / (J)}{(1-R^2)/(N-J-1)}
$$
- where
	- $R^2$ is the coefficient of determination
	- $J$ is the number of independent variables
	- $N$ is the number of observations
- $H_0: The \; independent \; variable \; X_j \; does \; not \; contribute \; to \; the \;explanation \; of \; the \; dependent \; variable$
- $H_A: The \; independent \; variable \; X_j \; contributes \; to \; the \; explanation \; of \; the \; dependent \; variable$
$$
t = \frac{b_j}{s_{b_j}}
$$
- where 
	- $b_j$ is the estimated coefficient for the independent variable $X_j$
	- $s_{b_j}$ is the standard error for the estimated coefficient
$$
R^2 = 1 - \frac {unexplained \; variance}{total \; variance} = 1 - \frac{\sum (y_i - \hat y _i)^2}{\sum (y_i - \bar y)^2}
$$
- when analysing the regression model, when comparing different regression models we instead use adjusted-$R^2$
$$
R_{adj}^2 = R^2 - \frac{J\times (1-R^2)}{N-J-1}
$$
## Calculating the Multiple Regression with Excel
- under the data tab, call up the command Regression using the Data Analysis tool
## When Is the Ordinary Least Squares Estimate BLUE
- ordinary least squares method has the following assumptions
	- the regression function is well specified and contains all the relevant independent variables. The relationship between the independent variables and the dependent variable is linear
	- the deviations of the observed $Y$-values from the estimated $\hat Y$-values have an expected value of zero
	- the deviations are not correlated with the independent variables
	- the variance of the deviations is constant
	- two or more independent variables are not correlated
	- the deviations are uncorrelated with each other
	- the deviations are normally distributed