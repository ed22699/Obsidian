---
tags:
  - swift
---
- two types of properties
	- instance properties: default, lifetime is the same as the instance of the object
	- static/class properties: lifetime is the same as the lifetime of the object type
```swift
class Dog {
	static let staticProperty = "static property"
	let instanceProperty = "instance property"
	func printInstanceProperty() {
		print(self.instanceProperty)
	}
}

class Cat {
	func printDogStaticProperty() {
		print(Dog.staticProperty)
	}

	func printDogInstanceProperty() {
		let d = Dog()
		print(d.instanceProperty)
	}
}
```
## Computed Variable Initialisation 
```swift
let times : Bool = {
	if val == 1 {
		return true
	}
	else {
		return false
	}
}()
```
```swift
var now : String {
	get{
		return Date().description
	}
	set{
		print(newValue)
	}
}
```
- can use getters and setters
- can just have a getter but there must always be a getter
## Computed Properties
- useful for:
	- facade for a longer expression
	- facade for a elaborate calculation
	- facade for storage
## Property Wrappers
- if you have several computed properties that do the same thing you can use a property wrapper
```swift
@propertyWrapper struct Clamped {
	private var _i : Int = 0
	var wrappedValue : Int {
		get {
			self._i
		}
		set {
			self._i = Swift.max(Swift.min(newValue,5),0)
		}
	}
}

@Clamped var p
```
## Built-In Simple Types
- if you know the hex code for the unicode character you can write it as `let left TripleArrow = "\u{21DA}"`
- can input stuff into a string like so `let s = "You have \(n) widgets."`
- `...` is a closed range operator, `a...b` means everything from a up to and including b
- `..<` means everything from a up to but not including b