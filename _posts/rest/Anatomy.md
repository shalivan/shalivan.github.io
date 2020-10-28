---
title: Anatomy
description: My practices.

tags:
- Data
---


![](/src/art/anatomy.jpg)  



# Old


https://vimeo.com/286184782 SIGGRAPH 2018  
https://youtu.be/vinCWv20Ib4?list=RDCMUCegWLyW4CYzph4dYW-gYy0g rigging2 SESI  

Edit > Object > Bone kinematic override - None / IK rest / Capture Pose



   - `namespaces`  


## Rig From Bones
### Bone
- have intrinsic orient: x dimension is flat to rotate like a knife (primary rotations)
- rotate evaluation default: (object: Rx,Ry,Rz, Bone: Rz,Ry,Rx - correctly with IK solvers)  
- dont rotate on bone - use purple square  
- `blend` - CHOP based
- `mirror`  

### Bone tools
- create from orthographic view. to correct angles
- change chain position: move root null
- manipulate bone by small cube (Y- to change coordinates)
- split bone - `Ctrl`+ `LMB` on bone
- bone lengths - to scale (don't scale in other)

### Building setup
- `end null` - (to attach systems together) - to create bone null parent to last one and move downward on local axis to the end.
- traditional connect 2 systems: draw `sysA` `sysB` and parent `end null` with nullA
- constraint shelf: parent blend select `nullA` of `sysB` and then `end Null` of `sysA`  // (CHOPS) (set to Simple, just rots and scales, Keep Position - After)?

### FK
Null controller:  
1. at `nullB` at origin parent to `boneB` output   
2. [v] keep position when parenting   
3. cut connection  
4. patrent 1up in hierarchy to `boneA`  
5. clean transforms (to create pre-transform)   
6. copy relative ref rotate from `nullB` and pase ref to `boneB`  
7. you can now rotate `nullA` to control system  

### IK
1. create hierarchy  
2. `target null` (first and last bone)   

(have a little angle between bones to work with IK)


---

## Capture



### Bone
For each bone there is region with 2 sets of params. Capt and def regions. Deform by comparing 2 set of params capture define what to deform.

Cregion parameters are promoted to bone level:
##### capture region
Bonbe capture pose - params that can set position and params and are override on capture tool operation (if destroy existing weights on `bone capture` is on (if append in option up to viewport it will respect )
###### deform region  
-  

### Capture  Geometry
Take hierarchy or series of regions (form inside of bones obj) and create attrib `pCaptFrame` i `pCaptSkelRoot`. You can add another bone by activating tool again  (if you modify capture pos earlier capture will override it)

(Use capture pose not frame)




Select Geometry [enter] > Select bone or root


- Select: Bone or Root (null or 1 bone from net)  
- Method: Override (will destroy prev) or Append (if second)  
- Type: Region, Proximity or Biharmonics

| Type | SOP ||
| - | -| -|
Regions | `Region` | Fast  
Proximity | `Bone Capture proximity` |  Better. Will fill weight through the model but with big blend have problems (drop off param in weighting tab)
Biharmonic | `Bone Capture Biharmonic`| Best. It get regions , build lines then tetrahedralizable and spread weights using tets and sometimes additional transfer if not connected
Wire Capture | `Wire Capture` | |

Biharmonic:  
- use bone link `Bone capture lines`
- Try options with `Solid embed` (terte) for one sided planes
- U can delete some parts before tet to get more rigid  

### Capture Wire

##### Capture Wire
1) Geo to capture      
2) Curve   

init from primitives

##### Capture deform
1) Capture wire
2) Rest Curve
3) Animated Curve




#### Bone Deform
~detail: `pCaptSkellRoot` on deform SOP - root for bones
regions from obj and create attribs + lock move geometry because will be deform not moved from now  
and create deform~  

## Edit Capture
Tool available  from shelf or tab menu in viewport


#### Edit Capture Region
Use if captured by region ?

- select bones to edit to transform region
- try with shift  to modify whole  

#### Edit Capture Weights
In viweewport or spredsheet -  control by diamonds or right click and global  mode.

`Capture override` SOP

#### Paint Capture Layer
(layers as such are not useful at all)   

- we can display deform and paint and see deformation
- [ctrl]+[MMB] - to change capture region to edit
- visualize only selected region  



##### Twist
How to fix twists ?

## Retarget

### BVH
https://www.sidefx.com/forum/topic/55681/
- Using the shelf tools to manually connect the mesh rig to the mocap rig and it does work. (BVH file from Mocapdata.com to a generated MakeHuman - FBX export) (select the FBX bones and target the autorig bones. you might need to place the autorig into all FK mode. @Atom



   http://www.bvhacker.com/  
   https://forums.odforce.net/topic/7026-retargeting-mocap/  
   https://vimeo.com/325094421  
   https://www.sidefx.com/forum/topic/38797/
   https://forums.odforce.net/topic/26599-mocap-retargeting-between-unlike-rigs/

   https://forums.odforce.net/topic/40466-motion-retargeting-tool/
