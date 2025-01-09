---
tags:
  - Unity
---
- first position the player object and set up the camera to look at this player
- in the characters scratch folder we have a 
	- FBX item which is the model
	- TGA item which is the texture
- in the FBX model select how to handle Normals and change to calculate
	- Normals are direction vectors sticking out of polygons that tell the computer which direction the polygon is facing. This facing direction is used for lighting calculations
	- default is Import which uses the normals defined in the imported mesh geometry. If this is not correctly defined Unity will calculate a vector for the facing direction of every polygon
	- go to the materials tab, Extract materials, choose a folder, drag the TGA onto the material
## Shadows
- with directional light soft shadows can be set
- another way of handling shadows is *light mapping*
	- lightmaps are textures applied to the level geometry, with pictures of the shadows baked into the texture image
	- drawing shadows onto a model's texture is referred to as baking the shadows
	- these can be elaborate and realistic as created ahead of time, however this also means that they wont move
		- this makes it great for static objects like geometry but bad for dynamic objects like players
- you can used both lightmaps and real-time shadows by setting the Culling Mask property on a light so that real-time shadows are used only for certain objects
# Orbiting the camera around the player character
- camera should be independent of player
- camera code will move its position along with the character but will rotate independently of the character
- create the script [[OrbitCamera]] and attach to the camera before dragging the player character into the target slot
- the `LookAt()` method points an object at a target (not just for cameras)
- **Cinemachine** is a suite of tools for advanced camera control (in this case this would be overkill, however, is used in many projects)
# Programming camera-relative movement controls
- camera-relative
	- in first-person camera is placed include the character and moves with it so no distinction exists between the character's left and the camera's left
	- in third-person camera is outside the character, thus the camera's left may be pointed in a different direction to the character's left
	- most third-person games make their controls camera-relative
- this involves two primary steps:
	 1. rotate the player character to face the direction of the controls
	 2. move the character forward
## Rotating the character to face movement direction
- create the script [[RelativeMovement]], drag this onto the player and link the camera to the target property
### Smoothly rotating using lerp
- the `Quaternion.Lerp()` method smoothly changes between the current and target rotations
- this is interpolating, Lerp is linear interpolation, you can interpolate positions, colours or anything else
- slerp - spherical linear interpolation is another method that works better for slower turns
## Moving forward in that direction
- add character controller component to the player object $Component \Rightarrow Physics \Rightarrow Character \; Controller$
- changes should then be added to the [[RelativeMovement]] script
## Jumping
- first we add vertical movement to [[RelativeMovement]]
- we then add a minimum downward force, acceleration and terminal velocity all together producing the final script
- issue, slopes appear as solid ground you can jump off when checking for collisions on the bottom of the character
	- solution: use raycasting to detect the ground
	- cast a ray straight down from the player's position. If it registers a hit just below the character's feet, the player is standing on the ground
	- when the raycast doesn't detect ground below but the character controller is colliding with the ground the code should make the character slide off the ledge, will fall and push away from the ledge as the capsule would otherwise still hit the platform
- this 0.4 that comes in the [[RelativeMovement]] script is meant to be the height of the player plus the rounded ends, divided by two with some leeway, e.g. 1.9 instead of 2
- collisions with the character controller are reported through a callback function called `OnControllerColliderHit()`
# Setting animation on the player character
- can be created with a few approaches, most character animation in modern games use a technique called *skeletal animation*
	- in skeletal animation a series of bones is set up inside the model, and then the bones are moved around during the animation. When a bone moves, the model's surface linked to that bone moves along with it
	- can also be used in bendy objects such as tentacles, although the bones move rigidly, the model surface around the bones can bend and flex
1. turn on the animation system
	- select the player model in the Project view to see its Import settings
	- select the animation tab and make sure Import Animation is checked
	- go to Rig tab and switch Animation Type from Generic to Humanoid
2. define animation clips in the imported file
	- different movements happen at different times, e.g. walking, running, jumping
	- often imported animations come as a single long timeline that can be cut up into shorter individual animations
	- to split up animation clips, select the Animations tab in the inspector, find the Clips panel, use the + and - buttons to add and remove clips on the list
	- when you select a clip information will appear, you can rename, define start and end times, allowing you to slice chunks out of the longer animation
	- if start and end of looped animation are the same there is a green dot, if they are slightly off its a orange dot and if they're completely off its a red dot
3. set up the controller to play those animation clips
	- begin by creating a new animator controller asset $Assets \Rightarrow Create \Rightarrow Animator \; Controller$ 
	- in Project view find the icon with a funny-looking network of lines on it and rename it to player
	- select the character in the scene, it has a component called animator, this has a controller slot for you to link a specific animator controller, drag and drop
	- open animator $Window \Rightarrow Animation$ select Animator
	- drag animation clips to get new nodes (project view, click. the arrow on the side of the model asset, among the contents are the animation clips)
	- set idle as layer default state (turns orange) this is where the network starts, handle setup similar to that in [[Basic 2D Platformer#Animating player|2D Platformer]]
4. incorporate that animation controller in your code
	- this involves making changes to [[RelativeMovement]] script
- Unity has a sophisticated system for managing animations on models, called Mecanim
	- Mecanim identifies the newer more advanced animation system
	- one major advantage of this approach is that you can apply animations from other FBX files to a character. e.g. all human enemies can share a single set of animations