---
tags:
  - swift
---
- object types can be *extended* in swift
	```swift
	extension Int {
		func sayHello(){
			print("Hello, I'm \(self)")
		}
	}
	
	1.sayHello() // outputs: "Hello, I'm 1"
	```
	- in swift here 1 is an object, all types are ultimately object types (everything is an object)
- variables can be defined with either *let* or *var*
	- *let* cannot have its initial value replaced. If possible always declare a name with let, as this permits Swift to behave more efficiently
	- *var* can have its initial value replaced as long as it remains the same type
## Object types
- in swift structs and enums are an object type
- all object types can be instantiated
### Class
### Struct
### Enum