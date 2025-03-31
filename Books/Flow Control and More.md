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