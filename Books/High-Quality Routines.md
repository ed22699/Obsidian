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
- Don't use routine parameters as working variables (naming conventions like workingVal coming from the parameter inputVal can help show where the data came from)
- Document interface assumptions about parameters 
	- whether parameters are input-only, modified or output-only
	- units of numeric parameters (inches, feet, meters, and so on)
	- meanings of status codes and error values if enumerated types aren't used
	- ranges of expected values
	- specific values that should never appear
- Limit the number of a routine's parameters to about seven
- Consider an input, modify, and output naming convention for parameters (i_, m_, o_, Input_, Modify_, Output_)
- Pass the variables or objects that the routine needs to maintain its interface (ensure parameters are consistent with the abstraction)
- Use named parameters
- Make sure actual parameters match formal parameters
# Special Considerations in the Use of Functions
## When to Use a Function and When to Use a Procedure
- with procedures you can use functions that return a value to show the routines success or failure, If you do this make a clear separation between the routine call and the test of the status value
- use a function if the primary purpose of the routine is to return the value indicated by the function name. Otherwise, use a procedure
## Setting the Function's Return Value
- check all possible return paths
- Don't return references or pointers to local data
# Macro Routines and Inline Routines
- fully parenthesise macro expressions
- Surround multiple-statement macros with curly braces
- Name macros that expand to code like routines so that they can be replaced by routines if necessary
## Limitations on the Use of Macro Routines
alternatives to the use of macros:
- const for declaring constant values
- inline for defining functions that will be compiled as inline code
- template for defining standard operations like min, max, and so on in a type-safe way
- enum for defining enumerated types
- typedef for defining simple type substitutions
**Use macro routines as a last resort**
## Inline Routines
- Use inline routines sparingly
# Key Points
- the most important reason for creating a routine is to improve the intellectual manageability of a program, and you can crate a routine for many other good reasons. Saving space is a minor reason; improved readability, reliability, and modifiability are better reasons
- Sometimes the operation that most benefits from being put into a routine of its own is a simple one
- You can classify routines into various kinds of cohesion, but you can make most routines functionally cohesive, which is best
- the name of a routine is an indication of its quality, If the name is bad and it's accurate, the routine might be poorly designed. If the name is bad and it's inaccurate, it's not telling you what the program does.Either way, a bad name means that the program needs to be changed
- Functions should be used only when the primary purpose of the function is to return the specific value described by the function's name
- Careful programmers use macro routines with care and only as a last resort