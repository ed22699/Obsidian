## Good Abstraction
- Present a consistent level of abstraction in the class interface (each class should implement one and only one abstract data type)
- Be sure you understand what abstraction the class is implementing
- Provide services in pairs with their opposites
- Move unrelated information to another class
- Make interfaces programmatic rather than semantic when possible (don't let Routine_A depend on Routine_B being called first)
- Beware of erosion of the interface's abstraction under modification (as you realise you forgot details, make sure all new public functions still adhere to the abstraction)
- Don't add public members that are inconsistent with the interface abstraction
- Consider abstraction and cohesion together
## Good Encapsulation
- Minimise  accessibility of classes and members
- Don't expose member data in public
- Avoid putting private implementation details into a class's interface
	- for languages like C++ this may mean writing `EmployeeImplementation *m_implementation` in the private section rather than `String m_name`, `String m_Address` separately. `EmployeeImplementation`  would then implement these details
	- Don't look at private methods in the interface if they are not hidden
- Don't make assumptions about the class' users
- Avoid friend classes (violate encapsulation, circumstances such as the State pattern can be okay)
- Don't put a routine into the public interface just because it uses only public routines (ensure routine is consistent with abstraction if you want to expose it)
- Favour read-time convenience to write-time convenience
- Be very wary of semantic violations of encapsulation (don't rely on what you know about the specific implementation of the interface. If implementation means you can call B because it ensures A is called first, don't. Just call A then B implicitly)
	- you should never need to look at the implementation of the interface, the interface should explain everything you need for use
- Watch for coupling that's too tight
	- minimise accessibility of classes and members
	- avoid friend classes, because they are tightly coupled
	- make data private rather than protected in a base class to make derived classes less tightly coupled to the base class
	- avoid exposing member data in a class's public interface
	- be wary of semantic violations of encapsulation
	- observe the "Law of Demeter"
# Design and Implementation Issues
## Containment
- Implement "has a" through containment
- Implement "has a" through private inheritance as a last resort
- Be critical of classes that contain more than about seven data members (7+-2 is the rule, if primitive datatypes the higher end is okay but objects go on the low end)
## Inheritance ("is a" relationships)
- Implement "is a" through public inheritance
- Design and document for inheritance or prohibit it
- Adhere to the Liskov Substitution Principle (LSP)
	- Subclasses must be usable through the base class interface without the need for the user to know the difference
- Be sure to inherit only what you want to inherit
	- Abstract overridable routine - derived class inherits the routine's interface but not its implementation
	- Overridable routine - inherits the routine's interface and a default implementation an it is allowed to override the default implementation
	- Non-overridable routine - inherits the routine's interface and its default implementation and it is not allowed to override the routine's implementation
- Don't "override" a non-overridable member function (don't reuse names of non-overridable base-class routines in derived classes)
- Move common interfaces, data, and behaviour as high as possible in the inheritance tree
- Be suspicious of classes of which there is only one instance (could confuse objects with classes)
	- consider whether you could just create an object instead of a new class or variation of derived class be represented in data rather than a distinct class. 
	- Use singleton pattern if you still want to make this class
> [!question] Need to look up
> Should every base class have an interface?

- Be suspicious of base classes of which there is only one derived class (don't create anymore inheritance structure than is necessary)
- Be suspicious of classes that override a routine and do nothing inside the derived routine (indicates error in base class)
- Avoid deep inheritance trees (try to keep it no more than two or three levels and 7+-2 subclasses)
- Prefer polymorphism to extensive type checking (repeated case statements sometimes indicate inheritance might be a better design choice)
- Make all data private, not protected
	- if a derived class needs access use protected accessor functions instead
## Multiple Inheritance
- be careful with multiple inheritance. Sometimes valuable but mostly you're better off leaving the tool so it can't do damage
- can be good for mixins, however, mixins must be truly independent of each other
- should use multiple inheritance only after carefully considering the alternatives and weighing the impact on the system complexity and comprehensibility
## Why Are There So Many Rules for Inheritance?
- inheritance tends to work against the primary technical imperative you have as a programmer, which is to manage complexity
- if multiple classes share common data but not behaviour, create a common object that those classes can contain
- if multiple classes share common behaviour but not data, derive them from a common base class that defines the common routines
- if multiple classes share common data and behaviour, inherit from a common base class that defines the common data and routines 
- inherit when you want the base class to control your interface; contain when you want to control your interface
## Member Functions and Data
- Keep the number of routines in a class as small as possible
- Disallow implicitly generated member functions and operators you don't want (such as construction methods)
- Minimise the number of different routines called by a class
- Minimise indirect routine calls to other classes
	- Law of Demeter - Object A can call any of its own routines. If Object A instantiates an Object B, it can call any of Object B's routines. But it should avoid calling routines on objects provided by Object B.
- In general, minimise the extent to which a class collaborates with other classes
	- minimise:
		- number of kinds of objects instantiated
		- number of different direct routine calls on instantiated objects
		- number of routine calls on objects returned by other instantiated objects
## Constructors
- Initialise all member data in all constructors, if possible
- Enforce the singleton property by using a private constructor
	- if you want to define a class that allows only one object to be instantiated, you can enforce this by hiding all the constructors of the class and then providing a static `GetInstace()` routine to access the class's single instance
- Prefer deep copies to shallow copies until proven otherwise
	- deep copies are simple to code and maintain than shallow copies
> [!question]  Look up
> What are deep and shallow copies

# Reasons to Create a Class
- Model real-world objects
- Model abstract objects
- Reduce complexity
- Isolate complexity
- Hide implementation details
- Limit effects of changes
- Hide global data
- Streamline parameter passing
- Make central points of control
- Facilitate reusable code
	-  Projects that used an object-oriented approach were able to take more than 70% of their code from previous projects according to a NASA study
- Plan for a family of programs
- Package related operations
- Accomplish a specific refactoring
## Classes to Avoid
- Avoid creating god classes (creating classes that are all-knowing and all-powerful)
- Eliminate irrelevant classes (class that has only data but no behaviour)
- Avoid classes named after verbs (don't make classes with only behaviour but no data)
# Language-Specific Issues