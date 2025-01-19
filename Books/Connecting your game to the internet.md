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
	- will need [[ManagerStatus]] and [[IGameManager]] altered slightly [[IGameManager (Internet)]]