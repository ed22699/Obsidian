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
