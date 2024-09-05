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
- Be very wary of semantic violations of encapsulation (don't rely on what you know about the specific implementation of the interface. If implementation means you can call B because it ensures A is called first, don't. Just call A then B)