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
- this can be done with a second variadic parameter but you still need an external label on the second one
### Modifiable parameters
- parameters themselves cannot be reassigned within the function will need to create a local variable for this within the function
- if we want a function to alter the original value of an argument we must:
	- the type of the parameter we intent to modify must be declared `inout`
	- when we call the function, the variable holding the value to be modified must be declared with `var` not `let`
	- instead of passing the variable as an argument, we must pass its address. This is done by preceding its name with an ampersand (&)
```swift
func removeCharacter(_ c: Character, from s: inout String) -> Int{
	var howMany = 0
	while let ix = s.firstIndex(of:c){
		s.remove(at:ix)
		howMany += 1
	}
	return howMany
}

// calling
var s = "hello"
let result = removeCharacter("l", from:&s)
```