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

public class AudioManager: MonoBehaviour, IGameManager{
	public ManagerStatus status {get; privaet set;}
	private NetworkService network;

	public void Startup(NetworkService service){
		Debug.Log("Audio manager starting...");

		network = service;

		status = ManagerStatus.Started;
	}
}
```