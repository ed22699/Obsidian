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
