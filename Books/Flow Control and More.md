---
tags:
  - swift
---

## Switch cases
```swift
switch i {
case 1:
	print("You have 1 thing")
case let n:
	print("you have \(n) things")
}

switch i {
case 1:
	print("You have 1 thing")
case 2...10:
	print("you have \(i) things")
default:
	print("you have more things than can count")
}
```
- patten can include boolean operators
- pattern can include condition to limit
- can include optionals
- can include `is` or `as` operators
- can wrap switch case in tuple
```swift
switch i {
case is Int, is Double:
	print("some kind of number")
default:
	print("not a number")
}
```
## Loops
- there is a repeat loop
```swift
repeat{
	statements
} while condition
```
## Jumping
- fallthrough - in a switch case aborts execution of the current case code and immediately begins executing the code of the next case
- continue - aborts execution of the current iteration and proceeds to the next iteration
- break - aborts the current construct and proceeds after the end of the construct 
## Aborting the whole program
- use `fatalError`
```swift
required init?(coder: NSCoder){
	fatalError("init(coder:) has not been implemented")
}
```
- when your program is made public you throw a build switch which tells the compiler that assert should be ignored. At this stage no assertion calls should be failing as all bugs should be ironed out.
## Guard
- when your code needs to decide whether to exit early, you can exit early if the condition fails
```swift
guard condition else {
	statements
	exit
}
```

## Privacy
- internal - default
- fileprivate - only visible within its containing file
- private - only visible within its containing curly braces
- public - visible even outside its containing module
- open - code in another module can subclass it
## Introspection
- letting an object display the names and values of its properties (intended for debugging)
	- introspect an object with `reflecting`
## Operators 
- infix - takes two parameters and appears between them
- prefix - takes one parameter and appears before it
- postfix - takes one parameter and appears after it
```swift
infix operator ^^
extension Int{
	static func ^^(lhs:Int, rhs:Int) -> Int{
		var result = lhs
		for _ in 1..<rhs {result *= lhs}
		return result
	}
}

print(2^^3) //8

let r2 = (1..<10).reversed()

infix operator >>> : RangeFormationPrecedence
func >>><Bound>(maximum: Bound, minimum: Bound)
	-> rReversedCollection<Range<Bound>>
	where Bound : Strideable {
		return(minimum..<maximim).reversed
}

let r2 = 10>>>1

```
## Memory Management
- when two class instances have references to one another you can have a *retain cycle* which will result in a *memory leak*, the two instance will never go out of existence
	- swift doesn't have garbage collection
	- can set for leak by implementing a class's `deinit` (method is called when class goes out of existence), is a bad sign if this method is never called
- one solution to a retain cycle is to mark the problematic reference as `weak`
	- weak reference means the object referred to can now go out of existence even while the referrer continues to exist
- another solution is to make the reference as `unowned`, good for when one object absolutely cannot exist without a reference to another but where this reference need not be a strong reference
## Miscellaneous Swift Language Features
### Synthesised Protocol Implementations
- some protocols can supply code behind the scenes so that an object that adopts the protocol will satisfy the protocol's requirements automatically
	- Equatable
	- Hashable
	- Comparable
### Key Paths
### Instance as Function
- you can treat instances as functions
```swift
struct Adder {
	let base: Int
	init(_ base:Int){
		self.base = base
	}
	func callAsFunction(_ addend:Int) -> Int{
		return self.base + addend
	}
}

let add3 = Adder(3)
let sum = add3(4)
print(sum) // 7
```
### Dynamic Membership
**notes p331**
- primary purpose of dynamic membership is to prepare swift for future interoperability with languages like Ruby
### Property Wrappers
- purpose will likely be to act as a facade
**code p333**
- property wrapper may also. vent a value that can be referred to elsewhere by the prefixing dollar sign ($), this is how SwiftUI `@State` attribute works, this is why when you use it you get the binding in return
### Custom String Interpolation
**Code p338**