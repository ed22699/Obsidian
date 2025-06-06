---
tags:
  - Unity
---
- Unity supports multiple approaches to network communication, however, here we cover issuing HTTP requests
> [!note]
HTTP is a communication protocol for sending requests to and receiving responses from web servers (GET or POST)

- the Unity project is essentially a thick client that communicates with the server in an Ajax style
	- Video games often have much more stringent performance requirements than web applications, these differences can affect design decisions
	- Time scales can be vastly different between web apps and video games fast is more important here
- online games usually connect to a server specifically intended for that game
# Creating an outdoor scene
- we will be using weather data in the game for an example of connecting to the internet
- you need to have two textures that can be used on your skybox e.g. rainy and sunny
## Setting an atmosphere that's controlled by code
- create a shader that takes two sets of skybox images and transitions between them
	- create new shader script: $Create \; menu \Rightarrow Standard \; Surface \; Shader$ 
	- copy the code from [here](https://github.com/jhocking/from-unity-wiki/blob/main/SkyboxBlended.shader) and add it to the `skybox.shader` file
	- set your material to the Skybox Blended shader, this will give you 6 more slots where you can add the other skybox
- we now need to create a script to scroll the blend value and switch between scenes 
	- create an empty object in the scene and name it `Controller`
	- create a new script and name it [[WeatherController]]
## Downloading weather data from an internet service
- code will be structured around a [[Managers]] script, [[WeatherManager]] will be initialised from here and be in charge or retrieving and storing weather data. For this it will need to be able to communicate with the internet using the [[NetworkService]] script.
	- will need [[ManagerStatus]] and [[IGameManager]] altered slightly [[IGameManager (Internet)]], [[Managers]] will also be altered to [[Managers(Weather)]]
### Requesting HTTP data using coroutines
- the primary class for this is `UnityWebRequest` which communicates with the internet. Instantiating a request object using a URL will send a request to that URL
- co-routines are important here
	- first send a request, then you continue with the rest of the program, after some time you receive a response
- This will be written in [[NetworkService]]
#### Writing coroutine methods that cascade through each other
- `GetWeatherXML()` is the coroutine method that outside code can use to tell `Network-Service` to make an HTTP request
	- yielding can cascade through multiple methods. If the initial coroutine method itself calls another method, and that other method yields part of the way through, then the coroutine will pause inside that second method and resume there. Thus the yield statement in `CallAPI()` pauses the coroutine that was started in `GetWeatherXML()`
#### How the callback works
- `Action` type is a delegate. Delegates are references to some other method/function. They allow you to store the function (or rather the pointer to that function) in a variable and to pass the function as a parameter to another function

- You can update [[WeatherManager]] to use the [[NetworkService]]
## Parsing XML
- use [[Messenger]] and create a script called [[GameEvent (weather)]]
- once in place, adjust [[WeatherManager]]
## Parsing JSON
- alternative format for transferring data
- [[JSON (JavaScript Object Notation)]]
- Unity provides a `JsonUtility` class, also external developments like Json.NET
- [[NetworkService]] can be altered to also parse JSON files
- modify [[WeatherManager]] to request JSON instead
## Affecting the scene based on weather data
- once extracted we can use `SetOvercast()` method in [[WeatherController]]
## Game networking beyond HTTP
- form many games making a request and receiving a response is too slow
- for something like multiplayer FPS this would need a different approach
	- Unity provides an API for multiplayer games called MLAPI but other options include Mirror or Photon
# Adding a networked billboard
- besides text data images are also a common request. `UnityWebRequest` can be used to download images too
## Loading images from the internet
- Create a new manager module called [[ImagesManager]] which will be in charge of downloaded images to be displayed
	- connecting to the internet and sending the HTTP request will be handles in [[NetworkService]]
### Displaying Images on the billboard
- create a billboard object (create a cube object)
- need to create a device that operates just like the colour-changing monitor
	- use [[DeviceOperator]] and create a script for the billboard device called [[WebLoadingBillboard]]
### Caching the downloaded image for reuse
- Provide a callback function in [[ImagesManager]] that first saves the image and then calls the callback from [[WebLoadingBillboard]]
	- this is hard and requires lambda function to complete
		- *lambda (anonymous) function*: function that doesn't have a name, created on the fly inside another function
# Posting data to a web server
- an example of sending data
- this requires a server to send requests to
	- XAMPP is recommended for a test server
	- Once XAMPP is running, create a folder called `uia` in htdocs, this is where you'll put the server-side script
- this task is posting weather data to the server when the player reaches a checkpoint
	- checkpoint will be a trigger volume
## Tracking current weather: sending post requests
- the code for sending data will involve [[WeatherManager]] telling [[NetworkService]] to make the request. [[NetworkService]] handles the details of HTTP communication 
- create a [[CheckpointTrigger]] script
### Server-side code in PHP
- create a text file in htdocs and name it [[api.php]]