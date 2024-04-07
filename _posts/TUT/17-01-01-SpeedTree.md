---
title: Modeling - Vegetation
categories:
  - ART
tags:
  - Art
  - 3D
  - CG
  - Software
description: Vegetation, foliage
permalink: /foliage/
aliases:
  - foliage
---


> Pxlink:
>Obsidian:  [[17-01-01-Modeling]], [[21-01-01-Art]] [[17-01-01-Modeling_Foliage]] [[02-01-01-LSystem]]  [[18-01-01-Color]]  [[14-01-01-Procedural]] [[08-01-01-Material]] 


# Speed tree

#### Shortcut 
`F` / `Ctrl` + `F` - hide 
`H` - hide

You can construct tree procedurally to make an advantage of generators randomization 

edit modes: 
- Generator  - edit all instances
- Node - edit single branch  “Clear Node Edits” option in the menu when you right-click a generator in the 

parameters:
- **[+-]** - Variance. help with seed randomization    
- **[green curve]** -  Parent curve. Along length of parent from bottom to end. 
- **[blue curve]** - Profile curve. How it behave along spline. From 0 to param value.       
- **% of parent** - Use % of parent to be procedural (can growth)   <<<< ?!!!!!!!

Shared parameters ??? 


# Properties

|  | Global | Branch | Leaves |
| ---- | ---- | ---- | ---- |
| Gen | Number of points ,  Spawn points placement spline | Global scale, Z-depth, Prune |  |
| Spine |  |  Length, Orientation , Start Angle, Noise  |  |
| Skin | Welding   | Radious, Roll, Split  | Size |
| Optimize |  |  |  |
| Orientation |  | - | Orient, Deform |
| Segments |  |  |  |

---

## Gen
Spawn points parameters

####  Placement Mode
| mode | Count | Placement | Placement | ORIENT | Usage |
| ---- | ---- | ---- | ---- | ---- | ---- |
| Absolut | 1 | Number | Random | Random | Stomps and trunk |
| Absolut step | *  | Number | Even |  |  |
| Proportional | 1 | Number | Random | Flat | Adapts to the size of the parent. Suitable for randomization and cases where parents are of varying sizes. |
| Proportional Step | *  | Number | Even | Flat |  |
| **Interval** | *  | Distance | Even | Star | Constant frequency, adaptive number. - more for longer |
| **Phylotaxy** |  |  |  |  | Primarily used w high detail vfx targeted Based on botanical classifications. |
| Opposite (distichous) | 2 | Distance | Even | Flat |  |
| Opposite (decussate) | 2 | Distance | Even | Cross |  |
| Opposite | 2 | Distance | Even | Random |  |
| Whorled | *  | Distance | Even | Star |  |
| Alternating (distichous) | 1 | Distance | Even | Flat |  |
| Alternating | 1 | Distance | Even | Random |  |
| **Bifurcation** |  | Unpredictable | Random | On Curvature | Best places to produce organic structures. Natural junctions of the parent branch |
| Flood |  | Number | Random | Random | Create targets or meshes attached to mesh generator or fill a general area at random. |
| Parent |  | Anchors | Anchors | Random | Spawn on anchors |

##### Align style 
When “Align” is enabled, generated nodes attempt to roll their initial orientation skyward as much as they can, according to the following options:

|   |   |
|---|---|
|Individual|Each node rolls skyward independently.|
|Group|All of the nodes in the group roll skyward together.|

## Spine

Orientation 
- start angle 
- roll 
- garvity / zig zag 
- noise 
- break 

## Orientation 
For leaf generator 

Orient 
- Sky influence - rotate toward sky 
deform 
- deform leaf mesh 
- vertex control - noise

## Skin

## UV 

## Mat 

## Segments
Optimization / Mesh Density. Can optimize along spline with blue curve. 

Length 
Radial 


## LOD
https://docs9.speedtree.com/modeler/doku.php?id=kcgameslod

## Hand drawn 


----- 

# Branch 
- **Branch** 
- **Trunk** 
- **Little branches**  
- **Twigs** 
- **Shell** - divide trunk to 2 and blend materials 

# Leaves
- **Batch leaf** - packed instances 
- **Mesh leaf** - access to each leaf 
- **Fond** - aspect ration depend on texture aspect ratio 

You can add one of leaves generators and open: **Edit Cutout** editor. You should add pivot, direction and plane mesh 

# Clusters
Planes with leaf clumps 

##### Bake billboard
1. Change view from perspective to orthographic  (LMB on left upper corner of viewer) or add camera ()
2. Window properties > Set screenshot safe frame > set resolution 
3.  Lighting preset > set for overcast then increases ambient light and bake AO 
4. File > export image > same width and height as in prev.   streak colors for padding, and uncheck ground. Add imagfes channels and bake 
Tip: to much collisions may look like solid from distance

---

# Features

## Forces
Just add force. 
Select generators for which you want use the force and enable 

Direction 
- Magnet 
- Direction   
- Planar 
- Return - gradual undo of forces like gravity  
Rot
- Gnali - rot on horizontal axis
- Twist - on y axis 
- Curl - 
Other  
- Mesh - (growth on object) can attract or repel -  (need to enable collision)
	- obstruct - push 
	- prune - delete and cut 
	- stop - stop growth 


## Free Hand
Hand drawn 
`Space` + `LMB` - create 

## Hand drawing 
Old 

## Shape control
- Shape control style by sphere or mesh (add mesh force enable it and then change to mesh )

## Photogrammetry
- add geo > photo branch generator
- space bar and RMB

## Collision
On toolbar
- low - will remove intersect other on same level
- medium - will remove intersection with parent
- high -

## Material / Wind


## Projectors 



```
- Vertex Editing - minor vertex change
- Bending - without  
- Click Place - clone
- Hand Drawing  - <<< !!!!  (space)
- Paint Displacement - move
- Paint Vert - move
- Paint Vert Col - color
```