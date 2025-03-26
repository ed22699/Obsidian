---
tags:
  - swift
---

**Take notes from notebook**
```swift
class Moi {
	let first = "Matt"
	let last = "Neuburg"
	let whole = self.first + " " + self.last // compile error
	// either make computed property
	var whole : String {
		self.first + " " + self.last
	}
	// or make lazy
	lazy var whole = self.first + " " + self.last
}
```
- the above issue is fine for static properties as they are lazy
## Enums
- instances represent distinct predefined alternative values
	- list of known possibilities
- you can assign values to the enums, these are known as *raw values*
```swift
enum Filter : String {
	case albums = "Albums"
	case playlists = "Playlists"
	case podcasts = "Podcasts"
	case books = "Audiobooks"
}

let type = Filer.albums
print(type.rawValue)
```
- raw values can have no case, aka they are optionals
	- can still compare without unwrapping
```swift 
let type = Filter(rawValue: "Albums")
if type == .albums{
//
}
```
- an optional is just an enum with two cases, `.none` and `.some`
- if you declare the enum with `Equatable` then you can compare
- if you declare the enum with `CaseIterable` it keeps a list automatically
- can have explicit initialisations as long as the choose one case
```swift
enum Filter : String, CaseIterable {
	case albums = "Albums"
	case playlists = "Playlists"
	case podcasts = "Podcasts"
	case books = "Audiobooks"
	init(_ ix:Int){
		self = Filter.allCases[ix]
	}
}

let type1 = Filter.albums
let type2 = Filter(rawValue:"Playlists")
let type3 = Filter(2)
```
- an enum instance property can't be a stored property
- enums can include methods
```swift
enum Shape {
	case rectangle
	case ellipse
	case diamond
	func addSahpe (to p: CGMutablePath, in r: CGRect) -> () {
		switch self {
		case .rectangle:
			p.addRect(r)
		case .ellipse:
			p.addEllipse(in:r)
		case .diamond:
			p.move(to: CGPoint(x:r.minX, y:r.midY))
			p.addLine(to: CGPoint(x: r.midX, y: r.minY))
			p.addLine(to: CGPoint(x: r.maxX, y: r.midY))
			p.addLine(to: CGPoint(x: r.midX, y: r.maxY))
			p.closeSubpath()
		}
	}
}
```
- an enum instance method that modifies the enum itself must be marked as `mutating`
- enum is a switch whose states have names, this is great when theres 5 or so things but even when there is only two things it can be better than a bool because it has names
	- can also store extra information in enums associated value or raw value
## Structs
- basically a class with less features
- struct doesn't need an explicit initialiser as it has no stored properties, or because all its stored properties are assigned default values as part of their declaration
- have implicit initialiser, if you create a explicit initialiser this will be lost
```swift
var d = Digit(123) // digit is a struct
print(d.number) // 123
var d2 = d
d2.number = 42
print(d.number) // 123 (because structs can't have multiple references, copies the struct rather than pointing to it)
```
## Classes
- classes are reference types - means they are:
	- mutable
		- with structs when you change values you are actually replacing the entire struct instance with another instance
	- can have multiple references
- classes can have a superclass that they inherit from
- to override inherited functions you must use the `override` keyword
- you can access the superclass with `super`
```swift
class Dog : Quadruped {
	func bark () {
		print("woof")
	}
}

class NoisyDog : Dog {
	override func bark () {
		for _ in 1...3{
			super.bark()
		}
	}
}
```
- classes can also have deinitialisers which use the `deinit` phrase, subclasses deinitialisers are called before the superclasses
- `static` members cannot be overridden, think of it as a `class final`
## Casting
- a way to get round the `Dog mark = NoisyDog()` issue where you cannot use methods unique to noisyDog
- Casting utilises the *as* keyword
	- it will let you cast a superclass to a subclass, this is known as *casting down*, if you use `as!` it will force the computer to do this, e.g. `d as! NoisyDog`
	- rather than forcing the `as` you can test it first with an `is`
