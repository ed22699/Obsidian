---
tags:
  - Unity
  - Script
---
- Controls weather in the game
```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class WeatherController : MonoBehaviour
{
    [SerializeField] Material sky;
    [SerializeField] Light sun;

    private float fullIntensity;


    void OnEnable()
    {
        Messenger.AddListener(GameEvent.WEATHER_UPDATED, OnWeatherUpdated);
    }

    void OnDisable()
    {
        Messenger.RemoveListener(GameEvent.WEATHER_UPDATED, OnWeatherUpdated);
    }
    
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        fullIntensity = sun.intensity;
    }

    private void OnWeatherUpdated()
    {
        // Use cloudiness value from WeatherManager
        SetOvercast(Managers.Weather.cloudValue);
    }

    // Adjust both the material's Blend value and the light's intensity
    private void SetOvercast(float value)
    {
        sky.SetFloat("_Blend", value);
        sun.intensity = fullIntensity - (fullIntensity * value);
    }
}
```