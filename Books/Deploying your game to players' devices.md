---
tags:
  - Unity
---
- capable of building apps for the following platforms:
	- Windows PC
	- macOS
	- Linux
	- WebGL
	- Android
	- iOS
	- tvOS
	- Oculus VR
	- VIVE VR
	- Windows Mixed Reality
	- Microsoft HoloLens
	- Magic Leap
- in addition, by contacting the platform owners for access Unity can build for game consoles:
	- Xbox One
	- Xbox Series X
	- PlayStation 4
	- PlayStation 5
	- Nintendo Switch
- When you click Build, the first thing that comes up is a file selector so you can tell Unity where to generate the app package. Unity creates an executable app for the currently active platform
## Building for desktop
### Building the application
- go to $File \Rightarrow Build \; Settings$ 
- by default the current platform will be set to PC, Mac and Linux. If not correct click the correct platform from the list and click Switch Platform
- On the right-hand side of the window, you'll notice the Target Platform menu
	- this lets you choose between Windows, macOS and Linux
- once chosen click Build
### Adjusting player settings: Setting the game's name and Icon
- Build Settings, click Player Settings 
### Platform-dependent compilation
- unity provides compiler directives known as platform defines that can cause different code to run on different platforms, a link to all these are on p319
- some code assemblies only exist on one platform, [[PlatformTest]] shows how to write this
- you can change quality settings for different platforms
## Building for the web
### Building the game embedded in a web page
- in build settings switch the platform to WebGL
- you will need to run the game from a web server
### Communicating with JavaScript in the browser
- unity can communicate with the browser with messages going in both directions
- to send messages to the browser, you write JavaScript code into a code library
- for messages from the browser, JavaScript in the browser identifies an object by name, and then Unity passes the message to the named object in the scene
- create  [[WebTestObject]] and an empty object in the scene called JSListener
	- `DllImport` imports a function from the JavaScript library to use in C# code. Implies you have a JavaScript library
	- create a special folder called `Plugins` and within that create a folder called `WebGL`, put a file called [[WebTest]] in there that has the extension jslib 
- to send the other way Unity provides templates
- create a folder called WebGLTemplates directly under assets, this is where custom templates go. Create a subfolder names WebTest and put [[index.html]] in here
- once you make your custom template you need to tell unity to use this. Open the Player Settings and find WebGL Template in the web settings, change to WebTest
## Building for mobile: iOS and Android
### Setting up the build tools
#### Setting up iOS build tools
- this requires XCode
#### Setting up Android build tools
- unity can generate the final Android application (either an APK for android application package, or AAB for android app bundle), this requires pointing unity to the Android SDK, which includes the necessary compiler
### Texture compression
- image compression is trickier on android, as they are not all the same hardware
### Developing plugins
- the process of communicating with mobile plugins is similar to the process of communicating with the browser
- create a folder called Plugins and a subfolder for both Android and iOS
#### iOS Plugins
- create a script in Unity to handle the native code, call this [[TestPlugin]]
- create a script called [[MobileTestObject]], create an empty object in the scene and attach the script
	- this initialises the plugin object then calls plugin methods in response to touch input
- write the native code that [[TestPlugin]] references. For iOS with is in Objective C and or C (or swift) so you need both a .h file and a .mm file so create [[TestPlugin.h]] and [[TestPlugin.mm]]
#### Android plugins
- almost exactly the same, no changes to [[MobileTestObject]] are required. Make additions to [[TestPlugin]]
- the android plugins will only compile when unity is set to the android platform, in particular note the calls to AndroidJNI, this is the system within Unity for connecting to native android
	- in android activity is an app process
- the native Android code is required, you must be a JAR packaged 
- write [[TestPlugin.java]] that compiles into a JAR
## Developing XR (both VR and AR)
- XR stands for extended reality (this encompasses both VR and AR)
### Supporting virtual reality headsets
- install XR package and enable it in Project Settings
### AR foundation for mobile augmented reality
- create a new Unity project, go to Package Manager and install AR foundation, along with either ARKit XR (iOs) or ARCore XR (android) depending on which mobile platform you are developing for
- create a script called [[PlaneTrackingController]] and drag the script onto the Controllers object, drag AR Session Origin and AR Default Plane onto their component slots in the inspector
- planar surfaces should now be detected in the environment along with raycasting to show a cube 