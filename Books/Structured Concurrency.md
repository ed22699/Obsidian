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