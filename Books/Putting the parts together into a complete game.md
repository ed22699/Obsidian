---
tags:
  - Unity
---
## Building action RPG by repurposing projects
### Assembling assets and code from multiple projects
#### Updating the managers framework
- create [[IGameManager (final)]] and [[Managers (final)]] and adjust [[InventoryManager (final)]] and [[PlayerManager (final)]]
#### Brining over the AI enemy
- copy over the [[WanderingAI]], [[ReactiveTarget]], [[Fireball]], [[PlayerCharacter]] and the [[SceneController]]
- also copy the Flame material, fireball prefab and enemy prefab
- adjust [[PlayerCharacter (final)]]
### Programming point-and-click controls: movement and devices
#### Setting up the top-down view of the scene
- raise the camera for an overhead view and adjust [[OrbitCamera (final)]]
#### Writing the movement code
- player movement is being controlled indirectly by clicking
	- this movement is useful for AI characters as well. Rather than using mouse clicks, the target position could be on a path that the character follows
- create a new script called [[PointClickMovement]] and replace the [[RelativeMovement]] component on the player
#### Operating devices by using the mouse
- create a base script that all devices inherit [[BaseDevice]]
- now alter [[ColorChangeDevice]] to inherit from script [[ColorChangeDevice (final)]]. As this inherits from [[BaseDevice]] it gets the mouse control functionality
- change [[PointClickMovement]] so it will not move for device interactions
	- create a new layer, select edit layers in the menu and type Ground in an empty layer slot. Make everything the player can walk on a ground layer
### Replacing the old GUI with a new interface
- Create a HUD via the canvas method
- use the same [[Messenger]] system as before and create a [[GameEvent (final)]]
- broadcast this to [[PlayerManager (final)]]
- to adjust the health label create [[UIController (final)]]
	- attach this to the Canvas and create an [[InventoryPopup]] script and attach to the Inventory Popup object
- adjust the [[PointClickMovement]] so clicking popup doesn't cause player to move
#### Implementing the inventory popup
- create the popup interface and write the code for [[InventoryPopup]]
	- remember to add the EventTrigger to all the images added in the item icons, don't assign event listeners as this is done in the [[InventoryPopup]] code
## Developing the overarching game structure
- making multiple levels will involve decoupling teh scene further from the [[Managers (final)]] back end
- create a new script called [[StartupEvent]]
### Controlling mission flow and multiple levels
- you want a single set of game managers shared by all scenes. To do this you create a separate Startup scene that initialises the managers and then shares that object with the other scenes of the game
- create a new managers for progress management called [[MissionManager]]
	- `LoadScene()` is useful for this
- add to the [[Managers (final)]] script
	- the `DontDestroyOnLoad()` ensures the object will still be there in the new scene
#### Separate scenes for startup and level
- because the game managers object will persist in all scenes, you must separate the mangers for individual levels of the game. In project view duplicate the scene and rename appropriately startup and level 1
	- delete level 1 game managers object and in startup delete everything other than game managers, controller, main camera, HUD Canvas and EventSystem. Adjust the camera by removing the [[OrbitCamera (final)]] component. Remove the script components on controller and delete the UI objects parented to the canvas
	- the controller object no longer has any script components so create a new [[StartupController]] script and attach
- add the two scenes to Build Settings. Choose $File \Rightarrow Build \; Settings$ and add open scenes to add both the scenes 
### Completing a level by reaching the exit
- to handle completion put an object in the scene for the player to touch, this will inform [[MissionManager]]. This involves the UI responding ot a message about level completion so you will need to add another entry to [[GameEvent (final)]]
- you will need to adjust [[UIController (final)]] to respond to [[GameEvent (final)]]
- for the completion object create a cube, select is trigger, turn off both cast and receive shadows in mesh renderer and set the object to ignore raycast layer.
	- Create a new material called objective and create the [[ObjectiveTrigger]] script
### Losing the level when caught by enemies
- add another entry in [[GameEvent (final)]]
- adjust [[PlayerManager (final)]] to broadcast the message when player's health drops to 0
- add a method to [[MissionManager]] to restart the level
- add another event to the [[UIController (final)]]
## Handling the player's progression through the game
### Saving and loading the player's progress
- Unity and Mono provide I/O functionality that you can use for this purpose
- first add `UpdateData()` to both [[MissionManager]] and [[InventoryManager (final)]]
- saving the data will involve a procedure referred to as *serialising* the data
- `PlayerPrefs` can be used to save only a handful of values but for the entire game create [[DataManager]] script
- Add the [[DataManager]] to the [[Managers (final)]]
- create save game and add game buttons in the level 1 HUD canvas and update [[UIController (final)]]
	- link the functions to OnClick listeners in the buttons
### Beating the game by completing three levels
- add to [[GameEvent (final)]]
- modify [[MissionManager]] to broadcast that message after the last level
- respond to the message in [[UIController (final)]]
#### Adding more levels
- you must keep the player object the floor object set to the ground layer, and the objective object, controller, HUD canvas and EventSystem on all new levels
- you ideally should move the HUD to a central place that is shared among levels. Use the Additive scene loading mode (p312)
- you will also need to adjust the [[MissionManager]] to load new levels, changing the `maxLevel`