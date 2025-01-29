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

public class PlayerCharacter : MonoBehaviour
{
    private int health;
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        health = 5;
    }

    public void Hurt(int damage)
    {
		Managers.Player.ChangeHealth(-damage);
    }
}
```