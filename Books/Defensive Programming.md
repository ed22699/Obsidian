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
- Call an error-processing routine/object
- Display an error message whenever the error is encountered
- Handle the error in whatever way works best lcally
- Shut down
> [!tip]
 Use one or multiple of these techniques based on what is suitable for the system

## Robustness vs Correctness
Safety-critical applications tend to favour correctness to robustness. It is better to return no result than to return a wrong result. 

Consumer applications tend to favour robustness to correctness. Any result whatsoever is usually better than the software shutting down. 
# Exceptions
the basic structure of an exception is that a routine uses throw to throw an exception object. Code in some other routine up the calling hierarchy will catch the exception within a try-catch block.
- Use exceptions to notify other parts of the program about errors that should not be ignored
- Throw an exception only for conditions that are truly exceptional
- Don't use an exception to pass the buck (if error can be handled locally, handle it locally)
- Avoid throwing exception in constructors and destructors unless you catch them in the same place
- Throw exceptions at the right level of abstraction (if the error thrown requires knowlage of the method throwing it then it is breaking encapsulation)
- Include in the exception message all information that led to the exception
- Avoid empty catch blocks
- Know the exceptions your library code throws
- Consider building a centralised exception reporter
- Standardise your project's use of exceptions
	- if you're working in a language like C++ that allows you to throw a variety of kinds of objects, data, and pointers, standardise on what specifically you will throw. For compatibility with other languages, consider throwing only objects derived from the Exception base class
	- Consider creating your own project-specific exception class, which can serve as the base class for all exceptions thrown on your project. This supports centralising and standardising logging, error reporting, and so on
	- Define the specific circumstances under which code is allowed to throw an exception that won't be handled locally
	- Determine whether a centralised exception reporter will be used
	- Define whether exception are allowed in constructors and destructors
- Consider alternatives to exceptions
# Barricade Your Program to Contain the Damage Caused by Errors
Barricades are a dame-containment strategy. Interfaces that deal with external data should clean data so the rest of the system is not at risk of these external issues.

The class's public methods assume data is unsafe, and they are responsible for checking the data and sanitising it. Once accepted by the class's public methods, the class's private methods can assume the data is safe
- Convert input data to the proper type at input time
## Relationship Between Barricades and Assertions
- Routines outside the barricade should use error handling because it isn't safe to make any assumptions about the data
- Routines inside the barricade should use assertions, because the data passed to them is supposed to be sanitised before it's passed across the barricade 
# Debugging Aids
## Don't Automatically Apply Production Constraints to the Development Version
- Be willing to trade speed and resource usage during development in exchange for built-in tools that can make development go more smoothly
## Introduce Debugging Aids Early
## Use Offensive Programming
- Make sure asserts abort the program. Don't allow programmers to get into the habit of just hitting the Enter key to bypass a known problem. Make the problem painful enough that it will be fixed
- completely fill any memory allocated so that you can detect memory allocation errors
- Completely fill any files or steams allocated to flush out any file-format errors
- Be sure the code in each case statement's default or else clause fails hard (aborts the program) or is otherwise impossible to overlook
- Fill an object with junk data just before it's deleted
- Set up the program to e-mail error log files to yourself so that you can see the kinds of errors that are occurring in the release software, if that's appropriate for the kind of software you're developing
## Plan to Remove Debugging Aids
- Use version-control tools and build tools like ant and make
- Use a built-in preprocessor
- Write your own preprocessor
- Use debugging stubs
# Determining How Much Defensive Programming to Leave in Production Code
- Leave in code that check for important errors
- Remove code that checks for trivial errors
- Remove code that results in hard crashes
- Leave in code that helps the program crash gracefully
- Log errors for your technical support personnel
- Make sure that the error messages you leave in are friendly
# Key Points
- Production code should handle errors in a more sophisticated way than "garbage in, garbage out"
- Defensive-programming techniques make errors easier to find, easier to fix, and less damaging to production code
- Assertions can help detect errors early, especially in large systems, high-reliability systems, and fast-changing code bases
- the decision about how to handle bad inputs is a key error-handling decision and a key high-level design decision
- Exceptions provide a means of handling errors that operates in a different dimension form the normal flow of the code. They are a valuable addition to the programmer's intellectual toolbox when used with care, and they should be weighed against other error-processing techniques
- Constraints that apply to the production system do not necessarily apply to the development version. You can use that to your advantage, adding code to the development version that helps to flush out errors quickly

