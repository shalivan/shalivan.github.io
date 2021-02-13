---
title: configs Circuit Novation
description: guide
categories:
 - DTA
tags:
- Audio
- Music

permalink: /circuit/
---

2 mininova oscillator engines. Circuit is not FM  synth. It does analog modeling  and wavetable synthesis.

[Music](/music/)  
[Synth](/synth/)  



https://www.youtube.com/watch?v=t9-nFVj468o  
https://www.youtube.com/watch?v=4_ggryrYdwc&t=129s    
https://youtu.be/3orEPK4h5yo  

# PC
.sys /.sysex  -  drum samples / patch  
.circuitpack  - whole pack  
midi device on windows:  


---

# Patch Editor Software


## Oscillator
- `Waveform` - wave shape  
- `index` -  (Shift waveform) / (can modulate with LFO) [matrix destination name: OSC1 Pulse Width]
- `Semitones` - Detune semitones up or down on octave (have multiple octave playing one note if add to oscillator 2)   
- `Cents` -  Cents detune (can detune oscillator 2)   
- `Detune` -  Density detune
- `Density` -  Density   
- `Interpolate` - Wave interpolate  
- `VSync` - Virtual Sync depth ?     



## Mixer  
- `Osc1` / `Osc2` - Add Oscillators to mix !  > can detune adding second oscillator and mix them on `mixer`  
- `Noise` -  Add noise
- `Ringmode` -    
- `PreFX` / `PostFX` -  


## Filter
Color and Shape of sound. Help filter out certain frequencies.

#### Filter
- Filter type
  - `Lowpass`,  `High pass`, `Bandpass`  - cut right, cut left, both    
  - `12dB`(more flat) sound is bassy more higher ,  `24dB` (more slope)  - cutoff slope. Greater value sooner cut off  (higher freq pass through)  
- Filter `Frequency` - How much to cut off filter, alter the tone of your sound from soft to sharp.
- Filter `Resonance` - End    


#### Mod
- `Key Track` 0-127 - change freq depend on how high on keyboard note is (higher keys higher freq) (if playing large range )
- `Env2 > Freq` +-64 - Add automatically Filter to react  on  Envelope 2 !!!!!!!!!
- `Q norm`

#### Drive
- `Type`
- `Drive` - distort / amplify going in to filter. dif types  (bit crush, rat reduce)


#### Bypass
- `Normal`, `O1 bypass`,  `O1+O2 bypass` - bypass filter in given oscillators !!!!!!!!!!!!!!!! What oscillator will be affected ! bypass will still affect noise and some settings

## Envelopes
3 Envelopes
Set Attack Decay Sustain Release

1. Velocity
2. Velocity
3. Delay

```
 1. Envelope Amplifier  (amplifier allow go sound through so 1 env will change loudness)
 2. Envelope Filter  
 3. Envelope Extra one  (you can  control by macro ) normally attack   
```




## LFO
2 LFOs

- `Waveform` - Wave shape
- `Slew` (as portamento or glide for LFO wave ) limits how quickly wave can change value  
- `Phase` - Shift tells LFO where in the wave to start
- [ ] `One Shot` -
- [ ] `Common Sync` -

#### Rate / Delay
- `Rate` - (can sync to temp )  Speed
- [ ] `Rate Sync` -
- `Delay` - (can sync to temp )with fade modes   
- [ ] `Delay Sync` -


- Delay Triger
  - `singiel` -  
  - `multi` -

- Sync style
  - `free` - not synced  
  - `Key Sync` - start with new key push

- Fade mode
  - fade in
  - out
  - gate in
  - out



## FX


#### Chorus / Phaser
- chorus is great


#### EQ   
- low mid high for freq and gain

#### Distortion
- `level`  
- `comp`   

#### Voice
Mono, Auto-Glide, Poly
- Portamento -  
- Pre-glide -   
- Keyboard Octave -

## Modulation Matrix


Up to 20 slots

|.||||
|-|-|-|-|
|Source 1
|Source 2 |Performance, LFO, Envelopes
|Depth
|Destination | Oscillator / Mixer / Filter / LFO / Envelopes


