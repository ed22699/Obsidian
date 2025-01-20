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