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
- in general UI interaction is programmed with a standard series of steps:
	1. Create a UI object in the scene (e.g. buttons)
	2. Write a script to call when the UI is operated [[UIController]]
	3. Attach that script to an object in the scene (can use an empty object)
	4. Link UI elements (e.g. buttons) to the objects with that script

- for buttons add an `OnClick` entry to the button and drag the controller object onto it. Look. in `UIController` and select `OnOpenSettings()` in that section
### Creating pop-up window
- create a new image for the UI. Popup will be a *sliced image*
	- a sliced image is split into nine sections that scale differently from one another. As you can scale the edges and middle separately you can ensure sharp crisp edges
	- to set up the nine borders, select the popup sprite in the Projects view, in Inspector find Sprite Editor button
- create a script for the popup [[SettingsPopup]]
	- Add button to be the child of the popup and set it to close in the script
### Sliders and input fields
- use $GameObject \Rightarrow UI \Rightarrow InputField - TextMeshPro$ to create text field
- use $GameObject \Rightarrow UI \Rightarrow Slider$ to create the slider
- make the objects children of the pup-up

## Updating the game by responding to events
- To alert the UI of actions in the scene we can use a broadcast messenger system
	- scripts can register to listen for an event, other code can broadcast an event, and listeners will be alerted about broadcast messages
# Saving settings between plays by using PlayerPrefs
- one method is called `PlayerPrefs`
	- you don't worry about details to save small amounts of information
	- this isn't too useful for large amounts of data but good for settings
	- provides simple commands to get and set named values
	- example in [[SettingsPopup]]