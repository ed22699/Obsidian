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