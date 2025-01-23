---
tags:
  - Unity
  - Script
---
- Communicates with a server
```cs
using System;
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.Networking;

public class NetworkService
{
    // URL to send request to 
    private const string xmlApi =
        "http://api.openweathermap.org/data/2.5/weather?q=Chicago, us&mode=xml&appid=APIKEY";

    private const string jsonApi =
        "http://api.openweathermap.org/data/2.5/weather?q=Chicago,us&appid=APIKEY";
    
    private const string webImage =
        "http://upload.wikimedia.org/wikipedia/commons/c/c5/Moraine_Lake_17092005.jpg";

    // Address server side script
    private const string localApi = "http://localhost/uia/api.php";

    private IEnumerator CallAPI(string url, WWWForm form, Action<string> callback)
    {
        // Create UnityWebRequest object in GET mode
        using (UnityWebRequest request = (form == null) ? UnityWebRequest.Get(url) : UnityWebRequest.Post(url, form))
        {
            yield return request.SendWebRequest();

            if (request.result == UnityWebRequest.Result.ConnectionError)
            {
                Debug.LogError($"network problem: {request.error}");
            }
            else if (request.result == UnityWebRequest.Result.ProtocolError)
            {
                Debug.LogError($"response error: {request.responseCond}");
            }
            else
            {
                callback(request.downloadHandler.text);
            }
        }
    }

    public IEnumerator GetWeatherXML(Action<string> callback)
    {
        // Yield cascades through coroutine methods that call each other
        return CallAPI(xmlApi, null, callback);
    }

    public IEnumerator GetWeatherJSON(Action<string> callback)
    {
        return CallAPI(jsonApi, null, callback);
    }
    
    // Callback takes a Texture2D instead of a string
    public IEnumerator DownloadImage(Action<Texture2D> callback)
    {
        UnityWebRequest request = UnityWebRequestTexture.GetTexture(webImage);
        yield return request.SendWebRequest();
        // Retrieve the downloaded image by using the DownloadHandler utility
        callback(DownloadHandlerTexture.GetContent(request));
    }

    public IEnumerator LogWeather(string name, float cloudValue, Action<string> callback)
    {
        // Define a form with values to send
        WWWForm form = new WWWForm();
        form.AddField("message", name);
        // Send a timestamp along with the cloudiness
        form.AddField("cloud_value", cloudValue.ToString());
        form.AddField("timestamp", DateTime.UtcNow.Ticks.ToString());

        return CallAPI(localApi, form, callback);
    }
}
```