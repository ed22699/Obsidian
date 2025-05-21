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
## Localisation
- using different languages 
- this is controlled by localisation folders, this holds resources such as that concerning text, these are identified by their `.strings`
- you don't have to create or maintaining these files manually, instead you work with exported XML files in the standard `.xliff` format
- you need to modify the code for it to be localised, this can be done with `String(localized:comment:)`
```swift
let greeting = String(
	localized: "howdy",
	comment: "Alert title: Say hello"
)
```
### Exporting
- this generates the .strings files automatically
- for french:
	1. edit the target, make sure that the use compiler to extract swift stings build setting has been set to yes
	2. edit the project. In the info pane, under localisations, click the plus button, in the pop-up menu that appears, choose French
	3. choose $Editor \rightarrow Export \; for \; localization$, check french. This creates a folder
- you can modify the `fr.xliff` by supplying a `<target>` tag for every `<source>`
### Importing
- to incorporate it back into our project:
	1. edit the project
	2. choose $Editor \rightarrow Import \; Localizations$, locate and open the `fr.xcloc` bundle
> [!note] 
> Changing the distinct key (the english) will mess up these localisations, a workaround is instead of entering the English user-facing text as the `localized` parameter enter a key string then export the English localisation and "translate" the keys into the desired english user-facing text

## Distribution
- two primary types:
	- ad hoc distribution: providing a copy of your app to a limited set of known users that can test on specific devices
	- app store connect distribution: uploading the app to app store connect. Can be for one of two reasons:
		- TestFlight testing: temporary access for testing
		- App Store sale
### Making an Archive
- to create a copy of your app for distribution, you need to build an archive of your app. An archive is basically a preserved build. Has three purposes:
	- distribution: basis for subsequent distribution of the app, this will be exported from the archive
	- reproduction: every distribution from a particular archive contains identical binary and will behave in the same way. If a bug report arrives based on an app distributed from a particular archive, you can distribute that archive to yourself and run it, knowing that you are testing exactly the same app
	- symbolication: archive includes a `.dSYM` file that allows Xcode to accept a crash log and report the crash's location in your code. This helps you to deal with crash reports from users
- how to build:
	1. set destination in the Scheme pop-up menu in the project window toolbar to any iOS Device. 
	2. if you like, edit the scheme to confirm that the Release build configuration will be used for the Archive action (is the default but may want to check)
	3. choose $Product \rightarrow Archive$, the archive itself is stored in a date folder within your user archives folder. It is also listed in Xcode's Organiser window under the app's $Products \rightarrow Archives$ entry. In this window you can add a description and change the archive's name
- to export your archive, you need a distribution profile, hence a distribution certificate 
## Distribution Certificate
- just opt for automatic signing when you exprot to app store connect
## Distribution Profile
## Distribution for testing
- testflights are the better option
## Final preparations
- your marketing icon cannot be the same as the app icon but cannot be too different either
- needs a launch image
- screenshots must demonstrace actual user experience of the app
	- you can provide a screenshot corresponding to the screeen size and resolution of every device on which your app can run, or you can reuse a larger-size screenshot for smaller sizes
	- you can obtain these screenshots either from the simulator or from a device connected to the computer
		- choose $File \rightarrow Save \; Screen$ 