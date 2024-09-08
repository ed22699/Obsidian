# Valid Reasons to Create a Routine
- Reduce complexity
- Introduce an intermediate, understandable abstraction
- Avoid duplicate code
- support subclassing 
- Hide sequences
- Hide pointer operations
- Improve portability
- Simplify complicated boolean tests
- Improve performance
- isolate complexity
- hide implementation details
- Limit effects of changes
- Hide global data
- Make central points of control
- facilitate reusable code
- Accomplish a specific refactoring
> [!note] 
> You can put one line operations into a routine if it improves readability and cohesion

# Design at the Routine Level
- Functional cohesion i8s the strongest and best kind of cohesion, occurring when a routine performs one and only one operation
## Less than ideal cohesion
- Sequential cohesion - contains operations that must be performed in a specific order, share date step to step and don't make a complete function when done together
	- create separate routines where the reliant routine can call the other
- Communicational cohesion - operations in routine make use of the same data and aren't related in any other way
	- summary data should be reinitialised close to where it's created and the operations should be split into separate routines
- Temporal cohesion - operations are combined into a routine because they are all done at the same time
	- create separate routines for each operation and have one routine call them all
## Unacceptable Cohesion
- Procedural cohesion - operations in a routine are done in a specified order
	- put separate operations into their own routines and make sure the calling routine has a single complete job
- Logical cohesion - several operations stuffed into a routine and one is chosen via a flag
	- each operation should have its own routine and the calling routine (event handler) should have only the job of selecting which is ran
- Coincidental cohesion - operations in a routine that have no discernible relationship
# Good Routine Names
- Describe everything the routine does
- Avoid meaningless, vague, or wishy-washy verbs
- Don't differentiate routine names solely by number
- Make names of routines as long as necessary
- To name a function, use a description of the return value
- To name a procedure, use a strong verb followed by an object
- Use opposites precisely
- Establish conventions for common operations
# How Long Can a Routine Be
If writing a long routine its best to keep it below 100-200 lines, higher than that and you should be careful
# How to Use Routine Parameters
- Put parameters in input-modify-output order
- If several routines use similar parameters, put the similar parameters in a consistent order
- Use all the parameters 
- Put status or error variables last
- Don't use routine parameters as working variables