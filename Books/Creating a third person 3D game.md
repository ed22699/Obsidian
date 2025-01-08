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