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
## Context Switching
- a change in thread context: code that has been running on the main thread proceeds to run on a background thread, or vice versa
- if we want to have some specific code run on a background thread we can use an actor
```swift
class ViewController: UIViewController {
	actor MyDownloader {
		func download(url: URL) async throws -> Data {
			//
		}
		func fetchManyURLs() async throws -> [URL:Data] {
			//
		}
	}
	let downloader = MyDownloader()
	override func viewDidLoad() {
		super.viewDidLoad()
		Task {
			// runs on the main thread
			// but fetchManyURLs runs on a background thread
			let result = try? await self.downloader.fetchManyURLs()
			// ...
		}	
	}
}
```
### Explicit Context Switching
- to prevent the Task initialiser from running on the main thread you can use `Task.detached`
	- this is a factory method; like the Task initialiser, the result is a Task object
	- difference is that `Task.detached` cuts off any relationship between the resulting Task object and the surrounding context, so the operation: function runs on its own background thread
```swift
class ViewController: UIViewController {
	override func viewDidLoad() {
		super.viewDidLoad()
		Task.detached {
			// runs on the background thread
			let result = try? await self.downloader.fetchManyURLs()
			// ...
		}	
	}
}
```
- the other situation is you are running on background code and must be on the main thread for an interface for example
	- if you want to step out onto the main thread just long enough to mutate a view's property we can call the special MainActor run static method:
		```swift
		await MainActor.run{ self.imageView?.image = image }
		```
	- this sort of deliberate context switching to the main thread can be expensive, if you have multiple operations to perform on the main thread and you need to call MainActor.run, try to clump those operations into a single call to MainActor.run, as not to switch contexts unnecessarily
## More Tasks
### Task Priority
- by default task priority is inherited from the surrounding context, but can be specified if wanted
### Sleeping
- `sleep()` is an async method that pauses your code for a length of time
### Yielding
- if a task takes significant time to run, and if it doesn't say `await` regularly, you might like to express a willingness to be suspended momentarily just in case other tasks are queued up waiting for threads to come free
	- call the Task `yield` static method to show this willingness 
	- basically sleeping for an unspecified time
### Cancellation
- if a task takes significant time to run, you might discover while the task is still running that you no longer need it to keep doing whatever it's doing, in this case it is possible to cancel the task
- two main ways to respond to the discovery that the task has been cancelled:
	- stop looping: examine `Task.isCancelled` at the top of the loop and break if it's true
	- throw: aborts your code immediately and sends a signal up the call chain
- cancelling subtasks
	- when a task is told to cancel, then if it has subtasks, those subtasks are told to cancel automatically
	- when a task group throws an error, the subtasks of that task group are told to cancel automatically