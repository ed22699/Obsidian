---
tags:
  - Unity
---
## Importing sound effects
### Supported file formats
- compression reduces a file's size but accomplishes that by throwing out a bit of the information from the file, it is clever so the least important stuff is thrown out so still sounds good. However, is still a small loss of quality
	- choose uncompressed audio when the sound clip is short, longer clips should be compressed

| File type | Pros and cons                                                             |
| --------- | ------------------------------------------------------------------------- |
| WAV       | Default audio format on Windows. Uncompressed sound file                  |
| AIF       | Default audio format on Mac. Uncompressed sound file                      |
| MP3       | Compressed sound file; sacrifices a bit of quality for much smaller files |
| OGG       | Compressed sound file; sacrifices a bit of quality for much smaller files |
| MOD       | Music tracker file format. A specialised kind of efficient digital music  |
| XM        | Music tracker file format. A specialised kind of efficient digital music  |
- Music should be compressed in the final game, Unity can compress the audio after you've imported the file. When developing a game in Unity, you want to use uncompressed file formats even for lengthy music
	- You should always choose either WAV or AIF file format
	- Music tracker is a format that stores the notes and their intensity, this means notes can be used again, meaning music composed this way can be efficient, but is a fairly specialised sort of audio
### Importing audio files
- drag the files from their location on the computer to the Project view within Unity (create a folder called `Sound FX` to drag the files into)
- leave Force To Mono unchecked, often sounds are recorded in stereo, resulting in two waveforms in the file, one for the left ear/speaker and one for the right
	- to save on file size you might want to halve the audio information so that the same waveform is sent to both speakers rather than separate waves sent to the left and right speakers (normalise setting)
- preload audio data relates to balancing playback performance and memory usage. Will consume memory while the sound waits to be used but will avoid having to wait to lead. You don't want to preload long audio clips, turn it on for short sound effects
- Load in background will allow the program to keep running while the audio is loading; good idea for long music clips so that the program doesn't freeze, however, audio won't start playing right away. Usually you don't want this for shorter audios
- Load type controls how the data from the file will be loaded by the computer. Computers have limited memory and audio files can be large. Sometimes you want the audio to play while it's streaming into memory, saving the computer from needing to have the entire file loaded, but this give a bit of computing overhead so audio plays fastest when it's loaded into memory first. You can also choose if the loaded audio data will be in compressed form or will be decompressed for faster playback. For short clips choose Decompress on load
- compression format controls the formatting of the audio data that's stored, choose Vorbis to compress. Choose PCM for the shorter clips. ADPCM is a variation on PCM that occasionally results in slightly better sound quality
- Sample Rate Setting should be left at preserve sample rate
## Playing sound effects
- must define three parts `AudioClip`, `AudioSource` and `AudioListener`. This is broken up as Unity's support for 3D sounds uses different components to tell positional information that is used for manipulating 3D sounds
- 3D sounds have a specific location, volume and pitch are influenced by the movement of the listener
- *audio clip* is the sound file that we imported
- *audio source* is the object that plays audio clips (2D sounds must also be played by an audio source but their location doesn't matter)
- *audio listener* is the object that hears the sound projected from the audio sources
- Audio mixers are an advanced alternative way to control audio in Unity. They enable you to process audio signals and apply various effects to your clips
### Assigning a looping sound
- select $Audio \Rightarrow Audio \; Source$ to create an `AudioSource` component
- tell the audio source what sound clip to play, drag an audio file from the project view up to the audio clip slot in the inspector
- select both Play On Awake and Loop
	- play on awake tells the audio source to begin playing as soon as the scene starts
	- loop tells the audio source to keep playing continuously, repeating the audio clip when playback is over
### Triggering sound effects from code
- make changes to the [[RayShooter]] script
	- `PlayOneShot()` causes an audio source to play a given audio clip
## Using the audio control interface
- you need to create an [[AudioManager]], for this you need the [[Managers]] framework so [[IGameManager]], [[ManagerStatus]] and [[NetworkService]] are needed ([[NetworkService]] won't be used here)
### Volume control UI