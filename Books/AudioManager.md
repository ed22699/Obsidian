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
	[SerializeField] AudioSource musicSource;
	[SerializeField] AudioSource soundSource;

	[SerializeField] string introBGMusic;
	[SerializeField] string levelBGMusic;
	
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
	private float _musicVolume;

	public float musicVolume{
		get {return _musicVolume;}
		set {
			_musicVolume = value;

			// Adjust volume of the AudioSource directly
			if (music1Source != null){
				music1Source.volume = _musicVolume;
			}
		}
	}

	public bool musicMute{
		get {
			if (music1Source != null){
				return music1Source.mute;
			}
			return false;
		}
		set {
			if (music1Source != null){
				musicSource.mute = value;
			}
		}
	}

	public void Startup(NetworkService service){
		Debug.Log("Audio manager starting...");

		network = service;

		music1Source.ignoreListenerVolume = true;
		music1Source.ignoreListenerPause = true;
		
		soundVolume = 1f;
		musicVolume = 1f;

		status = ManagerStatus.Started;
	}

	// Play sounds that don't have any other source
	public void PlaySound(AudioClip clip){
		soundSource.PlayOneShot(clip);
	}

	// Load intro music from resources
	public void PlayIntroMusic(){
		PlayMusic(Resources.Load($"Music/{introBGMusic}") as AudioClip);
	}

	// Load main music from resources
	public void PlayLevelMusic(){
		PlayMusic(Resources.Load($"Music/{levelBGMusic}") as AudioClip);
	}

	// Play music by setting AudioSource.clip
	public void PlayMusic(AudioClip clip){
		music1Source.clip = clip;
		music1Source.Play();
	}

	public void StopMusic(){
		music1Source.Stop();
	}
}
```