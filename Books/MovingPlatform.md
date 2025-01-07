---
tags:
  - Unity
  - Script
---
- Code to move a platform between the position in which it is placed and some end position
- has a gizmo to show the path the platform takes in the scene view
```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class MovingPlatform : MonoBehaviour
{
    // Position to move to
    public Vector3 finishPos = Vector3.zero;

    public float speed = 0.5f;

    private Vector3 startPos;

    // How far along the "track" between start and finish
    private float trackPercent = 0;
    // Current movement direction
    private int direction = 1;

    // Draws a gizmo to see the path the platform takes in the scene view
    void OnDrawGizmos()
    {
        Gizmos.color = Color.red;
        Gizmos.DrawLine(transform.position, finishPos);
    }
    
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        startPos = transform.position;
    }

    // Update is called once per frame
    void Update()
    {
        trackPercent += direction * speed * Time.deltaTime;
        float x = (finishPos.x - startPos.x) * trackPercent + startPos.x;
        float y = (finishPos.y - startPos.y) * trackPercent + startPos.y;
        transform.position = new Vector3(x, y, startPos.z);

        // Change direction both at start and end
        if ((direction == 1 && trackPercent > .9f) ||
            (direction == -1 && trackPercent < .1f))
        {
            direction *= -1;
        }
    }
}
```