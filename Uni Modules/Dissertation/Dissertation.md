---
aliases:
  - Diss
tags:
  - favorite
---
## Predict
- will the price of this area *increase by 20%* over the next *3 years*, adjusting for inflation
### Assumptions
- first time buyers will not buy brand new properties
- first time buyers are looking for a house not a flat
- first time buyers aim to buy into an "up and coming area", i.e. are open to buying within dodgy areas which are likely to be gentrified in the coming years
## Dataset
[[HM Land Registry — Price Paid Data (PPD)]]
- gives transaction-by-transaction data
- allows volume analysis
- allows price-mix control
	- can exclude flats, newbuilds and additional price paid entry
		- aim is to *assist first time buyers*, they will likely not be buying brand new
		- assume the first time buyers we are catering for are looking for a form of house
- aligns with ML goal

>[!NOTE]
>Need to adjust for inflation myself

## Metrics For Initial Heatmap
- Heatmaps of: 
	- median house price
		- exclude areas under x amount of sales
		- median allows for
			- non-parametric tests
			- robustness against outliers
				- is suitable for skewed distributions and heteroscedastic areas
	- volume of transactions
	- multi-year % change
		- adjusted for inflation
- potential partitions:
	- postcodes
		- capture population density
		- align with how housing markets behave
		- enough volume for reliable medians
		- aligns with existing demographic data