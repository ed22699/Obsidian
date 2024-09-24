---
tags:
  - verification_tools
---

- driven based on events
- outputs are a function of inputs
	- outputs change only when the inputs do
	- event is the input changing
	- event causes the simulator to re-evaluate and calculate new output
- outputs of one block may be used as inputs of another
- re-evaluation happens until no more changes propagate through the design
- zero delay cycles are called [[delta cycles]]
- event simulator maintains many lists:
	- list of all atomic executable blocks
	- fanout lists: A data structure that represents the interconnect of the blocks via signals
	- time queue - records the points in time when events happen
	- event queue - one queue pair for each entry in the time queue (signal update queue, computation queue)
- simulator needs to process all these queues at simulation time
![[Screenshot 2024-09-24 at 13.21.54.png|400]]