---
tags:
  - Unity
---
- raycasting is casting a ray into the scene
	- a ray is an invisible line in the scene that starts at a point of origin and extends out in a specific direction
- `ScreenPointToRay()` is a method that can be used to project a ray through the centre of the cameras view
- once you have a ray it can be passed to the `Physics.Raycast()` method to perform raycasting using that ray
- for a shooting example see [[RayShooter]]