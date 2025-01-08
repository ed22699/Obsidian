---
tags:
  - Unity
  - Script
---
- Creates an instance from a prefab
- communicated with GUI
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
    private float speed = 3.0f;
    private const float baseSpeed = 3.0f;
    
    void OnEnable()
    {
        Messenger<float>.AddListener(GameEvent.SPEED_CHANGED, OnSpeedChanged);
    }
    
    void OnDisable()
    {
        Messenger<float>.RemoveListener(GameEvent.SPEED_CHANGED, OnSpeedChanged);
    }

    private void OnSpeedChanged(float value)
    {
        speed = baseSpeed * value;
    }
    
    void Update()
    {
        if (enemy == null)
        {
            // Copies prefab object
            enemy = Instantiate(enemyPrefab) as GameObject;
            WanderingAi wanderingAI = enemy.GetComponent<WanderingAi>();
            if (wanderingAI != null)
            {
                wanderingAI.speed = speed;
            }
            enemy.transform.position = new Vector3(0, 0.5f, 0);
            float angle = Random.Range(0, 360);
            enemy.transform.Rotate(0, angle, 0);
        }
    }
}
```