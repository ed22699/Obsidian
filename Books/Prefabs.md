---
tags:
  - Unity
---
- Prefabs are a flexible approach to visually defining interactive objects
	- they are fully fleshed-out game objects (with components already attached and set up) that don't exist in any specific scene but rather exist as an asset that can be copied into any scene
	- prefabs can be spawned from code
- a copy of a prefab is called an instance
- prefab - game object existing outside of any scene, instance - copy of the objet that's placed in a scene
- create prefab by dragging object down from Hierarchy view into the project view
- to instantiate the prefab we need to have an empty game object with the script for example see [[SceneController]]
- for a projectile prefab