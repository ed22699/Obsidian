---
tags:
  - swift
---
- receiving a communication from background code
	- how will the background code that gets the image talk to your code?
- running your own code in the background 
- concurrency was added in swift 5.5, apple refers to this suite of language features as structured concurrency
## Multithreading
### Main Thread
- the main thread is the interface thread, any code that affects or is triggered by the user interface has to run on the main thread
- your app's code generally runs on the main thread, in effect, while your app's code is running, the interface is frozen
	- usually a good thing, means the user cannot do anything else while your code is running
### Background Threads
- problematic particularly because of shared data
- you can implement a *lock* around your code
	- watch out for *deadlocks* and *race conditions*
### Asynchronous Code
- asynchronous code is code that might be called at an unknown time
```swift
func download(url: URL) {
	// obtain data task with a completion handler function
	let task = URLSession.shared.dataTask(with: url) { data, _, error in
		// some time later downloading finishes, completion handler function is called and if successful, we'll receive the data object
		if let data = data {
			// do something with the downloaded data
		}
	}
	// tell the data task to start downloading by calling resume
	task.resume()
}
```
- note above `task.resume()` will actually be done before the `data` line as that is asynchronous code
#### Returning a value
- instead of trying to return a value we need to pass our data to the completion handler
```swift
func download(url: URL, copletionHandler: @escaping (Data) -> ()) {
	// obtain data task with a completion handler function
	let task = URLSession.shared.dataTask(with: url) { data, _, error in
		// some time later downloading finishes, completion handler function is called and if successful, we'll receive the data object
		if let data = data {
			// do something with the downloaded data
			completionHandler(data)
		}
	}
	// tell the data task to start downloading by calling resume
	task.resume()
}
```
#### Throwing an error
- can't throw an error as anonymous function within the function
```swift
typealias MyCompletionHandler = (Result<Data, Error>) -> ()
func download(url: URL, copletionHandler: @escaping MyCompletionHandler {
	// obtain data task with a completion handler function
	let task = URLSession.shared.dataTask(with: url) { data, _, error in
		// some time later downloading finishes, completion handler function is called and if successful, we'll receive the data object
		if let data = data {
			// do something with the downloaded data
			completionHandler(.success(data))
		} else if let error = error {
			completionHandler(.failure(error))
		} else{
			fatalError("Should be impossible to get here")
		}
	}
	// tell the data task to start downloading by calling resume
	task.resume()
}
```
## Structured Concurrency Syntax
changes for swift 5.5:
- async code is marked
- async code runs in order
- async code can return a value
- async code can throw an error
### Async/Await
- await is used to call an asynchronous method
```swift
func download(url: URL) async throws -> Data{
	let result = try await URLSession.shard.data(from: url)
	return result.0
}
```
- await waits for async to finish
- you can only say await in an async context
### Tasks
- the basis of all asynchronous activity
	- async can only be called from within some task
- a task itself has no concurrency
	- while a task is running on a thread the same task cannot be running on a different thread
- task struct is a generic, parameterised on two placeholder types, success and failure
```swift
let url = URL(string: "https://www.apeth.com/pep/manny.jpg")
Task {
	do {
		let data = try await self.download(url: url)
		// do something with data
	} catch {
		print(error)
	}
}
```
### Wrapping a Completion Handler
- exactly one resume must be present 
```swift
func myDownload(url:URL) async throws -> Data {
	return try await withUnsafeThrowingContinuation { continuation in
		download(url:url) { result in 
			continuation.resume(with: result)
		}
	}
}
```
### Multiple Concurrent Task
#### Async let
- for a known finite number of subtasks
```swift
func fetchTwoURLs() async throws -> (Data, Data) {
	let url1 = URL(string:"https://www.apeth.com/pep/manny.jpg")!
	let url2 = URL(string:"https://www.apeth.com/pep/moe.jpg")!
	async let data1 = self.download(url: url1)
	async let data2 = self.download(url: url2)
	return (try await data1, try await data2)
}
```
#### Task Groups
- for an interment number of subtasks
- standard pattern is to loop through an array, however, this is very complicated
```swift
func fetchManyURLs() async throws -> [URL:Data] {
	let urls: [URL] = // ...
	return try await withThrowingTaskGroup(of: [URL:Data].self) { group in 
		for url in urls {
			group.addTask {
				return [url: try await self.download(url: url)]
			}
		}
		for try await d in group {
			result.merge(d) {cur,_ in cur}
		}
		return result
	}
}
```
### Asynchronous Sequences
- a type that conforms to the AsyncSequence protocol
### Actors
- structured concurrency is generally free to assign your code to any thread it chooses
- an actor is an object type flavour
	- you can have more than one reference to an actor instance
- to specify whether code should run on the main thread or on a background thread, you can associate that code with an actor
- actors help your multithreaded code run safely as actors protect against the possibility of mutating properties on more than one thread by isolating their properties
- when an actor's code is running, no other code belonging to the same actor can start
- behind the scenes there is an invisible global actor - the main actor - `@MainActor` attribute runs on the main thread