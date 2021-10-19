---
title: Animation

categories:
 - ART
tags:
- Art
- Animation
- VFX
description:  Principles, VFX
permalink: /animation/
---


[Unreal Animation](/uanim/)
[Houdini KineFX](/kinefx/)   



# Frame rate
typically 24-60 FPS

# Principles of animation

| Name | | Less| More|
| --- | --- |--- | ----|
Squash & Stretch | (for VFX), emphasize speed, momentum, weight  and mass | solid stiff | soft, characters, face | try to preserve volume
Anticipation |  (for VFX) prepare for action clue what hapen next and focus action. can be multiple layers ||face |if you have time for build up do it
Staging |make idea clear: wher to look what i happenieng |
Strait Ahead vs. pose to pose |character pose to pose but hairs frame to fram  |frame by frame for unpredictable like simulations | better in most actions
Follow through, overlaping action, drag| continoue after main body stop, ofset created by drag, drag=delay main body and tips and end wchch must follow > forearm drag elbow > drag hand | TV antena | feather  
Easing |  Slow In & Out (for VFX) ! Most efect have slow in and out | robots | all rest
Arcs | living reatures move with arcs |
Secondary Actions |  (for VFX) Add more dimention lik other hand (not in focus but iomportant ) additional things that Exaturate primal effect
Timing |sometime draw on 2 afarmes (less gitter slower action) |hit| look around  
Exaturation | ||more power
Solid drawing | volume weight drawing on solid spheres. Avoid twinning (mirror)
Appeal | chrismatic aspects > dynamic design. (varietyu of shapes on dif characters), play with proportions.


#### Dynamic of body
Inna dystrybucja ciezaru cia la przy biegnieciu i zakretach - kladziemy sie

# Animation types

## Skeletal anim

retarget  
ik  
root motion - wyciagnac z animacji. ale ciezkie do zreplikowania online. (wykorzystywane czesciowo) / animacje w miejscu nawigacja też musi byc inna jak jest root motion.  
motion matching  


layering  
ik rig - zeby wydobyc info   

## Manual
`Keyframe` from poses
- by expression or keys
- chop



## Data driven
### Mocap

## Procedural

`reactive` "reactive animation" is one involving discrete changes, due to events

## Dynamic
### Simulation   
   - Normalize - Fit parameters to 0- 1  #
   - Muscles & tissue
### Physics
#### Ragdoll




# VFX

https://youtu.be/WLMVpcK0WvA?list=PLQD_sA-R5qVKVYw3EVuRT7fSJsVukLEhD

**Game design driven**  
- shape & arena of effect. How far

**Visual**    
- level of importance
- shapes: simple but break symetries
- value ranges. Table for Brightest UI > tyhen character and fx > enviro.
- value keep in middlet to be able use dark or light contrast
- in one fx try use similar colors (chyba ze w hierarhi)

**Timing**  
  - All fx should have anticipation, main event and dissipation
  - Outro should be considered as separated fx (with lower values, saturation and opacity)
  - Fading energy can be represented by changing: value, hue , saturation, opacity, size
  - Color variation value, opacity are elements that can be altered in relation to an fx timing
  - color harmonizing
  - tempo (beats)
  - intensity over time.
  - Reaction time 0.2 for see 0.1 for hear and less for touch (go / no go time decision)


| intensity over time | |||
| --- | --- |--- | ----|
|constant | missile
|acceleration
|rapidly decelerating | explosion
|peak |
|repeated | light blink
|wave |  


[book: Illusion of Life: Disney Animation]




----------------------------



pose / motion matching z https://www.youtube.com/watch?v=KSTn3ePDt50&t=1649s


https://www.youtube.com/watch?v=KSTn3ePDt50&t=1649s

https://www.youtube.com/watch?v=KLjTU0yKS00

https://www.youtube.com/watch?v=o-QLSjSSyVk


https://advances.realtimerendering.com/destiny/siggraph2014/animation/index.html

 https://www.youtube.com/watch?v=KLjTU0yKS00 https://www.youtube.com/watch?v=SQo9pTQ14Jk Motion matching: https://www.youtube.com/watch?v=KSTn3ePDt50 Fullbody animation in Doom: https://www.youtube.com/watch?v=3lO1q8mQrrg Animation tricks for the trade: https://www.youtube.com/watch?v=zEYITZUHpo4
https://advances.realtimerendering.com/destiny/siggraph2014/animation/index.html
