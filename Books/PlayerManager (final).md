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

        // These values could be initializes with saved values
        health = 50;
        maxHealth = 100;

        status = ManagerStatus.Started;
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

        Debug.Log($"Health: {health}/{maxHealth}");
    }
}
```