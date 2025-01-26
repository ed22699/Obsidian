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

public class UIController: MonoBehaviour {
	[SerializeField] SettingsPopup popup;

	void Start() {
		// Initialises hidden pop-up
		popup.gameObject.SetActive(false);
	}

	void Update(){
		if (Input.GetKeyDown(KeyCode.M)){
			bool isShowing = popup.gameObject.activeSelf;
			popup.gameObject.SetActive(!isShowing);

			// toggles the cursor along with the popup
			if (isShowing){
				Cursor.lockState = CursorLockMode.Locked;
				Cursor.visible = false;
			}
			else{
				Cursor.lockState = CursorLockMode.None;
				Cursor.visible = true;
			}
		}
	}
}
```