---
tags:
  - Unity
  - Script
---
- Creates an instance from a prefab
```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class SceneController : MonoBehaviour
{
    // Serialized variable for linking to the prefab object
    [SerializeField] private GameObject enemyPrefab;

    // Keeps track of the enemy instance in the scene
    private GameObject enemy;
    
    void Update()
    {
        if (enemy == null)
        {
            // Copies prefab object
            enemy = Instantiate(enemyPrefab) as GameObject;
            enemy.transform.position = new Vector3(0, 0.5f, 0);
            float angle = Random.Range(0, 360);
            enemy.transform.Rotate(0, angle, 0);
        }
    }
}
```