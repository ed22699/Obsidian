---
tags:
  - stimuli_generation
---
- dispatch will delay an instruction if it is dependant on another e.g. a branch waiting for an addition to get its value
- it will wait for this addition to write to the register before comparing the registers value to the one that triggers the branch
- forwarding mechanisms do not wait for this write to the register and instead instantly check the result against the branch requirement, this saves at least one cycle, however, has less documentation as it doesn't get written first
- need to make sure when testing that the result register is used in the dependancy, this makes it more difficult as you need to consider registers