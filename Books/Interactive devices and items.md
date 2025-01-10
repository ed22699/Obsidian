---
tags:
  - Unity
---
# Interactive devices
- interacting with items in a game if it be a door or a lamp, have very similar scripting behind it, in this the door code can be adapted for other interactions
## Opening doors with keypress
- create a door object out of a cube and write the [[DoorOpenDevice]] script
- to make the opening of the door less instant you can use tweens to make it open smoothly
- you also need a script to call the `Operate()` function, for this we'll use [[DeviceOperator]]
	- `OverlapSphere()` returns an array of all objects that are within a given distance of a given position
	- `DontRequireReciever()` method means no error will occur if nothing in that object receives the message
	- you can use the dot product to filter out any objects you are not facing
## Operating a colour-changing monitor
- place a cube on a wall and attach the script [[ColorChangeDevice]]
	- in this script `Color` varies between 0 and 1 rather than 0 and 255, this is common in most places
# Bumping into objects
## Push away and fall over
- by default, Unity doesn't use its physics simulation to move objects around
	- this can be enabled by adding Rigidbody component to the object
	- Unity's physics system will act only on objects that have a Rigidbody component 
- to have the player apply a force to the boxes, make an addition to [[RelativeMovement]]
## Trigger a device in the level
## Disappear on contact (for item pickups)