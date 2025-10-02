---
tags:
  - Article
Url: https://research-information.bris.ac.uk/ws/portalfiles/portal/206346498/Full_text_PDF_accepted_author_manuscript_.pdf
---
**Note this is only up to and including section 2.3**
## Introduction
- successful trading in financial markets requires balancing the conflicting objectives
	- finding a counterparty with whom to trade
		- mostly solved by publicly announcing an intention (*an order*) to trade
		- if order is large other traders are likely to react to this information by moving the price in the adverse direction. Market reaction to large order is a *price impact* or *market impact*. Cost to a trader can be severe
			- suggested market impact increases roughly as the square root of order size
		- *publicly exposing intention to trade is costly*
	- attempt not to disclose one's trading interest
		- disguise large orders by salami-slicing them into multiple smaller orders to be submitted at irregular intervals
			- bears risk of market moving away
		- pass the order to a *trusted broker* who will attempt to find a natural counterparty within their network of customers and connections
			- if order remains secret within the network there is no market impact
			- is incentive for broker to cheat. Using *insider information* for their own gains by *front running* customers, or by selling the information to a third party
			- *Dark pool trading* venues emerged to counter the reliance on trusting human intermediaries
				- alternative electronic trading systems that automatically match orders in private with no human observers
				- unlike publicly visible orders entered onto the public limit order book (PLOB) of a major lit exchange (e.g. LSE or NASDAQ) orders entering a dark pool are invisible, remain there until a match occurs and only afterwards are the details of the trade published
				- means large orders can execute with little market impact
				- 11% of stock trading in the US executed on such systems in the first quarter of 2018
- *operators of dark pools* with full access to system data are trusted not to spy or abuse the information inside
	- only way to guarantee privacy is to ensure nobody, not even system operators can gain access to the information in the system
		- one mechanism is to apply a *multi-party computation (MPC)* technique 
			- internal algorithm data is held in secret-shared form, processed by a set of servers. If ratio (depending on MPC) of servers remains hones then the internal algorithm variables do not leak, privacy is preserved
			- orders entered into system use protocol to convert external user's order into secret shared form
			- MPC used to perform compuation (order matching) on the secret shared data, s.t. no order information is ever in the clear
			- if a financial regulator (e.g. SEC or FCA) is one of the servers the regulator can guarantee that a specific algorithm was used to perform the matching, aligns with MiFID II
- report introduces proof-of-concept fully encrypted MPC trading venue. Uses three main matching algorithms
	- *continuous double auction (CDA)*, using full limit order book (LOB)
		- natural auction methodology in lit markets
		- in privacy preserving performance is disappointing
		- commonly used in dark pools where the venue operator is an active participant, trading on principle and internally matching client order-flows
			- operator is trading on own account classified and regulated under MiFID II as *system internalisers*
	- *periodic interval crossing*
		- simpler for MPC than a CDA
		- two phases
			1. open auction period, orders collected and sorted, similar to LOB of a CDA, but without execution
			2. on auction close, price discovery phase calculates the clearing price that maximises volume traded
				- all trades execute at this clearing price
		- main cost in evaluating procedure is the algorithms to produce the initial sorted list, i.e. to process the incoming orders before the final clearing is performed
			- limits periodic auction implemented under MPC to be for auctions with a *relatively low throughput*
	- *scheduled volume match*
		- simplest of the three algorithms
		- volume is matched but price is determined by reference to some external lit market
		- not suitable for markets with high frequency trading
		- markets where priority is large volume execution rather than immediacy it may be sufficient
		- used today by venues such as LSE's Turquoise and ITG's Posit Match
- periodic auctions are classified as semi-transparent and so do not fall under MiFID II dark pool compliance 
	- example being LSE's Turquoise Lit Auction
- experiments conducted using the SCALE-MAMBA MPC system
## Background
### Information leakage, insider trading, and front running
- *insider trading* is illegal
	- trading one's own advantage through having access to *confidential information*
- *front running*, an example of insider trading
	- intermediary acts on advance confidential trading information for one's own gain
- aim to avoid *information leakage*
	- trusted broker, or trusted exchange venue is primary concern
		- this is where dark pool trading venues emerged 
### Trading in the dark
- dark pool crossing networks first appeared in 1980s
	- catered for relatively niche market of large volume traders prepared to forego immediate execution to avoid significant price impact 
	- market share of trading in dark pools was initially small
- last decade, largely driven by regulation changes (RegNMS and MiFID) and the rise of high-frequency trading (HFT), number of darl pool venues and volume they trade has ballooned
	- in US around 40 dark pool venues operate with approximately 15-18% market share of securities trading
- mechanisms of dark pool matching categorised into two types
	- *scheduled*: crosses occur at fixed times
	- *continuous*: crosses occur immediately 
		- all dark pools in Europe are now continuous 
- some offer randomised period crossing (matching is at random intervals between 10-45 seconds depending upon liquidity)
- commonly derive execution prices using a "primary" lit venue as reference (e.g. the midpoint of the NBBO)
	- executing all trades at a single midpoint reference provides no price discovery
		- some dark pools provide limited price discovery by maintaining a continuous non-displayed limit order book, where execution prices are bounded between the National Best Bid and Offer
### Out of the dark and into the semi-transparent
- subtle forms of *structural insider trading* which are currently non-illegal but problematic 
	- enable information leakage and include, HFTs "algo-sniffing" dark pools
		- algorithm detect order in dark pool, at least probabilistically, can position itself to profit when the purchase or sales in lit markets begin
- response, regulators attempted to fight back by requiring greater trading transparency
	- MiFID II required double volume cap (DVC)
		- in a given share, dark pool trading volume is now limited to 4% at any one venue, or 8% across all dark venues
		- markets have quickly adapted to the DVC by moving volume away from dark pools to newly-popular *periodic auction venues*
			- unlike continuous central limit order books (CLOBs) where trades are executed instantly as soon as there is a match, in a periodic auction, matching only occurs at the end of a call period
			- length of periodic auctions varies by operator, but many are very short
			- offer some protections traders look for in dark pool venues, with orders during the call period "hidden"
			- not classified by regulators as dark pools as "public information is provided about buying and selling interest during the auction call periods according to MiFID II rules"