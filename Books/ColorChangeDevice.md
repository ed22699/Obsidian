---
tags:
  - Unity
  - Script
---
- Randomly changes the colour of the object when triggered
```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class ColorChangeDevice : MonoBehaviour
{
    public void Operate()
    {
        Color random = new Color(Random.Range(0f, 1f), Random.Range(0f, 1f), Random.Range(0f, 1f));
        // Colour is set in the material attached to the object
        GetComponent<Renderer>().material.color = random;
    }
}

```