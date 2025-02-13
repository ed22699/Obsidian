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
### Reference Type Modifiable parameters
- one common situation where your function can modify a parameter without declaring it as inout, is when it is an instance of a class. Classes are mutable
	- classes are reference types
	- other object types are value types
### Function as value
- functions can be passed as values
```swift
func doThis(_ f:90 -> ()){
	f()
}
```
### Anonymous Functions
- a nameless function body. For this you need two things:
	- create the function body itself, including the surrounding curly braces, but with no function declaration
	- if necessary, express the function's parameter list and return type as the first thing inside the curly braces, followed by the keyword `in`
```swift
UIView.animate(withDuration:0.4,
	animations: {
		() -> () in
		self.myButton.frame.origin.y += 20
	}, 
	completion: {
	(finished:Bool) -> () in
	print("finished: \(finished)")
	}
)
```
#### Abbreviated syntax
- *omission of the return type*: if the return type is already known to the compiler, you can omit the arrow operator and the specification of the return type
- *omission of the in expression when there are no parameters*: if the anonymous function takes no parameters, and if the return type can be omitted, the in expression itself can be omitted
- *omission of the parameter types*: if the anonymous function takes parameters and their types are already known to the compiler, the types can be omitted
- *omission of the parentheses*: if the parameter types are omitted, the parentheses around the parameter list can be omitted
- *omission of the in expression even when there are parameters*: if the return type can be omitted, and if the parameter types are already known to the compiler, you can omit the in expression and refer to the parameters directly within the body of the anonymous function by using the magic names $0, $1 and so on
- *omission of the parameter names*: if the anonymous function body doesn't need to refer to a parameter, you can substitute an underscore for its name in the parameter list in the in expression
- *omission of the function argument label*: if your anonymous function is the last argument being passed in this function call - which will just about always be the case - you can close the function call with a right parenthesis before this last argument, and then put just the anonymous function body without a label. This is called trailing closure syntax
	- if you have multiple anonymous functions the first one does not take a label and the rest do
- *omission of the calling function parentheses*: if you use a trailing closure, and if the function you are calling takes no parameters other than the function you are passing to it, you can omit the empty parentheses from the call. This is the only situation in which you can omit the parentheses from a function call
- *omission of the keyword return*: if the anonymous function body consists of exactly one statement consisting of returning a value with the keyword return, the keyword return can be omitted 
### Define-and-call
- defining an anonymous function and calling it all in one move
	- curly braces define an anonymous function body and the parentheses call that anonymous function. 
```swift
content.addAttribute(
	.paragraphStyle,
	value: {
		let para = NSMutableParagraphStyle()
		para.headIndent = 10
		para.firstLineHeadIndent = 10
		return para
	}(),
	range: NSRange(location:0, length:1))
```