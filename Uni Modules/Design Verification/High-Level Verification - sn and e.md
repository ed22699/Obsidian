---
tags:
  - Lesson
  - high_level_verification
---
constraint-driven test generation test bench - test generator, driver, automatic checking (scoreboard, reference model), coverage collection

has errors in one direction for data and temporal checking and functional coverage analysis 
constant-driven test generation is online and offline so needs to interact with the HDL simulator

coverage-driven test generation is mainly done by humans (DUV to design stimulus arrow should not have disappeared)

testbench is the rest of the world

e marks the code rather than the comments, idea is you start from the verification plan (start in editor with empty piece of paper and copy verification plan), you have started off with the comment. Trying to make it natural process
- start comment then right code (supportive of requirements based testing)

interesting to define our own types as in the domain of attributes we need so functional coverage, we want to define opercodes etc. directly

keep soft, would be nice to have but doesn't need to be - can be thrown away if conflict

e stands for english, the intent of e language was to make it most like english

don't keep tests you keep the constrains so you can get the tests again
- as testbench evolves it changes, violating the same testbench version
what principles should be adhered to 
- repeatability
- random stability (acknowledging the fact that code does evolve)