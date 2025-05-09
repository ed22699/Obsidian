---
tags:
  - swift
---
## Environmental Dependencies
### Buildtime dependencies
- choices made at build time, affect the build process, including what the compiler does. Typical dependencies are:
	- version of Swift under which we're compiling
	- type of destination for which we're compiling - simulator or real device
	- a custom compilation condition defined for the current build configuration in the build settings
	- the action that causes the build - for instance, whether we're building to run or to archive
### Runtime dependencies
- type of device (iPad vs iPhone)
- the system version installed on this device
## Conditional Compilation
- is an if else kind of thing
- conditions include:
	- `swift(>=5.5), compiler(>=5.5)`
	- `targetEnvironment(simulator)`
		- means app can run coherently on the simulator even though the simulator lacks certain capabilities, such as the camera
	- `canImport(UIKit)`
	- custom compilation condition
- statements will not be compiled at all unless if the appropriate condition is met
## Build Action
## Permissible Runtime Environment
- environments in which your app is permitted to run, this is determined by build settings
	- device type: on which your app will run natively
		- iPhone: will run on iPhone or iPod touch, can also run on an iPad but not as a native iPad app; it runs in a reduced enlargeable window
		- iPad
		- iPhone, iPad: the app will run natively on both kinds of device; it is a universal app
	- iOS Deployment Target: the earliest system your app can run on
## Backward Compatibility
 - the complier will not allow you to run features not found on the older device as this would cause a crash
	 - can work around this with an availability check (`if #avalable(iOS 10.0, *){} else{}`)
## Device Type
## Arguments and Environment Variables
## Version Control
## Text Editing Preferences
- you can use the `MARK:` comment
## Multiple Selection
## Code Completion and Placeholders