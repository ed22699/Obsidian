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
## Snippets
## Navigation
- you can go back and navigate using `Cmd-Ctr-Left` and `Cmd-Ctr-Right`
- you can jump to definition with `Cmd-Ctr-J`
- open quickly with `Cmd-Shift-O`
## Finding
- you can do a global find with `Cmd-Shift-F`
## Running in the Simulator
- is powerful, can be used to:
	- slow animations 
	- simulate low on memory
	- simulate situations such as an incoming call
## Debugging
- `dump` has a console output that describes an object along with its class inheritance and its instance properties, by way of a Mirror object
## Testing
- unit tests
- interface tests
	- in the long run it is better to write the tests yourself but you can get started by recording actions and the code can be generated automatically
		1. in the test stub create a new empty line and leave the insertion point within it
		2. choose $Editor \rightarrow Start \; Recording \; UI \; Test$
		3. in the simulator tap the button in the interface. When the alert appears, tap OK to dismiss it
		4. return to Xcode and choose $Editor \rightarrow Stop \; Recording \; UI \; Test$. Also choose $Product \rightarrow Stop$ to stop running in the simulator
- you can view code coverage in the options pane. You can also choose $Editor \rightarrow Code \; Coverage$ to reveal it in the gutter
- you can also run performance testing by calling `measure(metrics:)` with an array of XCTMetric objects. This test will automatically run several times
- UI tests may sometimes be constructed for no other purpose than to take screenshots, these may be used on the app store
	- to do this call the XCUIElement `screenshot` method and call the XCTestCase `add` method to retain the actual screenshot
```swift
let screenshot = XCUIApplication().screenshot()
let attachment = XCTAttachment(screenshot: screenshot)
attachment.lifetime = .keepAlways
attachment.name = "OpeningScreen"
self.add(attachment)
```
## Test Plans
- you can create test plans through $Product \rightarrow Test \; Plan \rightarrow New \; Test \; Plan$
- you need to convert your scheme to use the test plans you want do this with $Product \rightarrow Scheme \rightarrow Convert \; Scheme \; to \; Use \; Test \; Plans$
## Massaging the Report
- you can add data to the report with the `self.add`, with this you can attach issues to your test report
## Clean
- good idea to do at some point
- cleaning removes the cruft. Cleaning removes the built app and all the intermediate build products that Xcode caches in order to construct it, this can often solve a problem
- can choose $Product \rightarrow Clean \; Build \; Folder$ which removes the entire build folder for this project. Or more extensive cleaning:
	1. choose $Product \rightarrow Show \; Build \; Folder \; in \; Finder$
	2. quit Xcode
	3. back in the finder, press Command-Up arrow twice. You're now in your user derivedData folder. Move all its contents to the trash
- on top of this you should also remove your app from the simulator
	- to clean out the current simulator while running the Simulator, choose $Hardware \rightarrow Erase \; All \; Content \; and \; Settings$
	- to clean out all simulators, quit the simulator and then say in terminal `% xcrun simctl erase all`
## Obtaining a Developer Program Membership
- you do not need an organisation program to distribute your built app, individual program is sufficient if you are a solo dev
- your developer program membership involves:
	- an apple ID: also allows you to post on Apple's development forums, download Xcode beta versions and so forth
	- a team name: you, under a single apple ID can belong to more than one team. On each team, you will have one or more roles dictating your privileges
- you should enter your developer program apple ID into the accounts preference pane in Xcode
## Signing an App
- an app that is not properly signed for a device will not run on that device. Signing requires:
	- an identity: represents apple's permission for a given team to develop
		- a private key: stored in the keychain on the computer. It identifies a computer where this team can potentially develop device-targeted apps
		- a certificate: virtual permission slip from Apple. Contains the public key matching the private key. With a copy of this certificate, any machine holding the private key can actually be used to develop device-targeted apps under the name of this team
	- a provisioning profile: virtual permission slip from apple uniting:
		- an identity
		- an app, identified by its bundle identifier
		- a list of eligible devices, identified by their unique device identifiers (UDIDs)
		- a list of entitlements: special privilege that not every app needs, such as the ability to talk to iCloud. This isn't always needed
- there are two types of identity, and hence two types of certificate and provisioning profile: development and distribution (production)
- apple is the ultimate keeper of all the information except the private key. To verify or obtain a copy of this information you will either:
	- the developer member centre: set of web pages. Click certificates, IDs & Profiles to access all features and information to which you are entitled by your membership type and role
	- Xcode: most things can be done through Xcode
## Automatic Signing
- a way to obtain and manage certificates and profiles in connection with a project. For new projects this is the default
## Manual Signing
## Managing Development Certificates and Devices
- if you have automatic signing this will be chill and will work itself out
## Profiling