## Design Challenges
### Design is a wicked problem
- a wicked problem is a problem that cannot be clearly defined until it has been "solved"
### Design is a sloppy process
- although the finished software design should look well organised and clean, the process of design isn't nearly as tidy
- sloppy as its hard to know when a design is good enough
### Design is about tradeoffs and priorities
- you will have different solutions based off what is important in the project e.g a speed focus will be different to a space focus
### Design involves restrictions
- the goal is to limit and restrict possibilities to improve the overall solution through limiting the complexity of that solution
### Design is nondeterministic
- there are many ways to solve the same problem
### Design is a heuristic process
- involves trial and error
### Design is emergent
- it evolves and improves through design reviews, informal discussions, experience and the code itself

## Complexity
- managing complexity is the most important technical topic in software development
- programs are too large for one person to understand, architecture can break down the sections into subsections to manage this
- keeping routines short helps reduce your mental workload
- overly costly, ineffective designs arise from three sources
	- complex solution to a simple problem
	- simple, incorrect solution to a complex problem
	- inappropriate, complex solution to a complex problem
- suggested 2 prong approach to managing complexity
	- minimise the amount of essential complexity that anyone's brain has to deal with at any one time
	- keep accidental complexity from needlessly proliferating
## Desirable Characteristics of a Design
- **Minimal Complexity:** avoid making "clever" designs make simple and easy to understand. Should let you ignore most over parts of the program
- **Ease of maintenance:** design the system to be self-explanatory 
- **Loose coupling:** keep connections to different parts of a program to a minimum. Minimum connectedness minimises work during integration, testing and maintenance
- **Extensibility:** can enhance a system without causing violence to the underlying structure. Change a piece without affecting other pieces. The most likely changes cause the system the least trauma 
- **Reusability:** can reuse pieces of system in other systems
- **High fan-in:** high number of classes that use a given class. System is designed to make good use of classes at the lover levels in the system
- **Low-to-medium fan-out:** a given class should use no more than 7 other classes within it
- **Portability:** easily move it to another environment
- **Leanness:** system has no extra parts
- **Stratification:** can view system at any single level and get a consistent view.  Can view one level without dipping into other levels. If theres poor code creating an interface that interacts with this code and the rest of the system then interacts with this interface instead
- **Standard techniques:** don't let the system rely on exotic pieces. System should be standardised with common approaches