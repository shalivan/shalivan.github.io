---
title: Modeling - Vegetation
categories:
  - ART
tags:
  - Art
  - 3D
  - CG
description: Vegetation, foliage
permalink: /foliage/
aliases:
  - foliage
---
> Pxlink: [Composition]  [Color](/color/)  [Modeling](/modeling/)  [Sculpting](/sculpting/) 
 >Obsidian: [[21-01-01-Art]]   [[17-01-01-SpeedTree]]  [[17-01-01-Modeling]], [[17-01-01-Modeling_Foliage]]  [[18-01-01-Color]] [[16-01-01-Sculpting]] [[14-01-01-Procedural]] [[08-01-01-Material]]  [[20-01-01-VisualDesign]] [[17-01-01-Paint]]  [[14-01-01-Procedural]]  [[12-01-01-LevelDesign]] 

https://www.exp-points.com/sven-mren-foliage-study <
https://www.textures.com/tutorials/Creating%20Realistic%203D%20Plant:%20Shaping%20The%20Leaves

[YT Houdini # Speedier Trees in Houdini: Botanically inspired production ](https://www.youtube.com/watch?v=e8ITnlrcvcQ&t=1709s)
https://www.textures.com/tutorials/Creating%20Realistic%203D%20Plant:%20Shaping%20The%20Leaves


# Vegetation

## Technical pipeline

We need parts which we will combine into objects. then objects will be used in composition.

#### **References**    
  - **Silhouettes** 
	  - different sizes and shapes  (grass, plants, bush , tree)  
	  - negative spaces 
	  - slightly noisy 
	  - organic and interesting on any angle
  - **Clustering** - cluster of leaves.
  - **Characteristic elements**: Ecosystem-biomes, Leaf band, Beginning, Gravity, Grouping (higher leaf more vertical change shape)
  - **Characteristic behavior**: 
	  - Growth towards the sun, 
	  - Not vascular plants growth in shadows  (to not dry out). 
	  - Moss mostly 'N' in North hemisphere.
	  - New trees growth only where is light - new and old forests. young mid forest compete for light so much there could be no place for new trees. 
  - where plants growth - in garden are clean
  - sizes: small mid …
  - natural shapes:  thickness constraint by Leonard DaVinci: - at any point parent branch needs to have combined thickness of all the tow branches. 


#### **Modeling**    
Methods for foliage production: 
- Pate: direct modeling / L system / self organizing models 
- Present: Skeletonization / Photogrammetry / Simulation 
- Future: Lidar / AI / Single View reconstruction / L-Systems

### problems: 
- branch transition - additional band with alpha
- clusters - atomic elements  + decorative detials + trunk 

##### Building parts (molecules ? nodes?)
```
**Low poly model** (parts)
  - Parts (leafs, stamp)
  - Symmetry
  - Direct leaf to create planes good for view

**Low poly cards** - for more optimised models or lods. Used with 'leafs clusters' (thigs)


**Early uv** unvrap on low
  - 2 sided leaf  for detail u can apply different textures (shifted on backside)

**Sculpt** think before sculpt if its what u need
  - Derive thickened and subdivided model from low poly.
  - Material id's for parts
  - sculpt

**Low poly refine**
  - Check how big cutoff could be to get optimal visible part without alpha, and avoid overdraw
  - Triangulation sometimes needs to be refine.

**Bake**
  - Bake by uv's (like cloths).
```


sposob 2 :
- zrob high w z.

**Compose** plants. Arrange and deform  
  - ... >?
  - Simulate to refine final shape
  - Set per object attributes

**Export**
  - Prepare Vertex Anim. (Vertex color for movement  (main branch, leafs and thin edges ))
  - ... >?  Normals. On bush:  Custom Vertex normals - transfer normal from vdb tree form.

**Painting**
  - Spots with color variations (some blurry)
  - Use also sharp lines
  - Paint masks: sss,
  - Veins and celular patterns
  - Vines to subsurface mask!

**Material**
- color
    - fuzzy shading
    - blend with landscape layer or use landscape layers as a mask
- normal
    - to camera ? bottom up ?  
    - rotating normals towards camera instead of pointing them up, is a good supplement to unify grass shading, while not causing uniform ugly white sheen
    - if tangent space normals are enabled in material, your normal will be flipped for backface. While it is desired behavior for grass cards with default normals,
    - if you are using foliage with edited normals, the backfaces will have incorrect normals. Using foliage with edited normals implies disabling disabling tangent space normals and handling normals yourself in the material using two-sided sign.
    - You’d want every grass blade to have some sort of distinct specular highlights, preferably corresponding to grass blade orientation, supported by normal map. (not pointing grass normals straight up)
    - normal map is in use, it also helps if its intensity is high enough to shift surface-subsurface balance from card level to grass blade level.
- vertex anim **movement**  
    - rotate on slopes to have grass pointing up all the time !!!
    - wind and interaction, bend grass near player
    - wygiac przy playerze cardsy troche do kamery  
    - scale anim and size on distance to betere disappear LOD
    - scale grass down on last lod
    - how fast move depend on scale `smooth ramp =x*(in+1))/(x-in)`
- sss
    - SSS color should not differ considerably from albedo.
    -  SSS is obtained by sampling environment cubemap in the direction, opposite of the normal. If your grass cluster normals are pointing upwards, they will sample the skylight from bottom part. Needless to say, that if skylight is set to use black for lower hemisphere, you won’t get any subsurface from indirect light.
- - off specular on bottom 
- shadows ... ?

**Placement**
  - cluster foliage, procedural placement system

**Engine optimization**
  - 2 sided foliage option
  - Early z pass 

**Lighting**
  -  balance between skylight and directional light intensity. In case, when latter is overly strong, there will be distinct separation between zones of dominant subsurface and surface It feels that tweaking subsurface intensity separately for direct and indirect light we pretty good thing to have, but this one would be only tweakable per light, not per material.

- use shadow, ? without can be smoother.


---


# Foliage


#### Grass
grass - https://www.artstation.com/artwork/qQVZqR

#### Fungi

#### Roots 

#### Trees

#### Moss

'Lot more porous, with amassive amount of self-shadowing, ambient occlusion, and transmitted light. The moss itself tends to have a lighter color at the tips than deeper towards the base. And there’s a strong viewing angle dependency – when viewed straight on, you can see down into the shadows between the fibers, and while viewed from an angle, only the tips are visible.'


---

# Tools
Available tools for foliage creation: 2023
- SpeedTree https://www.youtube.com/c/SpeedTreeMiddleware
- H GrowInfinite 1.2.19  https://fxmode.gumroad.com/l/GrowInfinite  
- H Simple Tree Tools 2.6    https://www.youtube.com/watch?v=0VqA99bpGHc
- H Labs https://www.youtube.com/watch?v=IZ5uJYg0ELM&list=PLXNFA1EysfYkiIWvM3CBXO-TsYE1H42dK   https://www.sidefx.com/tutorials/tree-generator/
- B The Grove3d  https://www.thegrove3d.com/releases/the-grove-release-6/ Blender  https://www.thegrove3d.com/
[houdini tree HDA](https://youtu.be/abQtNpUUdGw)
- Houdini pegasus tools - procedural sim 


-----------------


# Houdini Pegasus foliage 


4 types of nodes: 
- control
- component 
- switch 
- solver 


---


https://youtu.be/pVKDfZMffpc
[YT kanał H](https://www.youtube.com/c/RickBanks/videos)
[Tut dynamic grass](https://www.raywenderlich.com/6314-creating-interactive-grass-in-unreal-engine-4)
[FoliageLibrary](https://treelib.ca/)    
Bruno Moulia

> Book history : natural design of nature - computer generated plants and organics Oliver Deussen, Bernd Lintermann
