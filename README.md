# Chris Tammik's free audio tools

This is a Unity project which contains some audio tools I built and hereby release under the MIT License.

Download the newest versions of the scripts by simply navigating to: \FreeAudioTools\UnityPackage and download the newest file (yyyymmdd).

When opening up the project for the first time, please open the scene `main.unity` and hit Play to run the scene. The main camera has a listener attached (as per the default in a new scene). 

Another component which was added to demonstrate the tool is the `PlaySoundExample.cs` script. It holds a reference to the `raindrops` prefab. When the scene is played, `PlaySoundExample` will load the raindrops prefab and call the Play() method on the `FullIndieAudioSound` component attached.

PlaySoundExample has some useful comments in its code which explain how the sound is being instantiated and played. If you set the stop variable to true, the sound will stop.

The FullIndieAudioSound is a script that allows basic control over audio settings. It is an instance-based system, which means audio behaviour needs to be defined per sound effect and stored in a prefab (Unity's GameObject preset). To play a sound, the prefab must be instantiated.

- Play On Awake starts the sound as soon as the script wakes. Alternatively, call the Play() method on the FullIndieAudioSound component.
- The volume is being shown in decibels in a range from 0 (no volume change) over -6dB (1/2 amplitude), -12dB (1/4 amplitude) all the way down to -80 dB (silence).
- Volume randomization ranges from zero to -12 dB.
- The pitch is being shown in semitones, with a range of -24 (two octave lower / 0.25x playback speed) over 0 (no change in pitch) up to +24 (two octave higher / 4x playback speed).
- Pitch randomization has a range of 0 up to +12 semitones. To achieve natural sounding results for sound effects this should not exceed 3-4 semitones of randomization.
- Retriggering retriggers the sound based on frame updates. A basic threshhold for the frame counter can be set and then a random starting offset for the counter reset can randomize timings. WARNING: frames are not a reliable source of timing!
- When retriggering is not enabled the looping option becomes available. If selected, it will loop whatever audio is being played. To stop a FullIndieAudioSound from producing sound you can call the StopAll method.
- If neither retrigger nor looping are enabled, the sound will play once and then wait for new Play() method calls.
- Low Pass filter and High Pass filter cut treble / bass frequencies respectively. This can be used to simulate a "muffled" effect such as a sound playing from another room, etc.
- Positional audio lets the Unity Audio Engine pan the sound left / right across the speakers / headphones according to it's position in 3D space in relation to the audio listener (should be attached to the main camera by default).
- If a spatialization plugin is selected in the Unity Project Audio Settings, and positional audio is enabled, the option to spatialize the sound for Virtual Reality becomes effective. This will enable the player to track sounds that are outside of their field of view.
- The falloff curve sould be set to "Logarithmic" if the game is a 3D game. For 2D games it is possible that the "Linear" option may sound better. Custom should not be used.
- The Min- and Max-Distance setting define how far away from the listener the sound starts to attenuate (minimum distance for falloff to take effect) / fall to silent (maximum audible range).
- If positional audio is disabled the sound will play through the playback speakers directly. If the sound is a stereo sound (like most music) the left channel will come out the left speaker and right out the right speaker. If the sound is mono, it will play through both speakers equally.
- Audio Clips is a list of all the audio files that are attached to a sound. You can add variations to the sound by adding multiple audio clips here. To add clips, simply drag and drop them onto the FullIndieAudioSound inspector interface. To accomplish this with mutiple clips at once, lock the inspector after selecting the sound prefab (little lock symbol in the top right).
