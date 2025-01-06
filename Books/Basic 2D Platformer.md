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