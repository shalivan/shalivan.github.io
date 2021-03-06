---
title: Unreal Audio
description: Audio engine
categories:
 - PXL
tags:
- Unreal
- Game Dev
- Audio
- Real Time
permalink: /uaudio/
---


LOD for audio  files  



  - `send fx` - are those who work only on part of eg: send in a fn of distance (reverbm delay)
  - `bin` : quantize a spectrum to buckets cause cannot have continuous data
  - `stem` : segment of music  you can split audio to different layers of music
  - Virtualization - play when silent. (reserve voice so expensiveDefault condition - when out of source sound will stop !!!!


#### Audio files

<img align="right" src="/src/ue/audio/wav.png">

  Can drag and drop `waves`


#### Meta sounds
<img align="right" src="/src/ue/audio/cue.png">  
(Cue - legacy system)  Mixer.



#### BP
  - `fade out`
  - `play sound`
  - `play sound at location`
  - `re-triggers`


  ---
#  Sound Class <src="/src/ue/audio/class.png">

...

  ---
# Source
 Thing in the audio engine which actually generates audio in the audio renderer.  
Source Sound (which may be a SoundWave, a SoundCue, a Synth, etc.




---

#  Source Effects

- pre-distance attenuation and pre-spatialization.

<img align="right" src="/src/ue/audio/srcfx.png">

Audio effect which applies (a filter, a delay, an envelope, distortion,  ... )  to a single source ( SoundWave, a SoundCue, a Synth,)

<img  src="/src/ue/audio/srceffect.png">

.

<img align="right" src="/src/ue/audio/srcfxchain.png">

**Source Effect Chain** - Add `Source Effect Preset` to chain. wich u can add to: SoundWaves, Cues, or components

`Set Bypass Source Effect Chain Entry ` -  

**An Envelope Follower & listener** - is Old or new @synersdthesia?

---

# Submix

- occur after distance attenuation and spatialization.


<img align="right" src="/src/ue/audio/submix.png">


mix of individual sources. place where mixing hapen into a single buffer.    (u can put audio fx on submixes )




**Submix Effect** presets



<img align="right" src="/src/ue/audio/submixfxp.png">


place where mixing sound and u can add sound fx .  


<img  src="/src/ue/audio/submixeffect.png">

.

**Submix Effect Chain**  - to chain effects






------------

# Start Analyzing Output
Audio analysis live.

uzywana chyba w niagarze ?? i jest BP do tego.


# Synesthesia
Toolset for audio analyses.

### NRT
<img align="right" src="/src/ue/audio/nrt.png">

Links the analysis algorithm settings to the sound wave being analyzed.
Maintains the results of analysis as a uasset.
Provides Blueprint function access to the results.

#### ConstantQ
  higher quality (hi and low like spectrum fft) double frequencies is exponential
 growth so to visualize spectrum we must convert this log to human mapping.  

`Get Normalized Channel Constant Q At Time`    

##### Perceptual loudness
 (bit dif than envelope) take in amount  

 `Get Loudness At a Time`  

#####  On sets
 loudness and changing in loud  

 `Get Channel Onset between Times`  




---

## Time Sync

Audio Group      
Time Synth Clip   


## Quartz
Time Synth is a 'sample accurate clip sequencer' that is being utilized heavily for interactive music. However, it is lacking many features, so our plan to resolve this need is to bring the ability to "sample accurately" sequence clips to all sounds in the audio engine.

time synth > quartz

Retriger sound every time loop begins. to be sure
subsystem that handle and allow acces and recive dleegats from clocks (can multiple)

- timesync is old version


##### [Create new clock]
name
settings: quantization settings > time signature
 - 4/4
 - puls ovveride  / for odd metters 7/8 6/8 ....

##### [Get handle for clock]


##### [Set Beat Per Minute]
- set BPM

quntisation boundry


#####  [Set Tick Per Second]
Htz


### Play Quantized
on audio component it can be any specialized sound that play on audio component. np source buzz, sound que, sound wave.  

quantizet playback on specialized sounds on the world


##### Time signature
for musical timing
[Make QuartzTimeSignature] > [Quartz Clock settings]




framerate and callback freq
update rat must be smaller (callboacks in buffering syst )



---


# Sound fields
Encoding audio into in 3d space. Can use for source orientation lock ambience within word
`Ambisonic` is trying to represent sound with sound pressure around audoiopsphere. can be decoded with any speaker config.  not depend of speakers


import `ambix` file (but still .wav) but still can have 4 or more channels.  There are special tools to author them.

order:  
- 1 order relatively cheap but only for overall localisation
- higher order specific location

HOW TO
1. checkbox in wave that is ambisonic.
2. Enable spatialisation
3. in blueprint can set rotation of actor to infl. rot sound. https://youtu.be/wux2TZHwmck?t=5915

---

# Convolution reverb
A convolution filter.  (work on Impulse response. which u can record)  
Can simulate reverb or use recorded.


HOW TO:
0. record impulse wave
1. `RMB` on wave file: create impulse response  (settings: can set here premixing volume)
2. create new  `Submix Effect presets` of type: `submix convolution reverb presets` (settings:  reference impulse)
3. create `custom attenuation` > (settings:  `attenuation submix send` >> add list >> add submix as destination of send




---

# Modular Synth (component)


Modular Subtractive Synthesizer

Audio buses

`Note On` - Note 0-127 , velocity, duration


##### Synth bank

<img align="right" src="/src/ue/audio/synthbank.png">
<img align="right" src="/src/ue/audio/synthwavbank.png">

You can store synths patches and samples in banks:   

`Set Synth Presset` - (synth ref>get from array> break> synthpresste)

<img align="right" src="/src/ue/audio/synthclip.png">

**Synth Clips** - ??

---

# Granular Synth (component)

Wave player playing (usually) small pieces of the file (called grains)   Each grain can have its own settings, so in this way, it’s possible to play back dozens or even hundreds of audio grains from a single file all with different parameters.



---

# Niagara audio data interface

---

# Parameter Modulation (Beta to Production)
Upgrading features in 4.26, this new paradigm in game parameter modulation and mixing which will eventually replace the existing Sound Class and Sound Mix feature sets. This expands the power for sound designers to control audio in games, and allows the UE4 audio engine to modulate and control any audio parameter using a number of methods.

---


https://youtu.be/ONgxkAy3vpw   UE4: Audio Visualiser Tutorial  
https://youtu.be/822d1xNab14   Niagara Tutorial Audio Visualizer  
https://youtu.be/k5e5vdW5ITc    
https://youtu.be/9JBnEgXXR2E   Building an Ambient Sound System in UE4  
https://youtu.be/8XcHyu8yTN0  ArthursAudioBPs V8 (Synesthesia plugin examples, more musical Rollplates + + )  
https://youtu.be/wux2TZHwmck  State Of Audio in 4.25 | Inside Unreal  
https://youtu.be/7E0I93pZ7zs  UE4 New Audio Engine Early Access - Modular synth Basics  
https://youtu.be/upxldb4thUI  Sync Events To Audio In Unreal Engine (Repost)  
https://youtu.be/ix3oa7nB2VA?list=PL3kdAKmyto-lDIu3cUacNC1gyDvm0hC-L - dancing cubes Array !  

https://youtu.be/822d1xNab14  【UE4】Niagara Tutorial Audio Visualizer  
https://www.youtube.com/watch?v=k5e5vdW5ITc  
https://youtu.be/k5e5vdW5ITc  



---
UE Audio channels  
https://www.youtube.com/c/RussianPunchProductions/videos  
https://www.youtube.com/channel/UC_fUOKtkDh4sXao49dn0bNQ/videos  

Unreal engine audio  
https://forums.unrealengine.com/development-discussion/audio/116874-new-audio-engine-early-access-quick-start-guide    

synth   
https://learningsynths.ableton.com/oscillators/how-synths-make-sound  


https://youtu.be/wux2TZHwmck - first stream   
https://youtu.be/yce2t85MJD8 - blend audio   
