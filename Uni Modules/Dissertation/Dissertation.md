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
	- groups upon LSOA areas so price is median price of area and volume is volume of sales in area (uses lsoa for 2001, 2011 and 2021 to reflect population)
	- uses [ONSPD_MAY_2025_UK](https://geoportal.statistics.gov.uk/datasets/3be72478d8454b59bb86ba97b4ee325b/about) to link: 
		- LSOA
		- LAD (local authority district - housing markets)
			- ONS Local Authority District (Upper Tier / Lower Tier combined) - legacy name
	- Adjust prices for inflation (using 2015 as a base year and taking the mean cpi for the year) [Consumer price inflation time series - Office for National Statistics](https://www.ons.gov.uk/economy/inflationandpriceindices/datasets/consumerpriceindices)
		- note is adjusted based off year not season
		- $price_{infl} = price \cdot \frac{100}{CPI_{2015 \; adj}}$
- DF formatter
	- uses LSOA_2021_EW_BGC_V5 to link LOSA scores to geographic locations: [Lower layer Super Output Areas (December 2021) Boundaries EW BGC (V5)](https://geoportal.statistics.gov.uk/datasets/ons::lower-layer-super-output-areas-december-2021-boundaries-ew-bgc-v5-2/about) (adapt for 2001, 2011, 2021)
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
- splitData
	- tried:
		- adding in historical aggregation: had 0.0008 correlation ratio
	- splits data into groups of 3 years 
	- calculates the 3 year % increase
	- splits into test regions and non test regions
	- saves 2 files, features and ground_truths for each year (note none of these splits contain the test regions)
		- 1995-2012 train
		- 2013-2015 val
		- 2016-2019 test
	- test regions 2016-2019
	- skip shock year predictions (2008, 2009, 2021, 2022)
- correlation map
	- maps the correlation between features
	- can also get the correlation ratio for a specific feature
- Multi linear regression model
	- one-hot encodes LAD (could not do LSOA as there are over 33,000 of them so will exceed RAM space)
	- uses all features (except LSOA as this is technically embedded into each row)
	- takes all the training years and concatenates them into a singular file for training, does a similar thing for validation
	- tried it with only years and years and quarters, found quarters were better
	- is not given centeroids as the changes between 2001, 2011 and 2021 causes it to perform worse

- GTWR
	- [Local Authority Districts (December 2021) Boundaries GB BFC](https://geoportal.statistics.gov.uk/datasets/ons::local-authority-districts-december-2021-boundaries-gb-bfc/about) to split LAD into coordinates to get the centeroids of each LAD area
	- aggregated via LAD instead of LSOA for training use to LSOA exceeding RAM limits, still validated at LSOA level to keep it fair
	- parallelised and chunked for speed and ram limitations
	- coded in R
	- had to make adaptive false as too many datapoints so was basically static and not calculating anything over 8 hours
- XGBoost [GitHub - dmlc/xgboost: Scalable, Portable and Distributed Gradient Boosting (GBDT, GBRT or GBM) Library, for Python, R, Java, Scala, C++ and more. Runs on single machine, Hadoop, Spark, Dask, Flink and DataFlow · GitHub](https://github.com/dmlc/xgboost)
	- print out a feature importance graph
		- lead to changing inflPrice to %increase over year per quarter and LSOA price compared to LAD ratio
	- got the geographical centroids of each LSOA and added the long and lat to take the spatial data
- transformer
	- changes to spacetimeformer
		- add quarterly data
		- create a `__len__` and and `__getItem__`
		- simplify CSVTimeSeries to not automatically split data into train, val and test, so I can keep it consistent with others
		- remove the assumption that each feature has its own time encoding, made it to only have 1 for all features
	- got the geographical centroids of each LSOA and added the long and lat to take the spatial data
	- made it run on GPU
	- issue 5 epochs took 6 hours to run
### adding spatial features
- this would be useful for future cases [Points of Interest Documentation | OS Download Products' Documentation](https://docs.os.uk/os-downloads/products/addresses-and-names-portfolio/points-of-interest)
- school data: [Downloads - GOV.UK](https://get-information-schools.service.gov.uk/Downloads)
	- initial formula $score_{LSOA} = \sum_{i \in S_{LSOA, t}} (W_p \cdot  P_i + W_s \cdot S_i + W_f \cdot F_i)$ 
		- $p$ = primary (higher weighting then the others)
		- $s$ = secondary
		- $f$ = sixth form
		- $S_{LSOA, t}$ = set of all schools active in a specific LSOA during year $t$
		- $w$ are the chosen weights
- train and bus data: [Download national stop data - NaPTAN - DfT](https://beta-naptan.dft.gov.uk/download/national)
	- is a binary 1 if in, 0 if not in for both bus and train
- uni:
	- no good premade data, had to scrape Wikipedia for start and end dates: [List of universities in the United Kingdom by date of foundation - Wikipedia](https://en.wikipedia.org/wiki/List_of_universities_in_the_United_Kingdom_by_date_of_foundation)
	

> [!NOTE]
> As you have your decay, for schools you could also have a OFSTED factor, could also weight off school type i.e. primary school
