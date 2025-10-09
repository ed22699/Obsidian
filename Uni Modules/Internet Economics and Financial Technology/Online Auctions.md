---
tags:
  - auction
---
- internet = quicker and cheaper auctions
	- auction rules are algorithmic, no need for auctioneer
	- can participate remotely
	- sealed auctions quicker, no physical letter
	- bidding can be automated on your behalf
- rules can be easily adapted, do not have to follow the four common auction types
- scalable, run simultaneously, and/or repeated one after another
## Disintermediation
- dotcom boom: predicted small businesses would no longer need intermediaries to sell
	- cost of reaching customers directly reduced
- cost of reaching decreased, cost of getting people's attention increased
	- competition between sellers
- new kind of intermediary - the *online marketplace*
	- single site to access many sellers
	- mechanisms to help assess trustworthiness
	- Ebay
		- near-monopoly as an auction provider
	- Amazon
		- failed auctions
![[Screenshot 2025-10-09 at 16.09.29.png|500]]
## eBay auctions
- open-ascending with deadline
	- english auction, with a time limit
- time limit causes snipers
	- can lead to a rush of last minute bidding as people hope to 
		- not give away information about their value
		- get a cheaper price as there is no time for others to out-bid before auction close
- *solution*
	- get everyone to use a sniper
		- introduced proxy bidding functionality
			- enter your maximum value and the proxy will bid on your behalf up to that value
		- if everyone uses automated and enters their true maximum bid then it becomes similar to a Vickrey auction
	- extend the deadline whenever a new bid is placed
		- turns auction into true english auction
		- amazon auctions did this
![[Screenshot 2025-10-09 at 16.14.52.png|400]]
## Auctions vs Posted Prices
- choice between auctions and posted prices
	- price discovery vs convenience
- eBay
	- auctions favoured by less experienced sellers and for idiosyncratic products
- price discovery: auctions are most useful when sellers are unsure how bidders value an item
- price discrimination: used in combination, auctions and posted prices enable differential pricing
## Google Ad Auction
- largest number of auctions by far
	- auction per google search + per display ad page
	- more than two trillion each year
	- adverts are idiosyncratic, so lend themselves to auctions
- multiple slots auctions per Google search, with additional premium slots above the search
- google assigns slots using bid price and advert quality
- ad quality depends on
	- historic click-through-rate for the ad
	- relevancy
	- landing page quality and load speed
![[Screenshot 2025-10-09 at 16.22.34.png|400]]
- initially used first-price auction
	- game playing occurred, moved to second-price approach
	- want auction to be incentive compatible to reduce monitoring overheads
![[Screenshot 2025-10-09 at 16.24.53.png|400]]
## Reverse Auction
- multiple suppliers bidding to meet a contract
- suppliers offer lower and lower prices, and the lowest offer wins the contract to supply
- often suppliers must be qualified before being allowed to participate
- called an *offer* or *ask*
## Double Auction
- put open-ascending auction and reverse auction together
- when prices cross, we get a match
- *continuous double auction* (CDA) allows buyers and sellers to post bids and offers at any time
- underpins financial markets
- how shares and commodities are bought and sold
## Financial Markets
- major financial exchanges, e.g. London Stock Exchange, trade using a CDA
- bids to buy and offers to sell are visible in a *Public Limit Order Book*
![[Screenshot 2025-10-09 at 16.30.35.png|400]]
- sometimes you don't want to give away your private information
	- if you want to sell a large amount of stock, then if you tell everybody by posting to the public order book it is likely to move the price against you
		- share price will fall as you have dramatically increased supply
		- adverse market movement of the price, market impact or price impact
	- *dark pools* allow you to trade in secret
		- cannot be seen by others
		- similar to a sealed auction
![[Screenshot 2025-10-09 at 16.34.26.png|500]]