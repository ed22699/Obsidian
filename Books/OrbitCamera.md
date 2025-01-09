---
tags:
  - Unity
  - Script
---
- For third person games, camera can orbit player
```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class OrbitCamera : MonoBehaviour
{
    [SerializeField] Transform target;

    public float rotSpeed = 1.5f;

    private float rotY;
    private Vector3 offset;
    
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        rotY = transform.eulerAngles.y;
        // Store the starting position offset between the camera and the target
        offset = target.position - transform.position;
    }

    // Update is called once per frame
    void LateUpdate()
    {
        float horInput = Input.GetAxis("Horizontal");
        if (!Mathf.Approximately(horInput, 0))
        {
            // Rotate the camera slowling using arrow keys
            rotY += horInput * rotSpeed;
        }
        else
        {
            // Rotate camera quickly with mouse
            rotY += Input.GetAxis("Mouse X") * rotSpeed * 3;
        }

        Quaternion rotation = Quaternion.Euler(0, rotY, 0);
        // Maintain the starting offset, shifted according to the camera's roation
        transform.position = target.position - (rotation * offset);
        // No matter where the camera is relative to the target, always face the target
        transform.LookAt(target);
    }
}

```