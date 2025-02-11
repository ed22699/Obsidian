---
tags:
  - swift
---
```swift
func sum(_ x:Int, _ y:Int) -> Int{
	let result = x + y
	return result
}
```
### External parameter names
- external parameter names: must appear in a call to the function as labels to the arguments, this
	- clarifies the purpose of each argument
	- distinguishes one function from another
	- helps swift to interface with Objective-C and Cocoa where the method parameters nearly always have external names
- if you want the external name to be the same as the internal name do nothing, if you want it to be different you can
	- change the name of an external parameter
	- suppress the externalisation of a parameter
### Overloading
- this is where two functions with the exact same name, including their external parameter names can coexist as long as they have different signatures
```swift
func say() -> String {
	return "one"
}
func say() -> Int {
	return 1
}

// you must call like so
let result: String = say()
```
- overloading the type must be explicit or implied within the context
p33
### Default parameter values
```swift
class Dog{
	func say(_ s:String, times:Int = 1){
		for _ in 1...times{
			print(s)
		}
	}
}
```
### Variadic Parameters
- caller can supply as many argument values to this parameters type as desired, separated by a comma; the function body will receive these values as an array
```swift
func sayStrings(_ array:String ...){
	for s in array { print(s)}
}

// calling
sayStrings("hey", "ho", "hi")
```