---
tags:
  - Unity
  - Script
---
- Description
```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class BaseDevice: MonoBehaviour {
	public float radius = 3.5f;
	// Funciton runs when clicked
	void OnMouseUp(){
		Transform player = GameObject.FindWithTag("Player").transform;
		Vector3 playerPosition = player.position;

		// Correction to vertical position
		playerPosition.y = transform.position.y;
		if (Vector3.Distance(transform.position, playerPosition) < radius){
			Vector3 direction = transform.position - playerPosition;
			if (Vector3.Dot(player.forward, direction) > .5f){
				// Call Operate() if the player is nearby and facing
				Operate();
			}
		}
	}

	// Virtual marks a method that inheritance can override
	public virtual void Operate(){
	
	}
}
```