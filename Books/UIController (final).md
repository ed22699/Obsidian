---
tags:
  - Unity
  - Script
---
- Description
```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using TMPro;

public class UIController : MonoBehaviour
{
    [SerializeField] TMP_Text healthLabel;
    [SerializeField] InventoryPopup popup;

    void Start()
    {
		OnHealthUpdated();
		popup.gameObject.SetActive(false);
    }

	void Update(){
		if (Input.GetKeyDown(KeyCode.M)){
			bool isShowing = popup.gameObject.activeSelf;
			popup.gameObject.SetActive(!isShowing);
			popup.Refresh();
		}
	}

    void OnEnable()
    {
        // Declare which method reponds to the ENEMY_HIT event
        Messenger.AddListener(GameEvent.HEALTH_UPDATED, OnHealthUpdated);
    }

    void OnDisable()
    {
        // When an object is deactivated, remove the listener to avoid errors
        Messenger.RemoveListener(GameEvent.HEALTH_UPDATED, OnHealthUpdated);
    }

    // Method called by Settings button
    public void OnHealthUpdated()
    {
		string message = $"Health: {Managers.Player.health}/{Managers.Player.maxHealth}";
		healthLabel.text = message;
    }
}
```