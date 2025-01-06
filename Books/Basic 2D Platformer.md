---
tags:
  - Unity
---
- In 2D games whiteboxing is done with sprites rather than meshes 
	- for the platformer game we will use a blank image for a sprite
- Sprite sheets can be used for animation, multiple sprites are grouped into a single image
	- set Sprite Mode to Multiple
	- click Sprite Editor and click Slice, set Type to Grid By Cell Size and click Slice once size is correct, then save
	- to add this to the scene expand the sprite sheet and select the sprite you want
- remember to add collider and Rigidbody to the player along with Collider for the floor and blocks
	- Collider defines the shape for physics to act on, and the Rigidbody tells the physics simulation what objects to act on
	- Rigidbody needs Collision detection set to Continuous and Freeze Rotation Z turned on
- Unity applies a bit of acceleraton to arrow key input. That can feel sluggish for a platformer
	- increase Sensitivity and Gravity of Horizontal input to 6 to make it snappier (this is found in $Edit \Rightarrow Project \; Settings \Rightarrow Input \; Manager$)
## Animating player
- the Unity animation system is called *Mecanim* and it aims to control animation with minimal code
	- composed of two kinds of assets: *animation clips* and *animator controllers*
		- clips are individual animation loops to play
		- controller is the network controlling when to play animations (is a state machine diagram, different states will play different animations)
	- to create this do the following:
		1. select multiple frames and drag them into the scene
		2. this creates animations automatically
		3. after adding an Animator component to the Player, drag in the controller
	- only one animator is required so any others created along with other animations can be deleted
- to apply controller to character click add component to choose $Miscellaneous \Rightarrow Animator$
	- drag controller into the controller slot in the inspector, with the player still selected, open $Window \Rightarrow Animation \Rightarrow Animator$
		- animations in the animator window are displayed as blocks referred to as *states*, the controller switches between states when running 
		- conditions (parameters) can be used to choose the animations. These conditions can be altered using scripts such as [[PlatformerPlayer]]
		- connect states and use parameters to switch between them
## Making Player Jump
- by default gravity weakly affects the player, you can adjust this through the edit menu; $Edit \Rightarrow Project \; Settings \Rightarrow Physics \; 2D$, for the example we changed Gravity Y to -40
- A falling player sticks to the side of the floor, to change this add the $Physics \; 2D\Rightarrow Platform \; Effector \; 2D$ components to block and floor
	- this makes objects behave more like platforms in a platform game
	- you should also set Used By Effector on the collider and turn off Use One Way on the effector
- `AddForce()` adds an upward force to the Rigidbody and does so in impulse mode
	- *impulse* is a sudden jolt, as opposed to a continuously applied force
	- to stop the player jumping midair use the players collision box and look for overlapping colliders in an area of the same width just below the player
### Texturing the map
- one image for a level would be too large so a common solution are *tilemaps*
	- it is constructing a larger, combined image out of lots of small tiling images
	- uses small blocks that are repeated throughout the map so no single image is very large
	- an official tilemap system for Unity is available by looking for 2D Tilemap Editor in $Window \Rightarrow Package \; Manager$
	- you could also use an external library such as SuperTiled2Unity which imports tilemaps created in Tiled, a popular free tilemap editor
## Unusual Floors
### Slope
- set the duplicate floor objects rotation to `0, 0, -25` to create a slope
- player will slowly slide down when idle, to fix this turn off gravity for the player when they are standing on the ground and idle
### One-way Platforms
- platforms you can jump through but still stand on
- turn on the one-way setting for the Platform Effector Component
- set Order In Layer to `1` for the player to ensure when it jumps it goes in front of the other sprites
### Moving Platforms
- this requires the script [[MovingPlatform]]
- also requires changes to the players script so that they attach to moving platforms
	- this causes a scaling issue that can be fixed by counter-scaling
## Drawing custom gizmos
- Your scripts can draw custom helper images int he scene view
	- example is a gizmos that shows the movement path of the platform
	- Gizmos show only in the Scene view and not the Game view
	- for example see [[MovingPlatform]]
	- `DrawLine()` is used to define a line by using start and end points
	- `DrawRay()` is used to draw a line in a given direction (good for raycasts from AI characters)
- Gizmos also work in 3D games
