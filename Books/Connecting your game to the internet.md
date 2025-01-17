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