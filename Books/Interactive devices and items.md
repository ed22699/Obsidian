---
tags:
  - Unity
---
# Opening doors with keypress
- interacting with items in a game if it be a door or a lamp, have very similar scripting behind it, in this the door code can be adapted for other interactions
- create a door object out of a cube and write the [[DoorOpenDevice]] script
- to make the opening of the door less instant you can use tweens to make it open smoothly
- you also need a script to call the `Operate()` function, for this we'll use [[DeviceOperator]]
	- `OverlapSphere()` returns an array of all objects that are within a given distance of a given position
	- `DontRequireReciever()` method means no error will occur if nothing in that object receives the message
	- you can use the dot product to filter out any objects you are not facing