---
tags:
  - Unity
  - Script
---
- Manages the players details such as their health
```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class PlayerManager : MonoBehaviour, IGameManager
{
    public ManagerStatus status { get; private set; }
    
    public int health { get; private set; }
    public int maxHealth { get; private set; }

    public void Startup()
    {
        Debug.Log("Player manager starting...");

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