---
tags:
  - Unity
  - Script
---
- Communicates with the [[NetworkService]] to get the weather
```cs
using System;
using System.Xml;
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using Newtonsoft.Json.Linq;

public class WeatherManager : MonoBehaviour, IGameManager
{
    public ManagerStatus status { get; private set; }
    public float cloudValue { get; private set; }

    private NetworkService network;

    public void Startup(NetworkService service)
    {
        Debug.Log("Weather manager starting...");
        // Store the injected NetworkService object
        network = service;
        // Start loading data from the internet
        // StartCoroutine(network.GetWeatherXML(OnXMLDataLoaded));
        StartCoroutine(network.GetWeatherJSON(OnJSONDataLoaded));
        
        status = ManagerStatus.Initializing;
    }

    // Callback method after the data is loaded
    public void OnXMLDataLoaded(string data)
    {
        XmlDocument doc = new XmlDocument();
        // Parese XML into a searchable structure
        doc.LoadXml(data);
        XmlNode root = doc.DocumentElement;

        // Pull out a single node from the data
        XmlNode node = root.SelectSingleNode("clouds");
        string value = node.Attributes["value"].Value;
        // Convert the calue to a 0-1 float
        cloudValue = Convert.ToInt32(value) / 100f;
        Debug.Log($"Value: {cloudValue}");

        // Broadcast message to inform the other scripts
        Messenger.Broadcast(GameEvent.WEATHER_UPDATED);

        status = ManagerStatus.Started;
    }

    public void OnJSONDataLoaded(string data)
    {
        JObject root = JObject.Parse(data);

        JToken clouds = root["clouds"];
        cloudValue = (float)clouds["all"] / 100f;
        Debug.Log($"Value: {cloudValue}");

        Messenger.Broadcast(GameEvent.WEATHER_UPDATED);

        status = ManagerStatus.Started;
    }

    public void LogWeather(string name)
    {
        StartCoroutine(network.LogWeather(name, cloudValue, OnLogged));
    }

    public void OnLogged(string response)
    {
        Debug.Log(response);
    }
}
```