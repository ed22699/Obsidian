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
- parquet formatting
	- takes the complete PPD data 
	- creates a year column
	- removes 
		- new properties 
		- flats/mansionettes
		- others
	- drops columns
		- oldNew
		- property type
		- ppd type
		- record
	- uses ONSPD_MAY_2025_UK to link
		- LSOA
		- longitude/latitude
	- Adjust prices for inflation (using 2025 as a base price and taking the mean cpi for the year)
		- note is adjusted based off year not season
- DF formatter
	- uses LSOA_2021_EW_BGC_V5 to link LOSA scores to geographic locations
	- get_dataset_for_map
		- filters by year or multiyear
		- decides a score format: volume, median or % increase
		- returns a geographic dataframe that can be used in maps
	- get_dataset_significance 
		- returns a dataframe of price and year
- Significance level
	- takes a year and the number of years back and looks at those number of years back that are before the current year, given a significance level will then find the percentile boundary 
- Heatmap
	- Will build a map or an area, uses a postcode finds the LSOA area it resides in and centres a map upon that LSOA, produces a circular area of a defined distance around that area
	- can show either a binary map of higher or lower than percentile increase over 3 years, a map of volume of sales that year or a map of median sale prices that year