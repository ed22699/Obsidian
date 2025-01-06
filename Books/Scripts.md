---
tags:
  - Unity
---
## Example Scripts
```dataview
TABLE WITHOUT ID file.link AS "Title"
From #Script and -"_templates"
WHERE file != this.file and contains(Tags, Unity)
```
## Notes
- a frame is a single cycle of the looping game code
> [!note]
Code is written in a separate IDE, however, you should still click play in Unity rather than run in this other IDE

- to link a script to an object you drag it to that object, you will then see in the inspector menu that it has been linked
- there are local and global variables, local move upon their own axes whereas global move upon the axis of the parent of which it is linked to
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
- movement speed is frame-rate dependent, this means different computers would allow for quicker or slower movement
	- multiply speed by delta time to make this frame-rate independent (see [[FPSInput]])
- to stop character going through walls you need to link the `CharacterController` for collision detection (see [[FPSInput]])
- `GetComponent<>()` method returns other components attached to the same GameObject
> [!note]
> for looking around and its effect on movement think about having only horizontal movement on the character and vertical movement on the camera, which is a child class, this means the downwards force will always point down

- `RequireComponent` attribute ensures all needed components are also attached to the object
- `AddComponentMenu` adds script to the component menu in Unity editor, if you tell the attribute the name of the menu item you want to add and then the script can be selected when you click add component at the bottom of the inspector
- Coroutines are a way of handling tasks that execute incrementally over time, in contract, most functions make the program wait until they finish ^24a786
	- Unity makes coroutines behave similarly to asynchronous functions through the use of enumerators and the `yield` keyword
- Rendering is the process of displaying the 3D scene into the 2D grid, calculating the colour of all the pixels through running an algorithm	
## Basic AI
Basic AI follows a loop and is ran with each frame, the aim is to have the AI always moving
1. Move forward a little bit
2. raycast forward to look for obstacles
3. turn away from obstacles
4. frame rendered, return to step 1

- finite-state machines - code structure in which the current state of the object is tracked, well-defined transitions exist between states, and the code behaves differently based on the state 
- to see the initials of a FSM see [[WanderingAI]]
- using `SerializeField` means that it cannot be altered by other scripts like `Public` variables can, however, it is still visible to the Inspector (see [[SceneController]])
- `OnTriggerEnter()` is called automatically when the object has a collision
	- for this the collider needs to be a trigger (check the Is Trigger check box in sphere collider checkbox)
		- collider component will still react to touching / overlapping other objects but will no longer stop other objects form physically passing through
	- will also need to be a rigid body so the physics system is able to register collision triggers for that object ($Physics \rightarrow Rigidbody$)