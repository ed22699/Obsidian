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