---
title: Circuit Tracks
description: Configs, Patch Editor  
categories:
 - DTA
tags:
- Audio
- Music

permalink: /circuit/
---

https://isotonikstudios.com/wp-content/uploads/Circuit-Editor-Manual-ShiftSynth1.pdf

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

#  Components

Drums sample

|||||||||
|-|-|-|-|-|-|-|-|
KK | KK | SD | SD | CH | CH | OH | OH
TT|TT|P|P|V|V|V|V



# Patch Editor Software


## Oscillator
- [ ] **Waveform** - wave shape
- `Index` (OSC Pulse Width) -  Shift waveform.  
- `Semitones` - Multiple octave playing one note. Detune semitones up or down on octave.  setting it to +12 effectively shifts the oscillator tuning up one octave.
- `Cents` -  Cents detune. (1/100 of a semitone), ±50 tunes the oscillator to a quartertone
midway between two semitones.
- `Density` -  Density.   adds copies of the oscillator waveform to itself. Up to
eight additional virtual oscillators are used for this, depending on the value of the parameter.
This produces a “thicker” sound at low to medium values, but if the virtual oscillators are
detuned slightly (see Density Detune below), a more interesting effect is obtained.
- `Detune` -  Density detune. This parameter should be used in conjunction with the Density control
- `Interpolate` - Wave interpolate.  (value of 127 will create a very smooth transition, with the adjacent
waveforms blending together. With a value of zero the transitions will be abrupt and obvious)
- `VSync` - Virtual Sync depth?     



## Mixer  
Mix oscillator 1 and 2
- `Osc` - Add Oscillators to mix. Can detune adding second oscillator and mix them on mixer.  
- `Noise` -  Add noise
- `Ringmode` -    
- **PreFX** -
- `PostFX` -  


## Filter
Filter out certain frequencies. (Color and Shape of sound)

- [ ] **Filter type**: What to cutoff.  **Lowpass**  - cut right,  **High pass** - cut left, **Bandpass** - both / **12dB** (flat) sound is bassy (more higher freq), **24dB** (more slope) cutoff slope. Greater value sooner cut off.    
- [ ] **Bypass**: Which oscillator will be affected. **Normal**, **O1 bypass**,  **O1+O2 bypass**(will still affect noise and some settings)
- `Cutoff Frequency` Filter  - How much to cut off filter, alter the tone of your sound from soft to sharp.
- `Resonance` Filter - End    
- `Key Track` 0-127 - change freq depend on how high on keyboard note is (higher keys higher freq) (usefull if playing large range )
- `Env2 > Freq` +-64 - Add automatically Filter to react  on  Envelope 2 !!!!!!!!!
- **Q norm** - : This parameter alters the bandwidth of the peak created by the resonance control. The
value of filter res has to be set to something other than zero for this parameter to have any
effect. This feature enables the Filter section to emulate many of the filter responses found on
various classic analogue and digital synths
- `Drive` - distort / amplify going in to filter. dif types  (bit crush, rat reduce)
- [ ] **Drive Type** - Same as EFFECTS > DISTORTION

## Envelopes
3 Envelopes: **Velocity**, **Velocity**, `Delay`  

- `Attack`   
- `Decay`  
- `Sustain`   
- `Release`  

```
.
 1. Envelope Amplifier  (amplifier allow go sound through so 1 env will change loudness)
 2. Envelope Filter  
 3. Envelope Extra one  (you can  control by macro ) normally attack   

```



## LFO
LFO require destination to work. (Apply only in matrix)

- **Waveform** - Wave shape
- `Slew` (as portamento or glide for LFO wave ) limits how quickly wave can change value  shape of the LFO waveform. Sharp edges become less sharp as Slew is increased.
- **Phase** - Shift tells LFO where in the wave to start
- [ ] **One Shot** - o generate just a
single cycle of its waveform.
- [ ] **Common Sync** - LFOs are in use for pitch modulation (their most common application),
Common Sync is only applicable to polyphonic voices. It ensures that the phase of the LFO
waveform is synchronized for every note being played. When to set Off, there is no such
synchronization, and playing a second note while one is already pressed will result in an
unsynchronized sound as the modulations will be out of time
- `Rate` - (can sync to temp )  Speed /  LFO’s frequency. A value of zero stops the LFO, and most musical effects are
likely to use values in the 40~70 range,
 - [ ] **Rate Sync** - synchronized to aninternal/external MIDI clock. When set to Off, the LFOs run at a frequency set by the Rate
parameter
- **Delay** - (can sync to temp )with fade modes   
 - [ ] **Delay Sync** -
