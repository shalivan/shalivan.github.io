---
title: Unreal Animation
description: RAW
categories:
 - PXL
tags:
- Real Time
- Unreal
- Game Dev
- Tech Art
- Animation
permalink: /uanimation/
---

import: with skeleton - update skeleton reference pose - !!!!!!!!! important    
[Houdini KineFX](/kfx/)      
[Principles of animation](/animation/)     



## Persona:
- **Skeleton** `Skeleton Asset`  
  - `Sockets` - grab component to parent to mesh > choose parent socet in details.  
- **Mesh** - `Skeletal Mesh`     
- **Animations**
  - `Animations` - Files with anim data
  - `Composite` -  Stitching multiple animation clips into one  
  - `Animation Montage` - More complicated animation logic, (combo system with branching)
  - `Blend Space` - Blend on parameter change
  - `Notifies` -
- **Animation Blueprint** - `Animation BP` with 'Final Animation Pose' as output    
  - **Anim Graph** > State Machine for anim / anim blaend state blendings.
   - Locomotion
     - **State** (with anim) to add: drag anims states to graph
     - **Condition** transision - bool from gameplay blend
 - **Event Graph** - write code do get set params/variables.  
- `Physic Asset` - Ragdolls


## Unreal Assets

Other Assets:    

- Animation Layer Interface
- Anim Offset
- Animation Sharing Setup
- Bone Compression settings
- Control Rig - Control Rig shape library
- Mirror data table
- Pose Asset

Bones actions:

- `Copy pose from mesh` - [v]-use aatach parent -  direct attachment. State machine
- attach to bone or socket
- `IK bones` - for guns or use sockets  
- `Virtual bones` - virtual bone relation before apply anything  

-----------

# Skeleton

## Retarget

### Same skeleton
No retarget needed. Only bone translation data in bone translation component  - retarget animation change only bone names information's on runtime




###### Change influences source

Rotation always come from animation data. - Animation  drive rotation but not location and stretch  
Skeleton list (in persona)) > Advanced   
- `Animation` - bone translation come from anim (unchanged) (Root, IK's, And any markers)
- `Skeleton` - trom target skeleton bind pose (all)
- `Animation Scaled` - from animation but scaled with skeleton proportions (pelvis)
- Animation Relative -  All IK, foot, root. (Take rot from anim keep scale from skeleton)  
- Orient and Scale



### Different skeleton

Retarget >
go to skeleton asset and in retarget manager > manage retarget base pose



-----------
# Anim

TURN / INPLACE ANIMATIONS
BP:
- rotate 360 (face 0 in middle of animation), thenn counterfit rotation linear to face always front
  - `RMB` > `convert to single frame anim ` and feed angle
  - additive animation : `Apply Additive`

## Root Motion
motion driven by animation instead of animation controller. root bone is animated and collision capsule move and rotate.
Usefull because:

in place animation cant have root motion.

animation details panel:
- enable root motion: it will look like in place, (in wievport process rootmotion to visualize !!!!)
- root lock: - Anim first frame !

in anim BP:
- in class defaults: Root motion mode: root motion from everything (will extract from all anims that have it enable)

## IK

#### Full Body IK  



#### Motion Warping
- adjust motion to contact with world


#### Controll Rig

https://www.youtube.com/watch?v=y2WzNvJZk0E

## Anim Dynamics (Secondary Motion)
in component space.  but can wind interactions 
Setup in BP Graph. Dynamic on a bone behaviour  

- single bone dynamic - cheaper  
- chain dynamic

[VFX unreal - anim dynamics ](https://youtu.be/5h5CvZEBBWo)
-----------------

[VFX unreal](http://teres4enko.blogspot.com/)    
ptak flaping to the music: https://youtu.be/TBiepo5ZQhY
