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
	- advanced formula:
		- $$SchoolScore_{LSOA} = \sum_{j \in Radius} \frac{BaseWeight_{j} \times Multipliers_{j}}{(Distance_{j} + \epsilon)^{p}}$$
			- base weight is the initial value based on if its primary secondary of sixth form
			- multipliers features of the school, e.g. if its single sex or selective school
- train and bus data: [Download national stop data - NaPTAN - DfT](https://beta-naptan.dft.gov.uk/download/national)
	- is a binary 1 if in, 0 if not in for both bus and train
	- advanced score:
		- weighted volume: $$V_{i,t} = \sum (\text{StopType Weight}) \quad \forall \text{ stops where } StartYear \le t \le EndYear$$
			- weights: railway (5.0), Metro (3.0), Tram (3.0), Bus (1.0)
		- Hub multiplier: $$V_{weighted} = \begin{cases} V_{i} \times 3.0 & \text{if } \sum(\text{MajorStops}) > 1 \\ V_{i} & \text{otherwise} \end{cases}$$
		- Spatial decay: $$P_T = \sum_{n \in 3km} \frac{V_{weighted, n}}{(d_{Tn}^2 + 0.5)}$$
		- Normalisation: $$\text{Transport Score} = \ln(1 + P_T)$$
		- $$\text{Improvement}_t = \text{Score}_t - \text{Score}_{t-3}$$
- uni:
	- no good premade data, had to scrape Wikipedia for start and end dates: [List of universities in the United Kingdom by date of foundation - Wikipedia](https://en.wikipedia.org/wiki/List_of_universities_in_the_United_Kingdom_by_date_of_foundation)
		- had to manually alter some technicalities e.g. UCL becoming a Uni in 2023 because UL was awarding the certificates till then
	- use an API to determine which LAD area each uni resides in
	- used this to get student population per uni: [Just a moment...](https://www.hesa.ac.uk/data-and-analysis/students/table-1)
	- advanced score:
		- Weighted mass: $$M_i = Population_i \times PrestigeWeight_i$$
		- spatial decay: $$I_T = \sum_{i \in 30km} \frac{M_i}{(d_{Ti} + 1)^2}$$
		- score: $$S_T = \ln\left(1 + \left(\frac{I_T}{Households_T} \times 100\right)\right)$$
- business:
	- $score = \frac{births}{deaths+1}$
	- new more sophisticated score:
		- $$\text{Business Score} = \log\left(\frac{\text{Active Stock}}{\text{Households}}+\varepsilon\right) \times \left(\frac{\text{Births} + 1}{\text{Deaths} + 1}\right)$$
	- upgraded score:
		- $$BVS_{i,t} = \left( \text{ScaledLogDensity}_{i,t} + 1 \right) \times \left( \text{ScaledMomentum}_{i,t} + 1 \right)$$
		- $$\text{LogDensity} = \ln\left(1 + \frac{\text{Active Businesses}}{\text{Households}}\right)$$
		- $$\text{Momentum} = \frac{\text{Births} + 1}{\text{Deaths} + 1}$$
		- $$\text{ScaledValue} = \frac{x - x_{min, t}}{x_{max, t} - x_{min, t}}$$
	- upgrades business score with LAD lag
		- $$BusScore_{Total} = BusScore_{Local} + \sum \left( \frac{BusScore_{Neighbor}}{Distance_{ij}} \right)$$
	- 1995-2007
		- use [No dataset selected - Nomis - Official Census and Labour Market Statistics](https://www.nomisweb.co.uk/query/construct/components/stdListComponent.asp?menuopt=12&subcomp=100)
		- convert 2011 LADs to 2021
	- 2010-2024
		- use [Business demography, UK - Office for National Statistics](https://www.ons.gov.uk/businessindustryandtrade/business/activitysizeandlocation/datasets/businessdemographyreferencetable/current)
	- 2008-2009
		- could not find the LAD data for this, however in an archive I found a pdf showing the birth and death rates per region, I used this to interpolate based of ratios within regions for the 2007 data
			- [Error 500: Internal Server Error](https://webarchive.nationalarchives.gov.uk/ukgwa/20151013215343/http://www.ons.gov.uk/ons/rel/bus-register/business-demography/2009/index.html)
				- only accurate to the 1000
		- got 2007 regional sums for death and birth
		- $2009_{birth_{LAD}} = 2007_{birth_{LAD}} \cdot \frac{2009_{birth_{regional}}}{2007_{birth_{regional}}}$ 
		- 2008 is the midpoint for each LAD between 2007 and 2009
	- use table 125 to get dwellings: [Live tables on dwelling stock (including vacants) - GOV.UK](https://www.gov.uk/government/statistical-data-sets/live-tables-on-dwelling-stock-including-vacants)
		- interpolate using 5 year average to predict 1995 to 2000
	
- spatial-temporal lag
	- $$
ST_i=\frac{\sum _{j|sd_{[i,j]}<r_s;td_{[i,j]}<r_t}\frac{1}{sd_{[i,j]}^2} *hp_j}{\sum \frac{1}{sd_{[i,j]}}^2}
$$
	- new formula: $$ST_i(q) = \frac{\sum_{j \in R_s, \Delta q \in R_t} \left( \frac{1}{sd_{ij}^2 + 0.5} \cdot e^{-\lambda \Delta q} \cdot \Delta \% hp_j \right)}{\sum_{j \in R_s, \Delta q \in R_t} \left( \frac{1}{sd_{ij}^2 + 0.5} \cdot e^{-\lambda \Delta q} \right)}$$
		- I use the yoy instead of infl_price now
	- $$ST_i(q) = \frac{\sum (W_{spatial} \cdot W_{temporal} \cdot \text{Growth}_j)}{\sum (W_{spatial} \cdot W_{temporal})}$$
	- `main_df['relative_spatial_lag'] = main_df['st_lag_score'] - main_df['price_delta_yoy']`
> [!NOTE]
> As you have your decay, for schools you could also have a OFSTED factor, could also weight off school type i.e. primary school
