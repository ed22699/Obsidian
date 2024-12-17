## Art Assets
- an individual unit of visual information used by the game

| Type of art asset | Definition                                                                                                                                                                                     |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 2D image          | flat pictures. To make a real-world analogy, 2D images are like paintings and photographs                                                                                                      |
| 3D model          | 3D virtual objects. To make a real-world analogy, 3D models are like sculptures                                                                                                                |
| Material          | A packet of information that defines the surface properties of any object that the material is attached to. These surface properties can include colour, shininess, and even subtle roughness  |
| Animation         | Packets of information that define the movement of the associated object. These are detailed movement sequences created ahead of time, as opposed to code that calculates positions on the fly |
| Particle system   | An orderly mechanism for creating and controlling large numbers of small moving objects. Many visual effects, like fire, smoke. or spraying water, are created this way                        |
- Materials and particle systems are created within Unity, but the other art assets are created using external software
- Whiteboxing is blocking out the walls of the scene with blank geometry
	- closely associated with level design (the discipline of planning and creating scenes/levels in a game)
	- this is the foundation in which you typically build up from
- A floor plan is the simple layout of the level
- A texture is a 2D image being used to enhance 3D graphics

| File type | Pros and cons                                                                                                                                                                  |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| PNG       | Commonly used on the web. Lossless compression, has and alpha channel                                                                                                          |
| JPG       | Commonly used on the web. Lossy compression, no alpha channel                                                                                                                  |
| GIF       | Commonly used on the web. Lossy compression; no alpha channel                                                                                                                  |
| BMP       | Default image format for Windows. No compression; no alpha channel                                                                                                             |
| TGA       | commonly used for 3D graphics; obscure everywhere else. No or lossless compression; has an alpha channel                                                                       |
| TIFF      | commonly used for digital photography and publishing. No or lossless compression; no alpha channel                                                                             |
| PICT      | Default image format on old Macs. Lossy compression; no alpha channel                                                                                                          |
| PSD       | Native file format for Adobe Photoshop. No compression; has an alpha channel. The main reason to use this file format would be the advantage of using Photoshop files directly |
> [!note]
an alpha channel is used to store transparency information in an image. The visible colours come in three channels of information: Red, Green, and Blue. Alpha is an additional channel of information that isn't visible but controls the transparency of the image

- as alpha channel is used often in 3D graphics, an image that has an alpha channel is preferred
- the two recommended file formats for Unity textures are PNG, TGA and PSD

### Importing an image
- a tileable/seamless image is an image in which opposite edges match up when placed side by side. This way, the image can be repeated without any visible seams between the repeats
- you can find tileable images at [textures.com](https://www.textures.com/)
- the size (in pixels) of a texture should be in powers of 2
>[!warning]
Resources, Plugins, Editor, and Gizmos are special folders, avoid naming folders these

- typically each texture goes with a different material
	- Unity allows you to drop a texture onto an object and then it creates a new material automatically
	- the proper way to create a material is through $Assets \rightarrow Create \rightarrow Material$ 
- alter the tiling aspect in the material to change how much the pattern repeats itself
	- this is useful only for texturing whitebox geometry. In a polished game, the floor and walls will be built with more intricate art tools, and that includes setting up their textures
- A skybox is a cube surrounding the camera with pictures of the sky on each side. No matter what direction the camera is facing, it's looking at a picture of the sky
	- Unity can take care of this for you, go to $Window \rightarrow Rendering \rightarrow Lighting$ and switch to the Environment tab and see skybox material