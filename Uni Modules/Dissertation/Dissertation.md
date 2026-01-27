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
		- other