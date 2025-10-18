---
tags:
  - Lesson
---
![[Screenshot 2025-10-16 at 14.42.21.png|500]]
- useful to distinguish between
	- *Macroeconomics*: high-level impenetrable/mystical stuff
		- e.g. the relationship between a nation's inflation rate and unemployment levels
	- *Microeconomics*: just maths, much more useful for problem solving
		- is a set of theories with one aim: to help us gain an understanding of the process by which scarce resources are allocated among alternative uses, and of the role of prices and markets in this process
- there are lots of important resource-limited systems
	- e.g. telecoms, computer OS, staffing/timetabling
	- automating their control/regulation is attractive 
	- difficult for all the usual reasons
- ideas from microeconomics could help us do automated dynamic resource allocation and control in engineered systems
- MBC is not a radical new idea; initially explored in 1988, the ecology of computation 
- it happens that these automatically-optimised robot traders and market mechanisms, originally intended fro control of data centres, are of significant interest to major investment banks, buyside finds, and exchange operators
![[Screenshot 2025-10-16 at 14.52.58.png|500]]
- shortage shown on a graph
![[Screenshot 2025-10-16 at 14.56.04.png|300]]
- for surplus on a graph P will be higher than the equilibrium point
- opposing pressures balance out to the equilibrium point
![[Screenshot 2025-10-16 at 14.57.48.png|500]]
- *Pareto efficient* is no one can be made better off without someone else being worse off
![[Screenshot 2025-10-16 at 15.00.09.png|500]]
- posted offer - has a fixed price and the buyer either buys it or not, such as in retail
[[Online Auctions#Financial Markets|CDA]]
![[Screenshot 2025-10-16 at 15.04.13.png|500]]
- where it extends up to the sky there is no price in which any more are available is at max quantity
- utility is difference between the limit price and the transaction price (is the saving on the sale)
	- bought at a x% margin (this is the utility difference)
![[Screenshot 2025-10-16 at 15.10.17.png|500]]
- triangles are the utility margins
	- horizontal edge is the limit price
	- the point is the price plus the margin, what the trader would actually quote
- not true for very long
	- people leave the market once they have completed the transaction, so get removed from the graph
![[Screenshot 2025-10-16 at 15.13.09.png|500]]
- margins may be constantly changing based on the situation of the market
![[Screenshot 2025-10-16 at 15.15.30.png|500]]
- note that past the equilibrium point margins have been decreased whereas to the left they have been increased
## Experimental Economics
- laboratory-style studies of human market-trading behaviours
- small number of human subjects are split into buyer and seller groups
- all traders given a private-value limit price
	- buyers given sums of cash; can't buy above limit price
	- sellers given units of an arbitrary commodity; can't sell below limit price
- traders interact within some market mechanism
	- buyers may quote bid prices
	- sellers may quote offer prices
- demonstrated rapid equilibration in CDA with very small numbers of traders
- note: professional traders tend to do only slightly better than naive subjects
![[Screenshot 2025-10-16 at 15.24.54.png|400]]
![[Screenshot 2025-10-16 at 15.26.25.png|400]]
![[Screenshot 2025-10-16 at 15.26.58.png|500]]
- how much of the allocative efficiency of a CDA is due to the intelligence of the traders, and how much of it is due to the organisation of the market?
- Gode and Sunder '93 introduced zero-intelligence (ZI) trading agents for CDA markets
	- ZI-U: unconstrained, generate random bid/odder quote prices
	- ZI-C: random quote prices, but constrained not to trade at a loss
- ran experimental economics tests with ZI-U, ZI-C and human traders in 5 different markets, monitored their allocative efficiency
	- ZI-U traders were plain useless
	- ZI-C traders were surprisingly human-like
- conclusions:
	- most of the intelligence is in the market, not in the traders
![[Screenshot 2025-10-16 at 16.18.24.png|400]]
![[Screenshot 2025-10-16 at 16.19.50.png|400]]
![[Screenshot 2025-10-16 at 16.20.04.png|400]]
## Part 2 lecture
![[Screenshot 2025-10-18 at 12.33.50.png|500]]
![[Screenshot 2025-10-18 at 12.34.06.png|500]]
![[Screenshot 2025-10-18 at 12.35.01.png|500]]
- the gradients determine the shape of the probability density function of transaction prices as shown by the triangle
	- peak of triangle is the equilibrium price
	- means the most likely value is the equilibrium price
- a lot rests on the symmetry of the supply and demand curve
![[Screenshot 2025-10-18 at 12.37.51.png|500]]
- ZI-C is not enough
## ZIP algorithm
- for sellers, you have a thing to sell and a limit price $L$ 
- the price you ask, $P$, is $L$ plus some profit margin $M$
- if you have a thing to sell, and your current proposed price is $P$ and either
	- sellers are accepting bids below $P$; or
	- sellers are making offers below $P$
- then decrease $M$ but not below zero
- if trades are happening at prices above $P$, then increase $M$ 
	- even if you currently have no thing to sell
- the buyers do the inverse of this
- the amount by which you adjust your profit margin $M$ is determined by a learning rule (Widrow-Hoff with momentum)
- ZIP is adaptive - adjust behaviour according to other traders' actions
![[Screenshot 2025-10-18 at 12.47.55.png|500]]
![[Screenshot 2025-10-18 at 12.48.34.png|500]]
![[Screenshot 2025-10-18 at 12.48.52.png|500]]
![[Screenshot 2025-10-18 at 12.49.23.png|500]]
- at IBM in 2001
	- tested trader-bot algorithms: ZI-C, ZIP, Kaplan's Sniper and GD
	- pitted human traders against trading agents in experimental economics lab
	- both ZIP and GD beat humans
	- HP's ZOP did at least as well as IBM's GD traders
		- average efficiencies: 
			- ZIPs=1.030
			- GDs=1.023
			- Humans=0.876
	- "the successful demonstration of machine superiority in the CDA and other common auctions could have a much more direct and powerful impact  - one that might be measured n billions of dollars annually"
- ignoring secret algorithms that people are making money off heres the path of progress
![[Screenshot 2025-10-18 at 13.15.52.png|300]]
## Todd Kaplan's Lurking sniper trader
- entered into an early trading-agent contest
- was simple and outperformed all the competition 
- sat quietly in the background doing nothing until the bid-offer spread drops to a sufficiently small value or the offer is less than the smallest transaction price in the previous period, or there is not much time until the market closes
	- if any of these conditions are met, sniper jumps in and steals the deal so long as the deal makes the sniper a profit greater than its minimum threshold
- maybe too simple
	- don't adapt to market activity
	- they are unable to infer the market's $P_0$; they will snipe any deal, however far from equilibrium
	- they free-ride on the goodwill of other traders; and so are not much good when confronted with lots of copies of themselves
## Gjerstad-Dickhaut GD traders
- computes a belief function using data fro recent market activity: calculates the belief function from history $H$ and $n$ recent trades
	- belief function estimates the probability, for each possible bid or offer price, that a bid or offer would be accepted at that price
$$
f(p)=\frac{able(p)+ole(p)}{able(p)+ole(p)+rbge(p)}
$$
- where for a given price $p$
	- $able(p)$ is the number of accepted bids $\leq p$ in $H$
	- $ole(p)$ is the number of offers made $\leq p$ in $H$
	- $rbge(p)$ is the number of rejected bids $\geq p$ in $H$
![[Screenshot 2025-10-18 at 14.54.34.png|400]]
## Decide best
- with multiple alternative trader algorithms, deciding which is best becomes an issue
- attempting to form a full analytic understanding of the capabilities of algorithms such as ZI-C, KSniper, ZIIP, or MGD is typically either:
	- impossible
	- so difficult/laborious that it may as well be impossible
	- requires so many simplifying assumptions that the end conclusions are of limited or zero relevance to the real system
- *empirical studies* are the method of choice, you need to know
	- design of experiments (DoE)
	- Visualisation and statistical analysis of results
![[Screenshot 2025-10-18 at 14.58.44.png|500]]
![[Screenshot 2025-10-18 at 14.59.14.png|500]]
![[Screenshot 2025-10-18 at 15.01.00.png|500]]
## Homogeneous results
![[Screenshot 2025-10-18 at 15.01.32.png|400]]
## Switching strategy
- shows in first row don't switch to ZI-C
![[Screenshot 2025-10-18 at 15.02.53.png|400]]
### Results
- kaplan is only any good if there are a small number among a larger population
	- relies on others to equilibriate the market
- ZI-C clearly dominated by both ZIP and MGD
- other than this, no clear consistent winner
	- best strategy depends on the strategy chosen by the rest of the agents
- further work by IBM looked at a replicator dynamics games where agents would change their strategy over time, and identified attractors and fixed points in the resulting dynamic system
![[Screenshot 2025-10-18 at 15.07.41.png|500]]
- here darker shading means steeper
![[Screenshot 2025-10-18 at 15.10.21.png|500]]
![[Screenshot 2025-10-18 at 15.11.11.png|500]]
![[Screenshot 2025-10-18 at 15.17.02.png|300]]
![[Screenshot 2025-10-18 at 15.17.44.png|300]]
- note this finding that AA isn't always the best was not peer reviewed
![[Screenshot 2025-10-18 at 15.19.05.png|500]]
