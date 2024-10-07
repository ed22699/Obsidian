---
tags:
  - bloom_filter
  - Lesson
---
functions:
- $INSERT(k)$ - inserts the key $k$ from $U$ into $S$
- $MEMBER(k)$ - output yes if $k\in S$ and no otherwise

- let $n$ be the upper bound on the number of keys that will ever be in $S$ 
- motivation come from applications where the size of the universe $U$ is much much larger than $n$ 
>[!important]
you cannot ask "which keys are in $S$?", only "is this key in $S$"

### Example
- you are attempting to build a blacklist of unsafe URLs that users should not visit
- $U$ contains all possible URLs
- unsafe URLs are inserted into the data structure upon discovery
- whenever we want to visit a URL we check the data structure
# Bloom Filters
a Bloom filter is a randomised data structure for storing a set $S$ which supports two operations 
- $INSERT(k)$ operation inserts the key $k$ from $U$ into $S$ (always correct)
- $MEMBER(k)$ operation 
	- always returns yes if $k\in S$
	- if $k$ is not in $S$ there is a small chance (say 1%) that it will still say yes
>[!note]
sometimes it gets the answer wrong

**Why use Bloom filters?**
- both operations run in $O(1)$ time and the space used is very very good
- uses $O(n)$ bits of space to store up to $n$ keys
	- exact number of bits will depend on the failure probability

## Approach 1: build an array
- for simplicity, let us think of the universe $U$ as containing numbers $1,2,3,...,|U|$
- we could maintain a bit string $B$ where $B[k]=1$ if $k\in S$ and $B[k]=0$ otherwise
![[Screenshot 2024-10-07 at 13.00.38.png|200]]
- have $|U|=10$ and $S$ contains $3,6$ and $8$
- while the operations take $O(1)$ time, this array is $|U|$ bits long
## Approach 2: build a hash table
we now maintain a much shorter bit string $B$ of some length $m<|U|$ 
- assume we have access to a hash function $h$ which maps each key $k\in U$ to an integer $h(k)$ between $1$ and $m$ 
	- $INSERT(k)$ sets $B[h(k)]=1$
	- $MEMBER(k)$ returns yes if $B[h(k)]=1$ and no if $B[h(k)]=0$ 
![[Screenshot 2024-10-07 at 13.06.16.png|500]]
- if $m<|U|$ then there will be some keys that hash to the same positions
- collisions can occur with this method, giving false positives 
	- if we call $MEMBER(k)$ for some key $k$ not in $S$, but there is a key $k'\in S$ with $h(k)=h(k')$ we will incorrectly output yes
- to make sure that the probability of an error is low for every operation sequence, we pick the hash function $h$ at random
	- $h$ is chosen before any operations happen and never changes
### Probability of an error
- assume we haver already inserted $n$ keys into the structure
- further, we have just called $MEMBER(k)$ for some key $k$ not in $S$
- we want to know the probability that the answer returned is yes
![[Screenshot 2024-10-07 at 13.13.27.png|300]]
- bit-string $B$ contains at most $n$ 1's among the $m$ positions
- by definition of $h(k)$ we can conclude that the probability $P(B[h(k)]=1)\leq \frac nm$


