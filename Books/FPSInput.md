---
tags:
  - Unity
  - Script
---
- Movement keys so player can move around space, with collisions and gravity set
- Communicated with GUI
```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

[RequireComponent(typeof(CharacterController))]
[AddComponentMenu("Control Script/FPS Input")]
public class FPSInput : MonoBehaviour
{
    private CharacterController charController;
    public float speed = 6.0f;
    public const float baseSpeed = 6.0f;

    public float gravity = -9.8f;

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
    
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        charController = GetComponent<CharacterController>();
    }

    // Update is called once per frame
    void Update()
    {
        float deltaX = Input.GetAxis("Horizontal") * speed;
        float deltaZ = Input.GetAxis("Vertical") * speed;
        Vector3 movement = new Vector3(deltaX, 0, deltaZ);
        // Limit diagonal movement to the same speed as movement along an axis
        movement = Vector3.ClampMagnitude(movement, speed);
        // Activates gravity upon object
        movement.y = gravity;

        movement *= Time.deltaTime;
        // Transform movement vector into global coordinates
        movement = transform.TransformDirection(movement);
        // Tell the characterController to move by that vector
        charController.Move(movement);

    }
}

```