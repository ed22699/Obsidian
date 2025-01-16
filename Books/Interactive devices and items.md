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
- open and close a door in response to the character colliding with another object in the scene
- create another door
- create a new cube to be used as a trigger and check Is Trigger for the collider, set the trigger object to Ignore Raycast layer (top right corner of the Inspector has a Layer menu), turn off Cast Shadows from this object
	- Rigidbody isn't required on the trigger as the player's character controller already fulfils the physics system enabled requirement
- triggers are often referred to as *volumes* rather than objects to conceptually differentiate solid objects from objects you can move through
- create a script for this trigger called [[DeviceTrigger]]
- you will also need to alter [[DoorOpenDevice]] script
## Disappear on contact (for item pickups)
- Create a sphere object and place it hovering at about waist height, make it small but otherwise prepare it like you did in the last volume example
- select the is trigger setting in the collider and set the object to ignore raycast layer
- create a new script to attach called [[CollectibleItem]]
	- remember to call `Destroy()` on `this.gameObject` and not just `this` as `this` only refers to the script component rather than the object its attached to
- rather an names items in more complex games often have an identifier used to look up further data. E.g. one item might be assigned ID 301 and ID 301 correlates to a certain display name, image, description, so forth
- turn these objects into prefabs
### Managing Inventory data and game state
- you need background data managers for the game's inventory
- will be similar to a MVC architecture
- idea is to split up all the data management into separate, well defined modules with each managing its own area of responsibility
	- create a module to maintain player state in [[PlayerManager]]
	- create a module to maintain the inventory list in [[InventoryManager]]
	- both [[PlayerManager]] and [[InventoryManager]] will be have like *model* in MVC
	- *controller* is an invisible object in most scenes (not required here but think back to [[SceneController]])
	- rest of the scene is analogous to *view*
	- a higher level *manager of managers* will keep track of all the separate modules, this will keep a list of all managers and will control the life cycles of various managers (in particular initialising them at the start). All other scripts will be able to access these centralised modules by going through the main manager
		- other code can use static properties in the main manager to connect with the specific module desired
	- for main manager to reference other modules in a consistent way, these modules must all inherit properties from a common base, for this we will use an interface ([[IGameManager]]) so the [[Managers]] object can treat both [[PlayerManager]] and [[InventoryManager]] as type [[IGameManager]] 
		- the enum within [[IGameManager]] is defined in [[ManagerStatus]]
	- design patterns for accessing centralised shared modules are the Singleton pattern, alternatively some use the service locator or the dependency injection
		- the code here uses a variation of the service locator
- create an empty GameObject and link the data managers to it ([[Managers]], [[PlayerManager]] and [[InventoryManager]])
> [!note]
> `Awake()` runs once when the code first starts running but even sooner then `Start()`, allowing for initialisation tasks that absolutely must run before any other code modules

### Storing Inventory
- the list of items collected could also be stores as a `List` object, for this we update [[InventoryManager]] and have [[CollectibleItem]] now call its new function
	- one issue of the list is that you will see multiple copies of the same item listed if multiple are picked up
- using a `Dictionary` makes it more simple to aggregate multiple copies of the same item (updates the [[InventoryManager]])
### Displaying in the UI
- This requires public methods for accessing items in the [[InventoryManager]]
- Add the UI images into a *Resources* folder in a subfolder called Icons
	- Resources folder can be loaded in code by using the `Resources.Load()` method
- Create a new empty GameObject names `Controller` and assign is a new script called [[BasicUI]]
## Equipping a key to use on locked doors
- adjust [[DeviceTrigger]] script and [[InventoryManager]] script
- update the functionality of the UI so that buttons can be used [[BasicUI]]
- click requireKey option in `DeviceTrigger`, now you will only be able to get through the door if you have a key
## Restoring the player's health by consuming health packs
- requires a new method in [[InventoryManager]] and a new button in [[BasicUI]]