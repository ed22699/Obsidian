---
tags:
  - Unity
  - Script
---
- Mainly controls hover and clicking effects along with alerting the targetObject, running the chosen function from it
```cs
using UnityEngine;
using System.Collections;
using System.Collections.Generic;

public class UIButton : MonoBehaviour
{
    [SerializeField] GameObject targetObject;
    [SerializeField] string targetMessage;

    public Color highlightColor = Color.cyan;

    public void OnMouseEnter()
    {
        SpriteRenderer sprite = GetComponent<SpriteRenderer>();
        if (sprite != null)
        {
            // Tint the button when the mouse hovers over it
            sprite.color = highlightColor;
        }
    }

    public void OnMouseExit()
    {
        SpriteRenderer sprite = GetComponent<SpriteRenderer>();
        if (sprite != null)
        {
            sprite.color = Color.white;
        }
    }

    public void OnMouseDown()
    {
        // button size pops a bit when clicked
        transform.localScale = new Vector3(1.1f, 1.1f, 1.1f);
    }

    public void OnMouseUp()
    {
        transform.localScale = Vector3.one;
        if (targetObject != null)
        {
            targetObject.SendMessage(targetMessage);
        }
    }
}
```