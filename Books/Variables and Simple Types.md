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
## Variable Declaration