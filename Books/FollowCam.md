---
tags:
  - Unity
  - Script
---
- For a 2D platformer game the camera will follow the player
```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class FollowCam : MonoBehaviour
{
    public Transform target;
    public float smoothTime = 0.2f;
    private Vector3 velocity = Vector3.zero;

    void LateUpdate()
    {
        // Preserve the Z position while changing X and Y
        Vector3 targetPosition = new Vector3(target.position.x, target.position.y, transform.position.z);
        // Smooth transition from current to target position
        transform.position = Vector3.SmoothDamp(transform.position, targetPosition, ref velocity, smoothTime);
    }
}

```