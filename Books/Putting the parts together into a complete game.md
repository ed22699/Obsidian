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