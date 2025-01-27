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

public class SettingsPopup: MonoBehaviour {
	[SerializeField] AudioClip sound;

	// Button will toggle mute property of AudioManager
	public void OnSoundToggle(){
		Managers.Audio.soundMute = !Manager.Audio.soundMute;
		// Play the sound effect when the button is clicked
		Managers.Audio.PlaySound(sound);
	}

	// Button will toggle mute property of AudioManager
	public void OnMusicToggle(){
		Managers.Audio.musicMute = !Manager.Audio.musicMute;
		Managers.Audio.PlaySound(sound);
	}

	// Slider will adjust the volume property of AudioManager
	public void OnSoundValue(float volume){
		Mangers.Audio.soundVolume = volume;
	}

	// Slider will adjust the volume property of AudioManager
	public void OnMusicValue(float volume){
		Mangers.Audio.musicVolume = volume;
	}

	public void OnPlayMusic(int selector){
		Managers.Audio.PlaySound(sound);

		switch (selector) {
			case 1:
				Managers.Audio.PlayIntroMusic();
				break;
			case 2:
				Managers.Audio.PlayLevelMusic();
				break;
			default:
				Managers.Audio.StopMusic();
				break;
		}
	}
}
```