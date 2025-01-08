---
tags:
  - Unity
  - Script
---
- Communicates with the scene, controls GUI aspects such as settings tab and scoreboard 
```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using TMPro;

public class UIController : MonoBehaviour
{
    private int score;
    [SerializeField] TMP_Text scoreLabel;
    [SerializeField] SettingsPopup settingsPopup;

    void Start()
    {
        score = 0;
        scoreLabel.text = score.ToString();
        // Close popup when game starts
        settingsPopup.Close();
    }

    void OnEnable()
    {
        // Declare which method reponds to the ENEMY_HIT event
        Messenger.AddListener(GameEvent.ENEMY_HIT, OnEnemyHit);
    }

    void OnDisable()
    {
        // When an object is deactivated, remove the listener to avoid errors
        Messenger.RemoveListener(GameEvent.ENEMY_HIT, OnEnemyHit);
    }

    // Method called by Settings button
    public void OnOpenSettings()
    {
        settingsPopup.Open();
    }

    private void OnEnemyHit()
    {
        // Increment score in response to event
        score += 1;
        scoreLabel.text = score.ToString();
    }
}
```