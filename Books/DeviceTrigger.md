---
tags:
  - Unity
  - Script
---
- Trigger for when items enter and exit a volume
```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class DeviceTrigger : MonoBehaviour
{
    [SerializeField] GameObject[] targets;
	public bool requireKey;	

    // Called when object enters trigger volume
    void OnTriggerEnter(Collider other)
    {
		if (requireKey && Managers.Inventory.equippedItem != "key")
		{
			return;
		}
        foreach (GameObject target in targets)
        {
            target.SendMessage("Activate");
        }
    }

    // Called when object leaves trigger volume
    void OnTriggerExit(Collider other)
    {
        foreach (GameObject target in targets)
        {
            target.SendMessage("Deactivate");
        }
    }

}
```