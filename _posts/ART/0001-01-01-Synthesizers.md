---
title: Synthesizers
description: Novation Circuit guide
categories:
 - ART
tags:
- Audio
- Music
---


# Synths



### Scales:
musical notation since the middle ages. So, the list goes: Ionian, Dorian, Phrygian, Lydian, Mixolydian, Aeolian and Locrian

pitch from left to right

|32 | Chromatic | C |C# |D |Eb| E |F |F# |G |Ab| A |Bb |B  
|-|-|-|-|-|-|-|-|-|-|-|-|-|-|
17 | Naturl Minor | C|| D|Eb|| F| |  G |Ab| | Bb
18 | Major | C ||D ||**E** | F| |  G| | A ||B
19 | Dorian | C ||D |Eb||  F||   G || A| Bb    
20 | Phrygian | C | C#||Eb||  F ||  G |Ab| | Bb    
21 | Mixolyduan  | C ||D ||E | F ||  G || A| Bb    
22 | Melodic Minor | C|| D |Eb|| F | | G || A|| B
23 | Harmonic Minor | C ||D |Eb||  F| |  G |Ab| || B   
24 | Bebop Dorian | C|| |Eb| E|  F||   G | |A| Bb  
25 | Blues | C |||Eb||  F | F# |G | || Bb   
26 | Minor Penatotonic| C |||Eb||  F|F# |  G || | Bb    
27 | Hungarian Minor | C ||D|Eb||  | F# | G |Ab| || B
28 | Ukraninian Dorian | C|| D| Eb|| | F# | G || A| Bb   
29 | Marva| C |C# || |E | | F# | G| | A ||B  
30 | Todi | C| C# || Eb||  | F# | G |Ab| || B  
31 | Whole Tone  | C ||D|| E|| F#|| Ab|| Bb   

**Root Note** - niebieski u góry  - `Tonic note` - is the first scale degree. It is the tonal center and is the most stable note. Most often music ends on tonic because it's a good resting point and gives a sense of finality. This is possibly the easiest note in a scale to remember because it is one of two notes most often called by it's scale name.


### Waveforms:
Create sound in oscilator

|-|-|-|-|
|-|-|-|-|
Sin | Simple | Muted Warm Hollow Bassy |Flute Organ
Triangle| Simple few overtones  (not as full as square) | Pure, Dull | Chime, Organ
Saw wave | Complex excitements and bright at hi end in upper range. |  Full Harsh Bright | string
Square | Complex harmonics, full sound  Can be shape no other can| Hollow Harsh Brass ruddy | Horn
Square Pulse | Square with wariation in timing
Noise | very Complex many overtones. Hard Cutting  |Asymmetric | Noise

Smooth shape, smooth tone , hard; hard tone


### Filter
Shape sound and character of waveform

 if you low pass filter saw wave you will get sth like sin  

 |-|-|-|-|
 |-|-|-|-|
Lowpass |  Cut off High end freq (higher are filtered)  | (traditional ?) duller
Highpass | Cut off Low end freq  | (more esoteric ? )
Bandpass | Low + High  
Resonance | Peak before high cut. Add sharpness. | Laser zaps, Focused sounds  
Sweep | Move resonance center   
Key track | Low same but higher notes have higher filter (more open) frequencies / high-end on high notes  
Envelope | ie: Open and Close filter over time  
Cutoff frequency | Take out of focus  
Drive |   
Env2 Mode  |  how much filter env modulate filter ftreq  




### Envelope
How fast tur on and down. how much envelop impacts settings u can modulate: filters, pitch or frequencies

|-|-|-|
|-|-|-|
Attack | In (immediate in: drum / or long in) | How loud over time  
Decay | Out (loudness over time) After attack  | How loud over time
Sustain | Rest state after decay 0 - immediately stop even key down | Rest state
Release | how long will stay after trigger release  | Start Immediately after release



Examples :   
- filter envelope -   
- amplifier envelope -   
- frequency envelope -    
- pitch envelope -   
- pulse with modulation - shape square wave



### Modulation
using signal to shape aspect of sound over time
> Modulate Wave with additional waves

#### LFO (modulator)
> Low frequency oscillator generate waveform (e.g. sin) like oscillator and using it as control signal modulator

Examples :    
- source >> destination e.g. LFO can modulate filter freq  
- can create pitch vibrato
- pulse width modulation with  Square wave

```
`Rate`  
`Sync`  
`Slwe`  
```
---



# Samples

https://trisamples.com/  
https://cymatics.fm/pages/free-download-vault  
https://www.noiiz.com/  
https://www.looperman.com/  
https://r-loops.com/  