## Macros  
Combine up to 4 settings  in top knobs 1-8 for synths  
Set up in editor
- Set destination! WHAT TO CHANGE
- seto knob to 0
- set mini settings
- change knob to max
- change depth to where max should be (positive depth)

Depth, jak duzo zmiany i w ktora strone


#### Macro for drums


||fixed drums macro|
|-|-|
1 | Static pitch
3 | Decay envelope time
5 | Distortion
7 | Filter

#### Macro for synths

||Tracks|||Rhythm|
|-|-|-|-|-|
1 | Oscillator | Cutoff EG intensity  | filter cutoff - bring in out | Tune
2 |  Oscillator Mod | Cutoff  |Env2mod - how filter env  / lead arpeggio to softer sound | Start
3 | Amp Envelope | Resonance / Overdrive | attack | Length
4 | Filter Envelope | 50 % is for Attack/ Release | release | Slope
5 |  Filter Frequency |Vibrato, EFX Dry / wet / also chorus | lfo speed | Distortion
6 | Resonance | Performance: LFO speed / intensity, OSC Tune | modulation depth | HP
7 | Modulation | oscillator pitch | LP
8 | FX|Morph functions. Wavetable Positions, Oscillator A/B Ratio  | Resonance

trick
- modulate index with LFO  
- Env2mod - how filter env  

-------

# Circuit Hardware

- `notes`- Play  
- `velocity`-   (how hard is press) nie wszystkie mają głośność   Fixed Velocity is enabled by pressing Velocity 6 while holding down Shift 19 . Fixed Velocity
is confrmed by the Velocity button illuminating white while Shift is held down
- `gate`-  ile nut trwa dzwiek  
- `nudge`-  Cały pattern do przodu albo do tylu  Remember that when using Nudge with Patterns of less than 16 steps, the effect of Nudge is
restricted to the Pattern length. Steps outside the Pattern length will be unchanged.
- `length`- Dlugosc sekwncji  (ilość nut)  
- `patterns`  
- `mixer`- Mute  
- `fx`-  delay -{up}, reverbs - {bottom}   (global)  
- `side chain`-  on sustain things . will react to drum 1
right white knefels to more effect cutoff taki  


https://fael-downloads-prod.focusrite.com/customer/prod/s3fs-public/novation/downloads/10690/circuit-ug-en_0.pdf

---

### Scales:

**Root Note** - niebieski u góry  


||  |  | |||  | |
|---|---|---|---|---|---|---|---|
**17**| Natural Minor || <img src="/src/music/scales/patterns/NaturlMinor.png" width="200">
**18**| Major ||  <img src="/src/music/scales/patterns/Major.png" width="200">|
**19**| Dorian || <img src="/src/music/scales/patterns/Dorian.png" width="200">  |
**20**| Phrygian ||  <img src="/src/music/scales/patterns/Phrygian.png" width="200">  |
**21**| Mixolyduan  || <img src="/src/music/scales/patterns/Mixolyduan.png" width="200">   |
**22**| Melodic Minor| |<img src="/src/music/scales/patterns/MelodicMinor.png" width="200">|
 **23**|  Harmonic Minor ||<img src="/src/music/scales/patterns/HarmonicMinor.png" width="200">   |
  **24**| Bebop Dorian ||<img src="/src/music/scales/patterns/BebopDorian.png" width="200">
||  
**25** |  Blues  |(6)| <img src="/src/music/scales/patterns/Blues.png" width="200">   |
**26** | Minor Penatotonic | (6)|  <img src="/src/music/scales/patterns/MinorPenatotonic.png" width="200">  |
**27** |Hungarian Minor ||  <img src="/src/music/scales/patterns/HungarianMinor.png" width="200">|
**28**| Ukraninian Dorian| | <img src="/src/music/scales/patterns/UkraninianDorian.png" width="200">  |
**29**| Marva|| <img src="/src/music/scales/patterns/Marva.png" width="200"> |
**30** |Todi ||
**31**|Whole Tone | (6) |  <img src="/src/music/scales/patterns/WholeTone.png" width="200">
**32** |Chromatic|(12 keys)





