---
tags:
  - Unity
---

- The primary kind of 2D art asset is called a *sprite*
	- *Sprites* are 2D images displayed directly on the screen, as opposed to images displayed on the surface of 3D models (*textures*)
	- technically, these sprites will be objects in 3D space, but they'll be flat surfaces all oriented perpendicular to the z-axis
## 2D Editor Mode and 2D Scene View
- 2D scene view controls how the scene is displayed within Unity; toggle the 2D button along the top of the Scene view to change between what the camera sees and the editor view
- if you open the Edit menu and select Editor from the project settings drop-down list you'll see the Default Behaviour Mode setting with selections for either 3D or 2D
	- setting the editor to 2D mode causes imported images to be set to Sprite
## Displaying 2D Images
- for a background it may be positioned at `0, 0, 5` this is because objects still need to be stacked. 
	- Lower Z values are closer to the camera, so sprites with lower Z values are displayed on top of other sprites.
	- Background sprite should be the highest Z value
> [!note]
Pixels Per Unit - In Unity one unit isn't necessarily one pixel, by default it is `100:1` (this is recommended as the physics engine doesn't work properly at `1:1`)

### Switching the camera to 2D mode
- regardless of whether the Scene view is set to 2D mode the camera in the game is set independently
- the most import setting is **projection**
	- select the camera in Hierarchy to show its settings in the Inspector, then look for the Projection setting. For 3D graphics, the setting should be Perspective, but for 2D graphics, the camera projection should be **Orthographic** 
		- Orthographic is the term for a flat camera view that has no apparent perspective
- camera size is half the screen height (also remember to divide by the pixel-to-units scale)
- camera should have a low Z position e.g. -100
- camera's clear flag should be solid colour instead of Skybox
- camera's background colour should probably be black
## Building object that reacts to clicks
- in order to respond when the player clicks them, the object needs to have a collider component
	1. select the root object in Hierarchy
	2. click the add component button in the inspector
	3. select Physics 2D and choose a box collider
- a script is also required, in the example [[MemoryCard]] is used
## Displaying Different images with same functionality
- Use an invisible `SceneController` component and instantiate clones of an object
	- image on the card will be changed within the script via `SpriteRenderer`
		- `SpriteRenderer` makes the GameObject into a sprite object and determines which sprite asset will be displayed
- the scripts used for this are [[MemoryCard]] and [[MemorySceneController]]
### Comparing Cards
- Coroutines can be used to allow us to pause before checking for a match, allowing the user to see both cards even if match was incorrect ([[Scripts#^24a786|Coroutines]])
## Creating a text display
- TextMeshPro package is a good approach to creating text displays
	- if it isn't already installed for the menu, choose $Window \Rightarrow Package \; Manager$ and scroll down to $TextMeshPro$ 
	- with the installed package you can create a TextMeshPro object in the scene by going to the GameObject menu and choosing $3D \; Object \Rightarrow Text - TextMeshPro$ 
		- if TMP Importer window appears import TMP Essentials
## Creating a reset button
- insert the sprite
- add a collider to this sprite
- add a script [[UIButton]]
- `component.SendMessage("Method")` is another way of doing `component.Method()`, this way is more generic and so can be used in many different areas however, it is also less efficient for the CPU
- `LoadScene()` is a method that can load different scenes or reset a game
	- everything from the current level is flushed from memory, and then everything from the new scene is loaded
	- you can exclude objects from this flush with `DontDestroyOnLoad()`
