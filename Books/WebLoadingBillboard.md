---
tags:
  - Unity
  - Script
---
- Makes billboard interactable
```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class WebLoadingBillboard : MonoBehaviour
{
    public void Operate()
    {
        Managers.Images.GetWebImage(OnWebImage);
    }

    private void OnWebImage(Texture2D image)
    {
        // The downloaded image is applied to the material in the callback
        GetComponent<Renderer>().material.mainTexture = image;
    }
}
```