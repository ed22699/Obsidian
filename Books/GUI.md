---
tags:
  - Unity
---
- HUD (*heads-up display*) superimposes graphics on top of the view of the world
	- a GUI superimposed on the Game view is referred to as the HUD
- *Immediate mode* refers to explicitly issuing draw commands every frame (e.g. [[RayShooter]] in the `OnGUI` section)
	- default buttons are about the only thing easy to create with this system
- *Retained mode* defines all the visuals once, and then for every frame the system knows what to draw without you having to tell it again
	- more setup but more polished results
	- you can see what the UI looks like while placing UI elements
	- makes it straightforward to customise the UI with your own images
- *UI Toolkit* is a third UI system, this book covers the second UI system Unity UI or uGUI
- make sure UI images are set to sprites
# Creating a canvas for the interface
- for a UI system all images must be attached to a canvas object
	- Cavas is a special kind of object that Unity renders as the UI for a game
- open GameObject menu, in the UI category choose Canvas
	- when canvas is created an EventSystem object is also created, this is required for UI interaction
- to view the canvas select 2D mode and double click the canvas in the Hierarchy 
- Render Mode Options:
	- `Screen Space - Overlay` renders the UI as 2D graphics on top of the camera view (default)
	- `Screen Space - Camera` renders the UI on top of the camera view, but UI elements can rotate for perspective effects
	- `World Space` places the canvas object within the scene, as if the UI were part of the 3D scene
- Pixel Perfect setting causes the rendering to subtly adjust the position of images so that they're always perfectly crisp and sharp
## Buttons images and text labels
- the UI section of the GameObject menu contains options to create an image, text, or button: $GameObject \Rightarrow UI \Rightarrow Image$, $GameObject \Rightarrow UI \Rightarrow Text - TextMeshPro$ and $GameObject \Rightarrow UI \Rightarrow Button - TextMeshPro$
- UI elements need to be a child of the canvas object
- Click set native size to resize objects to the ratio of their sprites used
- for a custom font for a Text import the font into Unity then choose $Window \Rightarrow TestMeshPro \Rightarrow Font \; Asset\; Creator$
## Controlling the position of UI elements
- All UI objects have an anchor, displayed in the editor as an X shape
	- the *anchor* is a flexible way of positioning objects on the UI
	- anchors can keep the objects rooted in place even when different monitors are used
	- anchor points can also adjust scale as well as position
## Programming invisible UIController