---

# MIDI
### Key Mapping
type: Control Change
raw event: 11

|| Synth1 | Synth2 | Drum1 |Drum2  |Drum3 | Drum4  | Reverb| Delay |Filter |Mixer| Mixer   
|-|-|-|-|-|-|-|-|-|-|-|-|
|**channel** | **1** | **2** | **10** |**10**  |**10** | **10**  |**16**  |**16** |**16**|**10**| **16**  
knob1 |80|80|14||46||111|88|||12
knob2 |81|81||34||55|||||||
knob3 |82|82|15||47||112|89|||14
knob4 |83 |83||40||57
knob5 |84|84|16||48||113|90||12
knob6 |85|85||42||61|114|106||23
knob7 |86|86|17||49||115|109||45
knob8 |87|87||43||76|116|110||53|
filter|||||||||74

raw event: 10 keys 1-127


https://fael-downloads-prod.focusrite.com/customer/prod/s3fs-public/downloads/Circuit%20Programmers%20Reference%20Guide%20v1-1_0.pdf


---






---


```
- piano LFO 1 > destination: freq
- Source LFO +/- . Jak zmieniamy depth to 30 i -30 brzmi tak samo
- Source LFO + .
  - depth 20 .> 1/3
  - depth 25 > 1/5
  - depth 30 > interval of octve  (destinantion 1/2pitch)
- source: velo > destination LFO rate. give random
- LFO change another LFO: LFO 2 +/- , destination: LFO 1 rate destination2: Osc 1 Pulse Width   
```



- you can use wavetables



# Power Supply

1. Voltage must always be the same as that required by the device. (Tick)

2. Amperage on the adaptor must be same or higher than required by device (Tick)

3. Polarity must be the same (Is the power supply Centre Positive? (Tick?) This is the little symbol that looks like a C with a dot in the middle with a + and - on either side. If the Plus is pointing at dot in the middle it is center positive.

4. Power plug size

In regards to the amperage, think of amperage as how much current the power supply can handle safely without burning out. If the supply can deliver 1.5 amps and you only pull 1 amp then it is safe. (Never use a lower amperage power supply, it will probably burn up or catch fire if badly designed)


Not all USB cables are the same. The thickness of the wires that supply power to the device can be critical to both audio performance, and its resilience to static electricity. The best way to choose a cable is to look at the markings on the side. These will usually say '2725' and then another set of numbers containing 'AWG': '28AWG/1PR AND 24AWG/2C' or similar. The first number will always be 28AWG, and the second will be a number between 20 and 28. The lower this second number, the thicker the wire. If the printing just says '28AWG', this means 28AWG for both numbers. Focusrite recommends using cables where the second number is 24AWG or lower.

12 v 1250ma usb

------


# My Patches

piano - https://www.youtube.com/watch?v=LXrYyTmkaic



# Links


https://ledgernote.com/blog/interesting/musical-key-characteristics-emotions/

http://www.gradfree.com/kevin/some_theory_on_musical_keys.htm




#### Samples

https://trisamples.com/  
https://cymatics.fm/pages/free-download-vault  
https://www.noiiz.com/  
https://www.looperman.com/  
https://r-loops.com/  



```
- delete pattern not set tempo to 180
- side chain tab looks unused a lot of space > Arpeggiator
- abilities to preview last save difference (shift + session)
- delete all knob manipulation recordings (shift + clear )
- set start length (not always from 1 note let you nudge notes more ferally)
- able to nudge one note (there is a place in nudge mode)
- set gates length not only in record play mode
- slight color difference on sample swap (to know which are uses)
- Shift duplicate  - move (now its slow)
- remember sample names in software (bug)
- szybka kasacja samplke swapów i knobówhere
- - select aample + shift (change only in this stamp)
- notes lolonger than 2 patterns length
- MIDI 2.0
- drum page is empty
```
