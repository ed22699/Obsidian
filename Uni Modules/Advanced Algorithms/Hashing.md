---
tags:
  - Lesson
  - Hashing
---
## Dictionaries
- in dictionary data structure we store (key, value)-pairs s.t. any key has at most one pair in the dictionary 
- perform three operations
	- $add(x,v)$ 
	- $lookup(x)$
	- $delete(x)$
- many data structures can do this but none take $O(1)$ worst case time for all operations
## Hash Tables
- store $n$ elements from the universe, $U$ in a dictionary (typically $u=|U|)$ is much larger than $n$
- a **hash table** is an array $T$ or size $m$
- a **hash function** $h:U \to [m]$ maps a key to a position in $T$
- the aim is to **avoid collisions** i.e. $h(x) = h(y)$ for $x \neq y$ 
	- these collisions are resolved with **chaining** i.e. linked list
	- we cannot avoid collisions entirely since $u \gg m$ 
![[Screenshot 2024-09-19 at 08.39.50.png|500]]
Building a hash table with chaining results in the following time complexities

| Operation   | Worst case time                     | Comment                                                      |
| ----------- | ----------------------------------- | ------------------------------------------------------------ |
| $add(x,v)$  | $O(1)$                              | add item to the list link if necessary                       |
| $lookup(x)$ | $O($length of chain containing $x)$ | may search through the whole list containing $x$             |
| $delete(x)$ | $O($length of chain containing $x)$ | only $O(1)$ to perform actual delete, have to find $x$ first |
[[True randomness]]