```swift
func tellToHush(_ d:Dog){
	if d is NoisyDog{
		let d = d as! NoisyDog
		d.beQuiet()
	}
}
```
- you can also use `as?` to produce an optional
- you can bridge between swift and objective-c using the `as` keyword by itself, e.g. `s2 as NSString`
## Protocols
- protocols are swifts version of interfaces in java
## Generics
- a sort of placeholder for a type
	- an optional is an example of this with its `.some` case
```swift
enum Optional<Wrapped> : ExpressibleByNilLiteral {
	case none
	case some(Wrapped)
	init(_ some: Wrapped)
}
```
- here wrapped is a placeholder
- another use is in a function which should return the same class level as passed, e.g. dog should return a dog but noisyDog would rather return noisyDog
```swift
func dogMakerAndNamer(_ whattype:Dog.Type) -> WhatType {
	let d = WhatType.init(name:"Fido")
	return d
}
```
### Generic declarations
- using `Self` within methods in a protocol body so instances of protocol such as a class Dog can pass type `Dog` into the method
- `associatedtype` turns a protocol into a generic
- Generic functions can also be created like below
```swift 
func takeAndReturnSameThing<T> (_ t:T) -> T {
	print(T.self)
	return t
}
```
- generic object types can be created in a similar way to the function above (can have `var firstThing: T` within the struct of type `T`)
- can have multiple like `func flockTwoTogether<T, U>(_ f1:T, _ f2:U) {}`
### Type Constraints
- sometimes you want to compare your special `T` type, if you just did this it would cause a compile error, you will need to use `Comparable` like so `func myMin<T:Comparable>(_ things:T...) -> T {`
### Explicit Specialisation
- two forms
	- generic protocol with associated type - resolve an associated type manually through a type alias equating the associated type with some explicit type
	- generic object type - use the same angle bracket syntax used to declare the generic in the first place, with the actual type name in the angle brackets
- you can subclass generic classes like so `class NoisyDog<T> : Dog<T> {}`
### Where Clauses
```swift
func flyAndWalk<T: Flier> (_ f:T) {}
// is the same as 
func flyAndWalk<T> (_ f:T) where T: Flier {}
```
## Extensions
- a way of injecting your own code into an object type that has already been declared elsewhere
## Umbrella types
### Any
- anything can be passed without casting
```swift
func anyExpecter(_ a:Any) {}
anyExpecter("howdy")
anyExpecter(String.self)
anyExpecter(Dog())
anyExpecter(Dog.self)
anyExpecter(anyExpecter)
```
- if you want a more specific type you will need to cast down, make it safe with an if
```swift
if anything is String{
	let s = anything as! String
}
```
### AnyObject
- empty protocol that all class types conform to automatically
- useful when you want to take advantage of the behaviour of Objective-C id
## Collection types
- array 
	- arrays are a generic
	- are a value type
	- can create an array of three separate dogs (rather than 3 pointers) like so `let dogs = (0..<3).map {_ in Dog()}`
- dictionary
	- unordered collection of object pairs
	- must conform to the hashable protocol (equatable, implement an int hashValue property, equal keys have equal hash values)
```swift
var d = [String:String]()
// or
var d = ["CA": "California", "NY": "New York"]
// better to define explicitly
let state = d["CA"]
// if you want a default so no optional is returned
let state = d["CA", default:"N/A"]
```
- set
	- is an unordered collection of unique objects
	- type must be hashable and hence equatable
	- `let set : Set<Int> = [1, 2, 3, 4, 5]`
	- can be a quick way of uniquing the array as sets do not add duplicates so turning a set to an array will create this unique array
	- you can also filter sets in a venn diagram type way
```swift
let arr = [1,2,1,4,3,5,3,5]
let set = Set(arr)
let arr2 = Array(set) // [5, 2, 3, 1, 4]
```
- orderedSet and orderedDictionary
	- array plus hash table, elements must be unique unlike an array
