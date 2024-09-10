Programming safely with the assumption that others will sometime pass or misuse your code
# Protecting Your Program from Invalid Inputs
ways to handle garbage in:
- Check the values of all data from external sources
- Check the values of all routine input parameters
- Decide how to handle bad inputs
# Assertions
Use assertions to document assumptions made in the code and to flush out unexpected conditions. Check assumptions like
- that an input parameter's value falls within its expected range (or an output parameter's value does)
- That a file or stream is open (or closed) when a routine begins executing (or when it ends executing)
- That a file or stream is at the beginning (or end) when a routine begins executing (or when it ends executing)
- that a file or steam is open for read-only, write-only, or both read and write
- That the value of an input-only variable is not changed by a routine
- That a pointer is non-null
- that an array or other container passed into a routine can contain at least X number of data elements
- that a table has been initialised to contain real values
- That a container is empty (or full) when a routine begins executing (or when it finishes)
- that the results from a highly optimised, complicated routine match the results from a slower but clearly written routine
> [!note] 
> You can build your own assertion mechanism if there is not one already in your language

## Guidelines for Using Assertions
- Use error-handling code for conditions you expect to occur; use assertions for conditions that should never occur
- Avoid putting executable code into assertions (better to execute the code and put the status output into the assertion on another line)
- Use assertions to document and verify preconditions and postconditions
- For highly robust code, assert and then handle the error anyway
# Error-Handling Techniques
- Return a neutral value (value that will not affect the rest of the code)
- Substitute the next piece of valid data (skip it)
- Return the same answer as the previous time
- Substitute the closest legal value
- Log a warning message to a file
- Return an error code
	- Set the value of a status variable
	- Return status as the function's return value
	- Throw an exception by using the language's built-in exception mechanism
> [!tip]
 Use one or multiple of these techniques based on what is suitable for the system

