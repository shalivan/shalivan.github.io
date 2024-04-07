---
title: Animation
categories:
  - ART
tags:
  - Art
  - Animation
  - VFX
  - 3D
  - CG
description: Principles, VFX
permalink: /animation/
---
[[21-01-01-Art|art]]


[Unreal Animation](/uanimation/), [Houdini KineFX](/kinefx/)     


https://youtu.be/6TB62YKHwRQ
# Frame rate
typically 24-60 FPS

# Principles of animation

| Name | | Less| More|
| --- | --- |--- | ----|
**Squash & Stretch** | (for VFX), emphasize speed, momentum, weight  and mass | solid stiff | soft, characters, face | try to preserve volume
**Anticipation** |  (for VFX) prepare for action clue what hapen next and focus action. can be multiple layers ||face |if you have time for build up do it
**Staging** |make idea clear: wher to look what i happenieng |
**Strait Ahead vs. Pose to Pose** |character pose to pose but hairs frame to fram  |frame by frame for unpredictable like simulations | better in most actions
**Follow through, overlaping action, drag** | continoue after main body stop, ofset created by drag, drag=delay main body and tips and end wchch must follow > forearm drag elbow > drag hand | TV antena | feather  
**Easing** |  Slow In & Out (for VFX) ! Most efect have slow in and out | robots | all rest
**Arcs** | living reatures move with arcs |
**Secondary Actions** |  (for VFX) Add more dimention lik other hand (not in focus but iomportant ) additional things that Exaturate primal effect
**Timing** |sometime draw on 2 afarmes (less gitter slower action) |hit| look around  
**Exaturation** | ||more power
**Solid drawing** | volume weight drawing on solid spheres. Avoid twinning (mirror)
**Appeal** | chrismatic aspects > dynamic design. (varietyu of shapes on dif characters), play with proportions.


# Posing by James Chaing
Maximum expression & Maximum appeal
-Each pose/key relates to feelings and intentions of the character.
-Key is to achieve;
1. Strong Contrast.
2. Absolute Clarity.
ASSYMMETRY
-Avoiding Symmetry
-Solving twinning issues though posing and timing
-Looking for parallel shapes/contours
Eg. Kent Duncan (Jane)
Eg. John Lounsbary

SQUASH & STRETCH
-Keys to giving weight
-Rigid vs. Soft
-Use also for expression on face (not just in motion)
-Aids in anticipation
Eg . Ollie Johnston (Rufus and Brom Bones)

