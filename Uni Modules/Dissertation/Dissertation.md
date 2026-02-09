---
aliases:
  - Diss
tags:
  - favorite
---
[[Dissertation Canvas.canvas|Dissertation Canvas]]
## Predict
- will the price of this area *increase by 20%* over the next *3 years*, adjusting for inflation
### Assumptions
![[Persona Assumptions]]
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

## Heatmaps
![[Heatmaps]]

## What code has done/uses
- parquet formatting, using: [Price Paid Data - GOV.UK](https://www.gov.uk/government/statistical-data-sets/price-paid-data-downloads)
	- takes the complete PPD data 
	- creates a year column
	- creates a quarterly column
	- removes 
		- new properties 
		- flats/mansionettes
		- others
	- drops columns
		- oldNew
		- property type
		- ppd type
		- record
	- groups upon LSOA areas so price is median price of area and volume is volume of sales in area
	- uses [ONSPD_MAY_2025_UK](https://geoportal.statistics.gov.uk/datasets/3be72478d8454b59bb86ba97b4ee325b/about) to link: 
		- LSOA
		- LAD (local authority district - housing markets)
			- ONS Local Authority District (Upper Tier / Lower Tier combined) - legacy name
	- Adjust prices for inflation (using 2015 as a base year and taking the mean cpi for the year) [Consumer price inflation time series - Office for National Statistics](https://www.ons.gov.uk/economy/inflationandpriceindices/datasets/consumerpriceindices)
		- note is adjusted based off year not season
		- $price_{infl} = price \cdot \frac{100}{CPI_{2015 \; adj}}$
- DF formatter
	- uses LSOA_2021_EW_BGC_V5 to link LOSA scores to geographic locations: [Lower layer Super Output Areas (December 2021) Boundaries EW BGC (V5)](https://geoportal.statistics.gov.uk/datasets/ons::lower-layer-super-output-areas-december-2021-boundaries-ew-bgc-v5-2/about)
	- get_dataset_for_map
		- filters by year or multiyear
		- decides a score format: volume, median or % increase
		- returns a geographic dataframe that can be used in maps
	- get_dataset_significance 
		- returns a dataframe of price and year
- Significance level
	- takes a year and the number of years back and looks at those number of years back that are before the current year, given a significance level will then find the percentile boundary 
		- $sig = \frac{E[median(price|LSOA)_{t}]} {E[median(price|LSOA)_{t-3}]}$
- Heatmap
	- Will build a map or an area, uses a postcode finds the LSOA area it resides in and centres a map upon that LSOA, produces a circular area of a defined distance around that area
	- can show either a binary map of higher or lower than percentile increase over 3 years, a map of volume of sales that year or a map of median sale prices that year