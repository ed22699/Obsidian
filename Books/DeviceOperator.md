---
tags:
  - Unity
  - Script
---
- Allows player to interact with objects by clicking the `c` key
```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class DeviceOperator : MonoBehaviour
{
    // How far away from the player to activate devices
    public float radius = 1.5f;
    
    // Update is called once per frame
    void Update()
    {
        if (Input.GetKeyDown(KeyCode.C))
        {
            // Returns list of nearby objects
            Collider[] hitColliders = Physics.OverlapSphere(transform.position, radius);
            foreach (Collider hitCollider in hitColliders)
            {
                Vector3 hitPosition = hitCollider.transform.position;
                // Vertical correction so the direction won't point up or down
                hitPosition.y = transform.position.y;

                Vector3 direction = hitPosition - transform.position;
                // Send message only when facing right direction
                if (Vector3.Dot(transform.forward, direction.normalized) > .5f)
                {
                    // Tries to call the names function regardless of the target's type
                    hitCollider.SendMessage("Operate", SendMessageOptions.DontRequireReceiver);
                }
            }
        }
    }
}
```