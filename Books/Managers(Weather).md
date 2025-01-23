---
tags:
  - Unity
  - Script
---
- Manages all the managers in the weather server example
```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

[RequireComponent(typeof(WeatherManager))]
[RequireComponent(typeof(ImagesManager))]
public class Managers : MonoBehaviour
{
    // Static properties that other code uses to access managers
    public static WeatherManager Weather { get; private set; }
    public static ImagesManager Images { get; private set; }
    
    // The list of managers to loop through during the startup sequence
    private List<IGameManager> startSequence;

    void Awake()
    {
        Weather = GetComponent<WeatherManager>();
        Images = GetComponent<ImagesManager>();

        startSequence = new List<IGameManager>();
        startSequence.Add(Weather);
        startSequence.Add(Images);

        // Launch startup sequence asynchronously
        StartCoroutine(StartupManagers());
    }

    private IEnumerator StartupManagers()
    {
        NetworkService network = new NetworkService();
        
        foreach (IGameManager manager in startSequence)
        {
            manager.Startup(network);
        }

        yield return null;

        int numModules = startSequence.Count;
        int numReady = 0;

        // Keep looping until all managers are started
        while (numReady < numModules)
        {
            int lastReady = numReady;
            numReady = 0;

            foreach (IGameManager manager in startSequence)
            {
                if (manager.status == ManagerStatus.Started)
                {
                    numReady++;
                }
            }

            if (numReady > lastReady)
            {
                Debug.Log($"Progress: {numReady}/{numModules}");
            }

            // Pause for one frame before checking again
            yield return null;
        }

        Debug.Log("All managers started up");
    }
}
```