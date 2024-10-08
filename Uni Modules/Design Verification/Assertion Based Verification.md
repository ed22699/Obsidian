---
tags:
  - Lesson
  - assertion_based_verification
---
traffic light good example of real world safety instance (pedestrian and car lights do not work at the same time)
bounding a liveness property you essentially turn it into a safety property

## Implication operator

| $a$ | $b$ | $a \to b$ |
| --- | --- | --------- |
| 0   | 0   | 1         |
| 0   | 1   | 1         |
| 1   | 0   | 0         |
| 1   | 1   | 1         |
only really care when $a$ is $1$ 