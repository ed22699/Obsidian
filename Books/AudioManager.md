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
	[SerializeField] AudioSource music1Source;
	[SerializeField] AudioSource music2Source;
	[SerializeField] AudioSource soundSource;

	[SerializeField] string introBGMusic;
	[SerializeField] string levelBGMusic;
	
	public ManagerStatus status {get; private set;}

	private AudioSource activeMusic;
	private AudioSource inactiveMusic;

	public flot crossFadeRate = 1.5f;
	private bool crossFading;


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
			if (music1Source != null && !crossFading){
				music1Source.volume = _musicVolume;
				music2Source.volume = _musicVolume;
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
				music1Source.mute = value;
				music2Source.mute = value;
			}
		}
	}

	public void Startup(NetworkService service){
		Debug.Log("Audio manager starting...");

		network = service;

		music1Source.ignoreListenerVolume = true;
		music1Source.ignoreListenerPause = true;
		music2Source.ignoreListenerVolume = true;
		music2Source.ignoreListenerPause = true;
		
		soundVolume = 1f;
		musicVolume = 1f;

		activeMusic = music1Source;
		inactiveMusic = music2Source;

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
		if (crossFading){ return; }
		StartCoroutine(CrossFadeMusic(clip));
	}

	public void StopMusic(){
		activeMusic.Stop();
		inactiveMusic.Stop();
	}

	private IEnumerator CrossFadeMusic(AudioClip clip){
		crossFading = true;

		inactiveMusic.clip = clip;
		inactiveMusic.volume = 0;
		inactiveMusic.Play();

		float scaledRate = crossFadeRate * musicVolume;
		while (activeMusic.volume > 0){
			activeMusic.volume -= scaledRate * Time.deltaTime;
			inactiveMusic.volume += scaledRate * Time.deltaTime;

			yield return null;
		}

		AudioSource temp = activeMusic;

		activeMusic = inactiveMusic;
		activeMusic.volume = musicVolume;

		inactiveMusic = temp;
		activeMusic.Stop();

		crossFading = false;
	}
}
```