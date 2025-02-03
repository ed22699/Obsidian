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

[RequireComponent(typeof(PlayerManager))]
[RequireComponent(typeof(InventoryManager))]
[RequireComponent(typeof(AudioManager))]
[RequireComponent(typeof(MissionManager))]
[RequireComponent(typeof(DataManager))]
public class Managers : MonoBehaviour
{
    // Static properties that other code uses to access managers
    public static PlayerManager Player { get; private set; }
    public static InventoryManager Inventory { get; private set; }
    public static AudioManager Audio { get; private set; }
    public static MissionManager Mission { get; private set; }
    public static DataManager  { get; private set; }

    // The list of managers to loop through during the startup sequence
    private List<IGameManager> startSequence;

    void Awake()
    {
		// Persist object between scenes
		DontDestroyOnLoad(gameObject);
        Player = GetComponent<PlayerManager>();
        Inventory = GetComponent<InventoryManager>();
        Audio = GetComponent<AudioManager>();
        Mission = GetComponent<MissionManager>();

        startSequence = new List<IGameManager>();
        startSequence.Add(Player);
        startSequence.Add(Inventory);
        startSequence.Add(Audio);
        startSequence.Add(Mission);

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
				Messenger<int, int>.Broadcast(StartupEvent.MANAGERS_PROGRESS, numReady, numModules);
            }

            // Pause for one frame before checking again
            yield return null;
        }

        Debug.Log("All managers started up");
		Messenger.Broadcast(StartupEvent.MANAGERS_STARTED);
    }
}
```