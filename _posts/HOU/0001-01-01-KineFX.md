---
title: KineFX

categories:
 - HOU
tags:
- Houdini
- Animation
- SOP
description: Rigs, Animation, Retarget.
permalink: /kinefx/
---




All working on world level on points. Point is joint when has transform attribute and name attribute.  
- `@name` unique per point   
- `@P`  (3flt)    - handle world space translation
- `@transform` (9flt - matrix) - (matrix3) rotation, scale, ...? .

The parent-child relationship between joints in a hierarchy is determined by vertex order. However, point ordering is not considered when traversing the hierarchy.



[SOP.hiplc](/src/hip/SOP.hiplc)  

<img src="/src/kine/d1.png" width="350">    

---

# Create (rig)   
-  Rig is separated (like shadow rig) separated hgierarchy to control rig > clean for export   
- Any SOP polygonal line into a joint chain with the  Skeleton SOP node or the  Rig Doctor SOP node node.

<img src="/src/kine/c1.png" width="350">     


**[ Skeleton ] SOP**
 - create @localtransform.  
Can contorll bone placement, a lot of shortcuts.   
Modify and Create modes.  


**[ Rig doctor ] SOP**
 - create missing @name  

**[ Orient along curve ] SOP**
- create transform (3x3 transform), and tangent metod to next edge  

**[ Re-Orient Joints ] SOP**


[sidefx.com/docs/houdini/character/kinefx/skeletons.html](https://www.sidefx.com/docs/houdini/character/kinefx/skeletons.html#creatingskels)


---

# Controls

### IK
create controllers by deleting parts of skeleton

- fullbodyIK
- IkChain:
   - select  root mid and tip bones points
   - set! match by name

<img src="/src/kine/ik1.png" width="150">   

### Curve
<img src="/src/kine/curve.png" width="150">    


---

# Capture (skin)
<img src="/src/kine/skin.png" width="350">   



- `BoneCaptureLine` - define capture regions @joints    
- `Tetembed`, create mesh weightings  
- `BoneCaptureBiharmonic`, transfers weights to skin   

change pose and `Capturelayerpaint` to paint  after biharmonic (po region name wiec troche odporne )

---

# Motion / Animation


Convert to **Motion Clip** - **[ Motion Clip ] SOP** -  see all frames at once  (not time dependent)   Enable to operat on neighbour frames  
Convert to **Animation** - **[ Motion Clip Evaluate ] SOP** -  time dependent Geometry caches One frame per frame.

## Animation

#### Root motion
- **[ Extract Locomotion ] SOP** -  extract root motion   


#### Mix Anims
- **[ Skeleton Blend ] SOP** - feed with 2 animations
- **[ Time Shift ] SOP**

## Motion Clips

- **[ Configure Clip Info ] SOP**  

- **[ Motion Clip Cycle ] SOP**  
- **[ Motion Clip Extract] SOP**  - Extract Frames


---
# Retarget
Rig Match Pose  
Map Points   

---

# Rig Wrangle

`rotate(3@localtransform, @Time, {1,0,0});`


# Rig VOP

twoboneik
lookatconstraint
parentconstraint

---

# Repair
`realistic shoulder` -        
`reverse foot` -   
`stabilize joints` -   select joints to stabilize,

---


# To Unreal

90+- ?  how to position anim and where is save to rotate ?????

control rig - manipulating bones transforms   
animation graf - blending , playback  

https://vimeo.com/rokandic


---

https://www.tokeru.com/cgwiki/index.php?title=HoudiniKinefx
