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

public class PlayerManager : MonoBehaviour, IGameManager
{
	private NetworkService network
    public ManagerStatus status { get; private set; }
    
    public int health { get; private set; }
    public int maxHealth { get; private set; }

    public void Startup(NetworkService service)
    {
        Debug.Log("Player manager starting...");
		network = service

		// Call the update method instead of setting variables directly
		UpdateData(50, 100);

        status = ManagerStatus.Started;
    }

	public void UpdateData(int health, int maxHealth){
		this.health = health;
		this.maxHealth = maxHealth;
	}

    // Other scripts can't set health directly but can call this function
    public void ChangeHealth(int value)
    {
        health += value;
        if (health > maxHealth)
        {
            health = maxHealth;
        }
        else if (health < 0)
        {
            health = 0;
        }
		if (health == 0){
			Messenger.Broadcast(GameEvent.LEVEL_FAILED);
		}

		Messenger.Broadcast(GameEvent.HEALTH_UPDATED);
    }

	// Reset the player to the initial state
	public void Respawn(){
		UpdateData(50, 100);
	}
}
```