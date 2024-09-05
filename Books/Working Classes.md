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