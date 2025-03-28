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