- [ ]  **Sync Style** - **Key Sync** / **Free** - start with new key push s Off, there is
no way of predicting where the waveform will be when a key is pressed.
- [ ] **Delay Triger** - **Singiel** / **Multi** - Fade/Gate parameters set by Fade
- [ ] **Fade mode**
  - **Fade In** - gradually increased over the time period set by the Delay parameter
  - **Fade Out** gradually... , leaving the note with no LFO modulation.
  - **Gate In** - onset of the LFO’s modulation is delayed by the time period set by Delay
parameter, and then starts immediately at full level.
  - **Gate Out** - The note is fully modulated by the LFO for the time period set by the Delay. At
this time, the modulation stops abruptly.



## Effects


### Chorus / Phaser
- [ ] **Chorus / Phaser** chorus is great
- `Rate`
 - Sync
- `Feedback`
- `Depth`
- `Delay`
- `Level`


### Equalizer   
- **low** **mid** **high** for freq and gain

#### Distortion
- `Level`  
- **Comp**   
- **Type**

||||
|-|-|-|
Diode | Simulation of analogue Circuitry producing distortion | progressively “squared-off” as the amount of distortion is increased.
Valve | Simulation of analogue Circuitry producing distortion | similar to Diode, but atextreme settings alternate half-cycles of the waveform are inverted.
Clipper | Simulation of a | digital overload.
Cross-Over | Simulation of the |  crossover distortion generated by bi-polar analogue Circuitry, (e.g., amplifier output stages)
Rectify |  All negative-going half-cycles are inverted  | simulating the effect of rectification.
Bit-Reducer | | Reproduces the “grainy” quality associated with lower bit rates, as found in older digital devices.
Rate-Reducer | |  Gives the effect of reduced definition and HF loss, similar to the use of a low sample rate.




#### Voice
- [ ] **Voice** - **Mono**, **Auto-Glide**, **Poly**
- `Portamento` -  
- **Pre-glide** -   
- **Keyboard Octave** -

## Modulation
4 macros per knob, 20 matrix slots

###  Modulation Matrix

|Source |||
|-|-|-|
|Performance | Velocity | How hard key pressed
|Performance | Keyboard
|LFO|LFO +
|LFO|LFO +-
|Envelopes| Envelopes


Depth | how far parameter will be adjusted |

|Destination |||
|-|-|-|
| Oscillator | Pitch | Modulate Pitch
| Oscillator| V sync  |
| Oscillator | Pulse width  | Modulate wavetable index
Mixer  | Levels |
Mixer  | RingMod 1*2 Lvl |
Filter | Drive Amount |
Filter | Frequency |
Filter | Resonance |
LFO  | Rate |
Envelopes | 1 Amp Decay |
Envelopes |  2 Filter Decay |



- diff: 2 sources 1 slot on single destination different 2 sources 2 slots on same destination

###  Macros  
Combine up to 4 settings  in top knobs 1-8 for synths  
Set up in editor
- Set destination! WHAT TO CHANGE
- seto knob to 0
- set mini settings
- change knob to max
- change depth to where max should be (positive depth)

Depth, jak duzo zmiany i w ktora strone



#### Macro for synths

||Tracks|Rhythm| Track Drums|
|-|-|-|-|
1 | Oscillator |  Tune | Static pitch
2 |  Oscillator Mod |  Start |
3 | Amp Envelope |  Length | Decay envelope time
4 | Filter Envelope | Slope |
5 |  Filter Frequency  | Distortion | Distortion
6 | Resonance | HP | -
7 | Modulation | LP |  Filter
8 | FX| Resonance | -


---

- Env2mod - how filter env  / lead arpeggio to softer sound   
- 50 % is for Attack/ Release  
- Resonance / Overdrive
- Vibrato, EFX Dry / wet / also chorus | lfo speed

Performance:
- LFO speed / intensity, OSC Tune
- modulation depth
- Morph functions. Wavetable Positions, Oscillator A/B Ratio



# Circuit Hardware


**Setup View** -  `Shift` + `Save`

**Advanced Setup View** - `Shift` while `powering on`  
 - 2 MIDI Out enable:  Duplicate button is green
 - Enable compressor FX button is green
 - note:  Easy Start Tool
**Save Lock** - `Shift` + `Save`  while `powering on`.


**Bootloader Mode** - Hold down the `Scales` , `Preset` and `Note`

Synth 1 and Synth 2 are lit; selecting either of these displays a pattern of illuminated pads; the
pattern represents the version numbers of the three firmware elements in binary form. You may need
to describe these patterns to Novation’s Technical Support Team in the event of a problem.

https://fael-downloads-prod.focusrite.com/customer/prod/s3fs-public/novation/downloads/10690/circuit-ug-en_0.pdf


---

### Scales

**Root Note** - niebieski u góry  




