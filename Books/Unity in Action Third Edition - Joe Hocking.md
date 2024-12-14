---
title: Unity in Action, Third Edition
subtitle: Multiplatform Game Development in C#
author: Joe Hocking
authors: Joe Hocking
category: Computers
categories: Computers
publisher: Simon and Schuster
publishDate: 2022-02-08
totalPage: 414
coverUrl: http://books.google.com/books/content?id=77FYEAAAQBAJ&printsec=frontcover&img=1&zoom=1&edge=curl&source=gbs_api
coverSmallUrl: http://books.google.com/books/content?id=77FYEAAAQBAJ&printsec=frontcover&img=1&zoom=5&edge=curl&source=gbs_api
description: Unity in Action, Third Edition teaches you to create games with the Unity game platform. It's many 2D, 3D, and AR/VR game examples give you hands-on experience with Unity's workflow tools and state-of-the-art rendering engine. This fully updated third edition presents new coverage of Unity's XR toolkit and shows you how you can start building with virtual and augmented reality.
link: https://books.google.com/books/about/Unity_in_Action_Third_Edition.html?hl=&id=77FYEAAAQBAJ
previewLink: http://books.google.co.uk/books?id=77FYEAAAQBAJ&printsec=frontcover&dq=Unity+in+action&hl=&as_pt=BOOKS&cd=2&source=gbs_api
isbn13: 9781617299339
isbn10: 1617299332
tags:
  - Book
Status: Reading
---
[[Books]]
key points:
- Unity is a professional-quality game engine used to create video games targeting a variety of platforms
- [Unity Git Ignore](https://github.com/github/gitignore/blob/main/Unity.gitignore)
## Interface
### Layout
- Project tab - browse through all the files 
- Scene tab - position objects in the current scene
- Toolbar - controls for working with a scene
- Hierarchy tab - drag and drop object relationships
- Inspector - lists information about selected objects, including linked code
- Console tab - test playing in Game view while watching error output
### Views
1. scene view is where you can see what the game world looks like and move objects around
> [!note]
Mesh object is a visual object in space

2. game view - when the game is running, what you see in this view is the game
- you can switch between these two views while the game is running, this can be useful for debugging
- you can move in the view move in the view using `ctr-alt`
- you can orbit in the view using `alt`
### Objects
- you can move, rotate and resize objects using `w`, `e`, and `r` respectively once the object has been selected
- using an empty object you can place a bunch of related objects inside it to be grouped appropriately, e.g. all the walls and floor can be grouped under an empty object called maze
- all scene objects are instances of the `GameObject` class. `GameObject` is a container for a bunch of components, it provides `MonoBehaviour` (the class all script behaviours inherit from) something to attach to
#### Lights
- point lights - all light rays originate from a single point and project out in all directions, like a light bulb
- spot lights - all light rays originate from a single point but project out in only a limited cone
- directional lights - all light rays are parallel and project evenly, lighting everything in the scene the same way like the sun in the real world
#### 3D moving player
1. make object (in this case it was a capsule)
2. replace the capsule collider with character controller
3. make the main camera a child to this object
### Scripts
[[MouseLook]]
- a frame is a single cycle of the looping game code
> [!note]
Code is written in a separate IDE, however, you should still click play in Unity rather than run in this other IDE

- to link a script to an object you drag it to that object, you will then see in the inspector menu that it has been linked
- public variables are exposed in the Inspector so that you can adjust the component's values after adding a component to a game object (serialising)
	- this this you can adjust the script for the individual object like any other attribute 
- defining an enum allows you to define by name rather than by numbers, this will display as a drop down menu in objects
	```cs
	public enum RotationAxes
	{
		MouseXAndY = 0,
		MouseX = 1,
		MouseY = 2
	}
	public RotationAxes = RotationAxes.MouseXAndY;
	```