STRAIGHTS vs CURVES
- Design Concept to maximize appeal
- Have mix of straight and curves
- Gives dimension to surface (flesh against wall
-

LINE OF ACTION
- Gives strength + direction to the pose
- Sets up next move/key
- Forces you to use reversals
- About rhythm
- Extends through entire pose

POSITIVE &NEGATIVE SPACE
- Composition and focusing audience attention
- Using focused details against broad open areas
- Busy vs Clean
- Prevalent in Asian art and Rembrandt

POSITIVE &NEGATIVE SPACE
- Composition and focusing audience attention
- Using focused details against broad open areas
- Busy vs Clean
- Prevalent in Asian art and Rembrandt
Eg. Marc Davis (Maleficent)


TWIST+ TILTS + TURNS = TORQUE
- Forces shape changes within a pose
- Create tension
- Rubber band effect ties body together
- Glen Keane, Chuck Jones, Michelangelo

SHAPES
- Clean silhouettes
- Overlap of shapes to create interest and dimension
- Avoiding boxes

EXAGERRA TION
- Making it read
- Remember 1124 sec
- Sometimes just for feel
- Cartoons are not real. The are fun

CHANGE OF EXPRESSION
- Maximizing contrast between poses
- Helps clarify what is being said
- Creates interest
- Concept of reversals


30+20 SPACE
- Using your layout fully
- Move up down and across frame
- Move towards and away from camera
- Easy to forget 30 space in 30
- Visual overlap

UNITY
- Putting all together
- No contradicting messages in the pose
- Define the moment
-Ask:
Is there sense of movement? Feeling & emotion? Balance & solidity?

Expression in face and hands. v
ia tilts, torgue and squash and stretch




# Animation types

- `static animation` - always something is moving over the screen    world is not dead  
- `dynamic animation` - pet, ...


## Skeletal anim

- COG
body is organic aprts ar interrelated
- spine curvature controll
- foot roll (przod tył - podniesienie + rotacja po ziemi ) + palce
- twisty


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

problems:
- gimbal lock
- 90 ,180 flips
favour z (3d max) so:
- legs / spine draw from site (and left righ secondary motions less of them )
- from top

# Character Skeletons

Dont model and rig character in relaxed pose. (will complicate process)

Workflow:
create spine:
- from side view create 1 bone in center of gravity (COG)> to bottom of neck, (spine_end)
- select joint RMB > split  
 - child compensate on bar > fix pos
- select all RMB > orient selected joints
- select first (COG) > P > zero rotate value
- name
create leg
- from side view
- new chain MMB
- from hip  to foot
- from front view fix start and rotete
create head:
- enter to create mode
- from side view (no child compensate), connected to end spine
create hands:
create clavicle:
- as a point.
parent joints to connect:
mirror:




# Dynamic of body

- tetrapod locomotion = `quadropedal` ( 4 limbs on ground ) with `pronagrade` posture
- huans  bipeds  locomotion `bipedal` > posture Orthograde

## Biped


upright posture
- rotating in hip when (schylamy) sie. - to nasza apdptacja do bipeda
- heat to toe in animals, - human front to back compression of chest (jellybean shape) to minimize enedgetic  


- locked knee is key to human walking mechanism
- Urbavores huge backbone stiff 2 phases
- carnivore use backbone an can run faster.  (meet is easy to digest and you are lighter) tiger bandy backbone (floating face gathered or extended )
- human is  in between. (have a but - )
- kid locomotion is more toddlers (before they learn )
- faster walk imply more hip roattion

##### Walk cycle
walk is very efficient.
- poses walk. contact and passing
- `foot roll` over the ground - (in contact)
- Contact pose. Moment head is lower.

#### Run
floating phase in tunnning is what differentiates a run (phase where all feet are off the ground at least 1/2 of time)

##### Posing
- `Center of mass` - The center of mass shifts at the turns.  Different 'weight distribution' while run   
- `Contrapposto` - braking symmetry of archaic Greek figure (asymmetrical balance)  - weight in one leg is more complicated. torso shoulders and head response (s curve in spine) opposite leg-hand are straight. - it is representation of the human body in which the forms are organized on a varying or curving axis to provide an asymmetrical balance to the figure. Organic more loose quality to body
- `Lordosis Reflex` + lumbar curvature. (spine)
- hips are rotated down ! Pelvic orientation (wysuniete biodra do przodu )


## Quadruped


- how whide apart feats are




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

procedural with math  https://youtu.be/KPoeNZZ6H4s 

pose / motion matching z https://www.youtube.com/watch?v=KSTn3ePDt50&t=1649s


https://www.youtube.com/watch?v=KSTn3ePDt50&t=1649s

https://www.youtube.com/watch?v=KLjTU0yKS00

https://www.youtube.com/watch?v=o-QLSjSSyVk


https://advances.realtimerendering.com/destiny/siggraph2014/animation/index.html

 https://www.youtube.com/watch?v=KLjTU0yKS00 https://www.youtube.com/watch?v=SQo9pTQ14Jk Motion matching: https://www.youtube.com/watch?v=KSTn3ePDt50 Fullbody animation in Doom: https://www.youtube.com/watch?v=3lO1q8mQrrg Animation tricks for the trade: https://www.youtube.com/watch?v=zEYITZUHpo4
https://advances.realtimerendering.com/destiny/siggraph2014/animation/index.html