||  |  | |||  | |
|---|---|---|---|---|---|---|---|
| <img src="/src/music/scales/patterns/NaturlMinor.png" width="200">| <img src="/src/music/scales/patterns/Major.png" width="200">| <img src="/src/music/scales/patterns/Dorian.png" width="200"> |  <img src="/src/music/scales/patterns/Phrygian.png" width="200">  | <img src="/src/music/scales/patterns/Mixolyduan.png" width="200"> |<img src="/src/music/scales/patterns/MelodicMinor.png" width="200">     |<img src="/src/music/scales/patterns/HarmonicMinor.png" width="200">    |<img src="/src/music/scales/patterns/BebopDorian.png" width="200">
|**17** Natural Minor |**18** Major |**19** Dorian |**20** Phrygian |**21** Mixolyduan  | **22** Melodic Minor| **23**  Harmonic Minor | **24** Bebop Dorian |
<img src="/src/music/scales/patterns/Blues.png" width="200">   |<img src="/src/music/scales/patterns/MinorPenatotonic.png" width="200">  |<img src="/src/music/scales/patterns/HungarianMinor.png" width="200">|<img src="/src/music/scales/patterns/UkraninianDorian.png" width="200">  | <img src="/src/music/scales/patterns/Marva.png" width="200"> ||  <img src="/src/music/scales/patterns/WholeTone.png" width="200"> |
**25**   Blues  (6)| **26**  Minor Penatotonic  (6)| **27** Hungarian Minor | **28** Ukraninian Dorian| **29**  Marva|**30**  Todi |**31** Whole Tone  (6) |**32**  Chromatic (12 keys)




### Notes
- Play  

### Gate
  ile nut trwa dzwiek  

### Velocity
(how hard is press) nie wszystkie mają głośność   Fixed Velocity is enabled by pressing Velocity 6 while holding down Shift 19 . Fixed Velocity
is confrmed by the Velocity button illuminating white while Shift is held down


### Pattern settings / Probability

 multiplier/divider of the BPM
 1/16 is the default sync rate, where each step corresponds to a 16th note.

|1/4| |halfstep||1:1||2x||
|---|---|---|---|---|---|---|---|
1/4| 1/4 T |1/8| 1/8 T |1/16 |1/16 T| 1/32| 1/32 T

-  length - Dlugosc sekwncji  (ilość nut)  


-  nudge -  Cały pattern do przodu albo do tylu  Remember that when using Nudge with Patterns of less than 16 steps, the effect of Nudge is
restricted to the Pattern length. Steps outside the Pattern length will be unchanged.

### Pattern

##### Lock View


###  Mixer
- Mute  

##### Scenes
, press and hold Shift: the Scene pads change colour to dim gold. Press a Scene
pad (while still holding Shift) – it will light bright gold while pressed, indicating that Patterns are now
assigned to it.


###  FX
-  delay -{up}, reverbs - {bottom}   (global)  

 side chain
-  on sustain things . will react to drum 1
right white knefels to more effect cutoff taki  


|PRESET| DELAY TYPE|
|---|---|
1|Small Chamber
2 |Small Room 1
3 |Small Room 2
4 |Large Room
5 |Hall
6 |Large Hall
7 |Hall – long reflection
8 |Large Hall – long reflection

.

|PRESET| DELAY TYPE| MUSICAL DESCRIPTION|
|---|---|---|
1 | Slapback Fast | Very rapid repeats
2 | Slapback Slow | Rapid repeats
3 | 32nd Triplets | 48 cycles per bar
4 | 32nd | 32 cycles per bar
5 | 16th Triplets | 24 cycles per bar
6 | 16th | 16 cycles per bar
7 | 16th Ping Pong|  16 cycles per bar
8 | 16th Ping Pong Swung | 16 cycles per bar with swing
9 | 8th Triplets | 12 cycles per bar
10|  8th dotted Ping Pong | 8 cycles per 3 beats with Stereo Spread
11 | 8th | 8 cycles per bar
12 | 8th Ping Pong | 8 cycles per bar
13 | 8th Ping Pong Swung | 8 cycles per bar with swing
14 | 4th Triplets|  6 cycles per bar
15 | 4th dotted Ping Pong Swung | 4 cycles per 3 bars with swing
16 | 4th Triplets Ping Pong Wide | 6 cycles per bar


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






TRIX:
- Modulate index with LFO !!
 - LFO 1+ > OSC1 Pulse Width
- ?
    - LFO 1+ > Frequency ()
    - Env2mod - how filter env  
-  Tremelo  (lfo  modulating volu o amplifire)
    - LFO 1+ > mix: Osc 1 Lvevl
    - LFO 1+ > mix: Osc 2 Lvevl
    - LFO 1+ > noise level


```



- you can use wavetables


---------------

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
