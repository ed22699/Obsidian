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
	[SerializeField] AudioSource soundSource;
	
	public ManagerStatus status {get; privaet set;}
	public float soundVolume{
		get {return AudioListener.volume;}
		set {AudioListener.volume = value;}
	}
	public bool soundMute{
		get {return AudioListener.pause;}
		set {AudioListener.pause = value;}
	}

	private NetworkService network;

	public void Startup(NetworkService service){
		Debug.Log("Audio manager starting...");

		network = service;

		soundVolume = 1f;

		status = ManagerStatus.Started;
	}

	// Play sounds that don't have any other source
	public void PlaySound(AudioClip clip){
		soundSource.PlayOneShot(clip);
	}

}
```