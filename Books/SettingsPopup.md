---
tags:
  - Unity
  - Script
---
- Broadcasts to the scene
- saves the name and speed through PlayerPrefs
- is a settings popup
```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;
using TMPro;

public class SettingsPopup : MonoBehaviour
{
    [SerializeField] Slider speedSlider;
    [SerializeField] TMP_InputField name;

    void Start()
    {
        speedSlider.value = PlayerPrefs.GetFloat("speed", 1);
        Messenger<float>.Broadcast(GameEvent.SPEED_CHANGED, speedSlider.value);
        name.text = PlayerPrefs.GetString("name", "Name");
    }
    public void Open()
    {
        // Turn the object on to open the window
        gameObject.SetActive(true);
    }

    public void Close()
    {
        // Deactivate this object to close the window
        gameObject.SetActive(false);
    }

    // Triggers when the user types in the input field
    public void OnSubmitName(string name)
    {
        PlayerPrefs.SetString("name", name);
    }

    // Triggers when the user adjusts the slider
    public void OnSpeedValue(float speed)
    {
        Messenger<float>.Broadcast(GameEvent.SPEED_CHANGED, speed);
        PlayerPrefs.SetFloat("speed", speed);
    }
}
```