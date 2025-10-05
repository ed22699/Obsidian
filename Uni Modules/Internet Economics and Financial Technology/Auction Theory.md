---
tags:
  - auction
---
- auctions offer the chance for perfect first degree discrimination
- used because *seller is unsure* about the values attached to the object sold
- *Private values* (independent):
	- each bidder knowns the value of the object to him/herself at the time of bidding
	- no bidder knows with certainty the values attached by other bidders and knowledge of other bidders' values has no affect
	- most plausible when the value of the object to the bidder is derived from its consumption or use along (e.g. pizza, bike)
- *Interdependence*:
	- how much the object is worth may be unknown at the time of the auction to the bidder
		- bidder may have an estimate or some private signal that is correlated with the true values (e.g. expert's estimate)
		- other bidders may possess information (e.g. additional estimates) that if known, would affect the value that a particular bidder attaches to the object
	- values are *unknown at the time* of the auction and *may be affected by information available to other bidders*
	- suited for situations in which the object being sold is an asset that can possibly be resold after the auction (e.g. a first edition)
## Equivalent Auctions
- *equivalence*:
	- bidding a certain amount in a first-price sealed-bid auction is equivalent to offering to buy at that amount in a Dutch auction
	- Dutch open descending price auction is strategically equivalent to the first-price sealed-bid auction
- *strategic equivalence*: 
	- for every strategy in one game, a player has a strategy in the other game, which results in the same outcomes
- english and second-price sealed auctions are *weakly equivalent*
	- the two auctions are not strategically equivalent
	- optimal strategies in the two are the same only if values are private 
	- with interdependent values
		- information available to others in the open auction is relevant to a bidder's evaluation of worth
		- seeing some other bidder drop out early may bring bad news that may cause a bidder to reduce his own estimate of the object's value
		- if values are interdependent, the two auctions may not be equivalent from the perspective of the bidders
![[Screenshot 2025-10-05 at 19.46.58.png|500]]
## Incentive Compatibility
- an auction is said to be incentive compatible if it encourages bidders to bid their true value of the good
	- english and second-price sealed bid, optimal strategy is bid where price is equal to value
- dutch and first-price sealed-bid are not. Optimal strategy is to shade, by bidding lower than the true value
- incentive compatible auctions stop game-playing between bidders
### Revenue Equivalence Theorem (RET)
- expected revenue in a first-price auction is the same as the expected revenue in a second-price auction
- if private values are iid and all bidders are risk neutral, then any standard auction (such that the person who bids the highest amount is awarded the item) yields the same expected revenue to the seller
- requires *risk neutral* bidders
	- all bidders only seek to maximise expected profits
- in reality many bidders are *risk averse*
	- effect of a slightly lower winning bid on wealth level has a smaller utility consequence than the possible loss if this lower bid were to result in losing the auction
	- compared to a risk-neutral bidder, a risk-averse bidder will thus bid higher: as it were, they "buy" insurance against the possibility of losing
![[Screenshot 2025-10-05 at 19.56.04.png|500]]
- also requires *private values* (independent)
	- all bidders have an intrinsic value that does not depend on other bidders' values
	- in reality values are often *interdependent*
	- so ordinary ascending auctions are more profitable than standard (first-price) sealed-bid auctions
![[Screenshot 2025-10-05 at 20.00.10.png|500]]