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

	// Slider will adjust the volume property of AudioManager
	public void OnSoundValue(float volume){
		Mangers.Audio.soundVolume = volume;
	}
}
```