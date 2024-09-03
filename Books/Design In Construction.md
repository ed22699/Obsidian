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
## Levels of Design
### Level 1: Software System
### Level 2: Division into Subsystems or Packages
- identification of all major subsystems
- deciding how to partition the program into major subsystems and defining how each subsystem is allowed to use each other subsystem
- this definition of use is important to keep the structure of the system in tact 
	- how many different parts of the system does a developer need to understand at least a little bit to change something in the graphics subsystem?
	- what happens when you try to use the business rules in another system?
	- what happens when you want to put a new user interface on the system, perhaps a command-line UI for test purposes?
	- what happens when you want to put data storage on a remote machine?
- communication between subsystems should be on a need to know basis
- system-level should be an acyclic graph (a program shouldn't contain any circular relationships which A uses B uses C uses A)
#### Common Subsystems
- **Business rules:** laws, regulations, policies and procedures that you encode into a system
- **User interface** 
- **Database access:** hide implementation details of accessing a database 
- **System dependencies:** package OS dependencies into a subsystem, this allows you to swap them out
### Level 3: Division into Classes
- This is the creation of the interfaces and deciding which methods and attributes should be present
### Level 4: Division into Routines
- often left up to the individual programmer
- deciding the private functions and attributes of a class
### Level 5: Internal Routine Design
- often left up to the individual programmer
- the functionality of the individual routines
## Design Heuristics
### Real-World Objects
follows the steps
- identify the objects and their attributes (methods and data)
- determine what can be done to each object
- determine what each object is allowed to do to other objects
- determine the parts of each object that will be visible to other objects - which parts will be public and which will be private
- define each object's public interface
### Form Consistent Abstractions
- bad, low level abstractions complicate a system, package the interface levels into doorknob, door and house
### Encapsulate Implementation Details
### Inherit - When Inheritance Simplifies the Design
### Hide Secrets (Information Hiding)
- interface to a class should reveal as little as possible about this inner workings
- if you are creating a function such as creating a new ID encapsulate in within a function so the new ID process can evolve without other areas needing to know
two categories of secrets
- hiding complexity so that your brain doesn't have to deal with it unless you're specifically concerned with it
- hiding sources of change so that when change occurs, the effects are localised
#### Barriers to information hiding
- **Excessive distribution of information:** if information will be present in many places in the program it is better to define it once and use that definition instead
- **Circular dependencies:** avoid circular dependencies
- **Class data mistaken for global data:** direct access to data is restricted to a few routines organised into a single class. The routines are aware that other routines operate on the data, they know which other routines they are. Requires well designed, small classes
- **Perceived performance penalties:** the calling of these many classes may be perceived as penalising performance, however this modular design means once bottlenecks are exposed they can be dealt with more effectively as they are isolated
#### Value of Information Hiding
- easier to modify
- get into the habit of asking "What should I hide", if you can put a function or data into the class's public interface without compromising its secrets do, otherwise don't
### Identify Areas Likely to Change
1. Identify items that seem likely to change
2. Separate items that are likely to change
3. Isolate items that seem likely to change
Areas likely to change:
- **Business rules** 
- **Hardware dependencies** 
- **Input and output** 
- **Nonstandard language features** 
- **Difficult design and construction areas** 
- **Status variables:** you should not define these with boolean variables but instead using an enumerated typed, adding two levels of flexibility and readability to their use:
	- can easily add new status types
	- can use access routines rather than checking directly, allowing possibility of more sophisticated state detection
- **Data-size constraints**
### Anticipating Different Degrees of Change
- look at the minimal subset of the program, this is least likely to change. Next define minimal increments to the system
- less likely to change areas can be designed so the effect or scope of the change can have a greater impact
### Keep Coupling Loose
- coupling between modules should be loose enough that one module can be used easily by other modules
- criteria for evaluating coupling between modules:
	- Size (number of connections between modules, routines should take less parameters and classes should have minimal methods)
	- Visibility (make connections obvious)
	- Flexibility (the ease to change the connections between modules, the ease for other modules to call a module)
- kinds of coupling:
	- simple-data-parameter coupling (data passed between them are of primitive data types and all data is passed through parameter lists) this is normal and acceptable
	- simple-object coupling (an object instantiates that object) this is fine
	- object-parameter coupling (object1 requires object2 to pass it object3)
	- semantic coupling (one module makes use not of some syntactic element of another module but of some semantic knowledge of another module's inner workings)
### Look for Common Design Patterns
Design patterns are described in the gang of four's [[Design Patterns - Erich Gamma Richard Helm Ralph Johnson John Vlissides]]
patterns provide several benefits that fully custom design doesn't:
- patterns reduce complexity by providing ready-made abstractions
- patterns reduce errors by institutionalising details of common solutions
- patterns provide heuristic value by suggesting design alternatives
- patterns streamline communication by moving the design dialog to a higher level
traps that you could fall into with patterns are:
- force-fitting code to use a pattern. If pattern does not improve understandability it can sometimes increase complexity
- using a pattern because of a desire to try out a pattern rather than because the pattern is an appropriate design solution
### Other Heuristics
- Aim for strong cohesion
- Build hierarchies
- Formalise class contracts
- Assign responsibilities 
- Design for test
- Avoid failure
- Choose binding time consciously
- Make central points of control
- Consider using brute force
- Draw a diagram
- Keep your design modular
## Guidelines For Using Heuristics
1. Understanding the problem
2. Devising a plan
3. Carrying out the plan
4. Looking back
you don't have to solve the whole design problem at once, if you don't have enough information you can leave that last 20% to fall into place when more information is available 
# Design Practices
- Iterate (even if you think the first design is good enough the second will likely be better)
- Divide and Conquer
- Top-Down and Bottom-Up design approaches
	- Top-down is easier as you breaking something down into smaller components 
	- Bottom-up typically results in early identification of needed utility functionality, which results in a compact, well-factored design
	- Bottom-up is useful if similar designs have already been built as you can ask "what can I reuse?"
	- Bottom-up is hard to use exclusively
	- top-down starts simple but sometimes low-level complexity ripples back to the top, making it more complex then needed. Bottom up identifies complexity early leading to better design of higher-level classes, if complexity doesn't torpedo the system first
	- try a variety of approaches
- Experimental Prototyping (can help with wickedness if used correctly)
	- prototyping is <u>throw away code</u>
	- write the minimum code needed to answer the question
	- make sure the question is specific enough
	- do not use the code for the real system, either implement the prototype using technology not present in the production technology or at least prefix classes with prototype
- Collaborative design
	- use less structured approaches to foster creativity and increase number of design alternatives
	- use more structured approaches for quality assurance

## How much design is enough?

| Factor                                                                                     | Level of detail needed in design before construction | Documentation Formality |
| ------------------------------------------------------------------------------------------ | ---------------------------------------------------- | ----------------------- |
| Design/construction team has deep experience in applications area                          | low detail                                           | low formality           |
| Design/construction team has deep experience but is inexperienced in the applications area | medium detail                                        | medium formality        |
| Design/construction team is inexperienced                                                  | medium to high detail                                | low-medium formality    |
| Design/construction team has moderate-to-high turnover                                     | medium detail                                        |                         |
| Application is safety-critical                                                             | high detail                                          | high formality          |
| Application is mission-critical                                                            | medium detail                                        | medium-high formality   |
| Project is small                                                                           | low detail                                           | low formality           |
| Project is large                                                                           | medium detail                                        | medium formality        |
| Software is expected to have a short lifetime (weeks or months)                            | low detail                                           | low formality           |
| Software is expected to have a long lifetime (months or years)                             | medium detail                                        | medium formality        |
- if you can't decide how deeply to investigate a design, err on side of more detail. Errors tend to arise from areas you thought were easy so didn't design rather than areas you did design but badly
- better to have 80% effort go into exploring alternatives and 20% go into documentation than the other way around
## Capturing your work
for small projects, informal projects or projects that need a light-weight way to record design use there approaches:
- insert design documentation into the code itself
- capture design discussion and decisions on a Wiki
- write e-mail summaries
- use a digital camera
- save design flip charts
- use CRC (class, responsibility, collaborator) cards
- create UML diagrams at appropriate levels of detail
# Key Points
- software's primary technical imperative is managing complexity. This is greatly aided by a design focus on simplicity
- simplicity is achieved in two general ways: minimising the amount of essential complexity that anyone's brain has to deal with at any one time, and keeping accidental complexity from proliferating needlessly
- design is heuristic, Dogmatic adherence to any single methodology hurts creativity and hurts your programs
- good design is iterative; the more design possibilities you try, the better your final design will be
- information hiding is a particularly valuable concept. Asking "what should I hide?" settles many difficult design issues