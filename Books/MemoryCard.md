---
tags:
  - Unity
  - Script
---
- Code to create a basic card functionality. When the card is clicked the front is shown, it can also be flipped again
```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class MemoryCard : MonoBehaviour
{
    [SerializeField] GameObject cardBack;
    [SerializeField] SceneController controller;

    private int _id;

    public int Id
    {
        // getter function
        get { return _id; }
    }

    public void SetCard(int id, Sprite image)
    {
        _id = id;
        GetComponent<SpriteRenderer>().sprite = image;
    }
    
    // called when object clicked
    public void OnMouseDown()
    {
        // runs when object is currently active/visible
        // Checks the controller's canReveal property so only two cards are revealed at a time
        if (cardBack.activeSelf && controller.canReveal)
        {
            // sets the object ot inactive/invisible
            cardBack.SetActive(false);
            // Notify the controller when this card is revealed
            controller.CardRevealed(this);
        }
    }

    // Can hide the card again
    public void Unreveal()
    {
        cardBack.SetActive(true);
    }
}

```