------------

# Novation Circuit

### Macros
> Combine up to 4 settings  in top knobs 1-8


1. seto knob to 0
2. set mini settings
3. change knob to max
4. change depth to where max should be (positive depth)


Czyjes ustawienia:
- filter cutoff - bring in out
- Env2mod - how filter env  / lead arpeggio to softer sound
- Amplif and filter env attack
- Amplif and filter env release
- (lfo speed, modulation depth , distortion level, oscillator pitch...  )

Assignment of the potentiometers (fix for almost every patch)
1. Cutoff EG intensity  
2. Cutoff  
3. An intelligent transition of Resonance / Noise / Overdrive (depending on the patch, sometimes without Noise or Overdrive)  
4. first 50 % is for Attack Time / second half of the knob sets Release time, so you can smoothly morph a lead sound into a pad.  

The remaining four knobs are used for parameters most relevant for the selected patch  
5. Vibrato, EFX Dry / wet (depending on the patch also chorus when turning the knob further to the right)  
6. Performance Knob (could be LFO speed, LFO intensity, OSC Tune etc.)  
7. Volume & Amount of Noise  
8. Oscillator Morph functions. Those can be Wavetable Positions, Oscillator A/B Ratio etc.  



### Oscillator
 Default 1 oscillator .
 you can detune adding second oscillator and mix them on `mixer`

1. Oscillator 1
2. Oscillator 2


 `index`   
 `Interpolate`  

 `Cents`  
 `Semitones` - up or down on octave (have multiple octave playing one note)    
 `VSync`  
 `Density`  
 `Detune`   


Czyjes ustawienia:
 - you can use wavetables
    - trick (modulate index with LFO)


### Filter

`Lowpass`  
`Highpass`  
`Bandpass`  
`12dB`  - cutoff slope. Greater value sooner cut off  (higher freq pass through)
`24dB`   

`Key Track` - change freq depend on how high note is
`Env2 > Freq`   

`frequency` - how much to cut off filter   
`resonance`    
`Q norm`  

`Drive` - amplify going in to filter. dif types  (bit crush, rat reduce)
Q1 / Q2 -  where to apply  

### Envelopes

1. `Amplifier`  
2. `Filter`  
3. `Extra one`  (you can  conreol by macro ) normally attack   

Velocity - how much have

Czyjes ustawienia:
- if you control in macre set to low cutoff (nie obcinaj nic)

Delay   

### LFO

1. LFO 1
2. LFO 2

`Slew` (as portamento or glide for LFO wave ) limits how quickly wave can cahcnge value  
`Phase` - tels LFO where in the wave to start

`Rate` (can sync to temp )
`Delay` (can sync to temp )with fade modes  


`Comon Sync` - all notes use sam lfo in same time     
`Sync Style free` - not synced
`Sync Style Key Sync` - start with new key push
check
- alternative
- melodic

- piano LFO 1 > destination: freq
-
- Source LFO +/- . Jak zmieniamy depth to 30 i -30 brzmi tak samo
- Source LFO + .
  - depth 20 .> 1/3
  - depth 25 > 1/5
  - depth 30 > interval of octve  (destinantion 1/2pitch)
- source: velo > destination LFO rate. give random
- LFO change another LFO: LFO 2 +/- , destination: LFO 1 rate destination2: Osc 1 Pulse Width   
### FX
### Settings

### Modulation Matrix



### Circuit

`notes`  - Play  
`velocity` -   (how hard is press) nie wszystkie mają głośność
`gate` -  ile nut trwa dzwiek  
`nudge` -  Cały pattern do przodu albo do tylu  
`length` - Dlugosc sekwncji  (ilość nut)
`patterns`  
`mixer`  - Mute  
`fx` -  delay -{up}, reverbs - {bottom}   (global)  
`side chain` -  on sustain things . will react to drum 1
right white knefels to more effect cutoff taki  


# PC
.sys /.sysex  -  drum samples / patch  
.circuitpack  - whole pack  
midi device on windows:  

### PATCHES


#### Macros:
OSC:  
`Wave Interpolate`  
`Pulse Width Index`  
`Vsync Depth`  
`Density Detone`  
`Semitone Tune`    
`Cents Tune`  
FX:  
`Distortion`  
`Chorus`  
`Portamento`  
Modulation Matrix:  


------



Shift + octave up  - transpose whole octave pattern up  
https://ledgernote.com/blog/interesting/musical-key-characteristics-emotions/

http://www.gradfree.com/kevin/some_theory_on_musical_keys.htm
