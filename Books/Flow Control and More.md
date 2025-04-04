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
