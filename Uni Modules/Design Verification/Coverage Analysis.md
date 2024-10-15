---
tags:
  - Lesson
  - coverage_analysis
---
goal (times covered), relates back to the yellow and green from previous lecture

non-overlapping sets
- arith uses the ALU
- branch uses the control flow

find large areas of uncovered tasks - important because
- if they are similar to each other you might be able to get them in the same test, greater investment of time
- coverage tool presenting the graph is useful in finding these large areas, not very readable is table form
- aggregation algorithm helps find these smaller areas after you are finished with the larger areas

1** is the biggest hole

it took 3 months to get 80% of coverage, we'll be done in another month - **WRONG**, 80% of the coverage takes 20% of the time with the final 20% of coverage requiring 80% of the time

you get the tests from the design or the code - you're going to start from the requirements and derive tests from them (traceability - no test has a right to be there without it being traceable back to the requirement)
- sometimes you can get less than 100% coverage when designing tests with traceability, this is due to weird code that shouldn't be there (security issue) or unspecified requirements (then you would need to explicitly add the new requirement with a corresponding test)

>[!note]
assertion coverage is part of coverage 

- typically combine several coverage models