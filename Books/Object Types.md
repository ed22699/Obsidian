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