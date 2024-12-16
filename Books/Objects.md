---
tags:
  - Unity
---
- you can move, rotate and resize objects using `w`, `e`, and `r` respectively once the object has been selected
- using an empty object you can place a bunch of related objects inside it to be grouped appropriately, e.g. all the walls and floor can be grouped under an empty object called maze
- all scene objects are instances of the `GameObject` class. `GameObject` is a container for a bunch of components, it provides `MonoBehaviour` (the class all script behaviours inherit from) something to attach to
#### Lights
- point lights - all light rays originate from a single point and project out in all directions, like a light bulb
- spot lights - all light rays originate from a single point but project out in only a limited cone
- directional lights - all light rays are parallel and project evenly, lighting everything in the scene the same way like the sun in the real world
#### 3D moving player
1. make object (in this case it was a capsule)
2. replace the capsule collider with character controller
3. make the main camera a child to this object

### Giving an object colour
- surface properties such as colour are controlled using materials
	- a material is a packet of information that defines the surface properties of any 3D object that the material is attached to (e.g. colour, shininess and even subtle roughness)
	- materials can be made through choosing $Assets \rightarrow