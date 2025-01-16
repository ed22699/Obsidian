---
tags:
  - Unity
  - Script
---
- Opens a door, either with a trigger or via a volume
```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class DoorOpenDevice : MonoBehaviour
{
    // Amound to offset the position by when the door opens
    [SerializeField] Vector3 dPos;

    private bool open;

    public void Operate()
    {
        if (open)
        {
            Vector3 pos = transform.position - dPos;
            transform.position = pos;
        }
        else
        {
            Vector3 pos = transform.position + dPos;
            transform.position = pos;
        }

        open = !open;
    }

    public void Activate()
    {
        // Open the door if not already open
        if (!open)
        {
            Vector3 pos = transform.position + dPos;
            transform.position = pos;
            open = true;
        }
    }

    public void Deactivate()
    {
        if (open)
        {
            Vector3 pos = transform.position - dPos;
            transform.position = pos;
            open = false;
        }
    }
}
```