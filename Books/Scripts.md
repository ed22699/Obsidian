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