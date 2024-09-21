---
tags:
  - probability
  - Hashing
---
Let $V_{1},...,V_{k}$ be $k$ events. Then
$$
P(\cup_{i=1}^{k}V_{i}) \leq \sum_{i=1}^{k}P(V_{i})
$$
- this bound is tight ($=$) when the events are all disjoint ($V_{i}$ and $V_{j}$ are disjoint iff $V_i \cap V_{j}$ is empty)
- union bound typically used when each $P(V_{i})$ is much smaller than $k$