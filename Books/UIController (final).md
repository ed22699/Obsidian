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
    [SerializeField] TMP_Text levelEnding;
    [SerializeField] InventoryPopup popup;

    void Start()
    {
		OnHealthUpdated();

		levelEnding.gameObject.SetActive(false);
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
        Messenger.AddListener(GameEvent.LEVEL_COMPLETE, OnLevelComplete);
        Messenger.AddListener(GameEvent.LEVEL_FAILED, OnLevelFailed);
        Messenger.AddListener(GameEvent.GAME_COMPLETE, OnGameComplete);
    }

    void OnDisable()
    {
        // When an object is deactivated, remove the listener to avoid errors
        Messenger.RemoveListener(GameEvent.HEALTH_UPDATED, OnHealthUpdated);
        Messenger.RemoveListener(GameEvent.LEVEL_COMPLETE, OnLevelComplete);
        Messenger.RemoveListener(GameEvent.LEVEL_FAILED, OnLevelFailed);
        Messenger.RemoveListener(GameEvent.GAME_COMPLETE, OnGameComplete);
    }

    // Method called by Settings button
    public void OnHealthUpdated()
    {
		string message = $"Health: {Managers.Player.health}/{Managers.Player.maxHealth}";
		healthLabel.text = message;
    }

	private void OnLevelComplete(){
		StartCoroutine(CompleteLevel());
	}

	private IEnumerator CompleteLevel(){
		levelEnding.gameObject.SetActive(true);
		levelEnding.text = "Level Complete";

		// Show the message for two seconds then go to next level
		yield return new WaitForSeconds(2);

		Managers.Mission.GoToNext();
	}

	private void OnLevelFailed(){
		StartCoroutine(FailLevel());
	}

	private IEnumerator FailLevel(){
		levelEnding.gameObject.SetActive(true);
		levelEnding.text = "Level Failed";

		yield return new WaitForSeconds(2);

		Managers.Player.Respawn();
		Managers.Mission.RestartCurrent();
	}

	public void SaveGame(){
		Managers.Data.SaveGameState();
	}
		
	public void LoadGame(){
		Managers.Data.LoadGameState();
	}

	privae void OnGameComplete(){
		levelEnding.gameObject.SetActive(true);
		levelEnding.text = "You Finished the Game";
	}
}
```