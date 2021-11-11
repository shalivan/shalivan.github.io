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
[Houdini KineFX](/kinefx/)     
[Principles of animation](/animation/)  




# Unreal Assets

Base:
- `Skeletal Mesh` - Mesh     
- `Skeleton` Asset > Edit in persona skeleton tab.
- `Physic Asset` - Ragdolls

Composition:
- `Animation Composite` -  is just stitching multiple animation clips into one.  
- `Animation Montage` - is for more complicated animation logic, say a combo system with branching sections.   
- `Blend Space` - mix poses
- `Animation Blueprint` - BP with 'Final Animation Pose' as output    
  - **Anim Graph** > State Machine for anim / anim blaend state blendings.
   - **state** (with anim) to add: drag anims states to graph
   - **transision condition** - bool from gameplay blend
 - **Event Graph** - write code do get set params/variables.


Other:

- Animation Layer Interface
- Anim Offset
- Animation Sharing Setup
- Bone Compression settings
- Control Rig - Control Rig shape library
- Mirror data table
- Pose Asset


-----------


Contains:
- `Sockets` -
- `Copy pose from mesh` - [v]-use aatach parent -  direct attachment. State machine
- attach to bone or socket
- `IK bones` - for guns or use sockets  
- `Virtual bones` - virtual bone relation before apply anything  


https://youtu.be/Oe7fYS9qxmk
notifies, curve names, slot names  

character parts, character if



### Blend space ?
- to mix anim with variable
- can blend between static poses


-----------


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



# Full Body IK  



-----------


# Animation Blueprint


-----------

# Animation Montage


-----------

## Motion Warping
- adjust motion to contact with world



-----------

# Animation Composite



ptak flaping to the music: https://youtu.be/TBiepo5ZQhY



-----------


# Controll Rig

https://www.youtube.com/watch?v=y2WzNvJZk0E

-----------------

[VFX unreal](http://teres4enko.blogspot.com/)
