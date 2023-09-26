---
title: Modeling - Vegetation
categories:
- ART
tags:
- Art
description: Vegetation, foliage
permalink: /foliage/
---

---
https://www.raywenderlich.com/6314-creating-interactive-grass-in-unreal-engine-4

----
bruno moulia


# Vegetation

Library: https://treelib.ca/    


## Technical pipeline

We need parts which we will combiene into objects. then objects will be used in composition
#### **References**    
  - **Silhouettes** - different sizes and shapes  (grass, plants, bush , tree) - organic and instertesting on any angle - negative spaces - slightly noisey
  - **Clustering** - cluster of leaves.
  - Characteristic **elements**: Leaf band, Beginning, Gravity, Grouping (higher leafs more vertical change shape)
  - Characteristic **behaviour**: Growth towards the sun, Not vascular plants growth in shadows  (to not dry out). Moss mostly 'N' in North hemisphere.
  - where plants growth - in garden are clean
  - sizes: small mid ...


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
- shadows ... ?

**Placement**
  - cluster foliage, procedural placement system

**Engine optimization**
  - 2 sided foliage option
  - Early z pass 

**Lighting**
  -  balance between skylight and directional light intensity. In case, when latter is overly strong, there will be distinct separation between zones of dominant subsurface and surface It feels that tweaking subsurface intensity separately for direct and indirect light we pretty good thing to have, but this one would be only tweakable per light, not per material.

- use shadow, ? without can be smoother.


# Speed tree

## Parameters
Constuct proceduraly, important workflow tips:  
- **Generators** - Use generator to get behaviour on change  
- **[% of parent]** - Use % of parent to be procedural (can growth)  
- **[+-]** - Vatiance - help with seed randomization    
- **[blue curve]** - Profile Along branch      

## Options

#### Generators
- **Classic** - old
- **Absolut** - number of branches - limited not adaptive! for main stemps and trunk
- **Absolut steps** - Absoolut + steps (steps=few from one ) (number of branches will not change )
- **Interval** - frequency (adaptive)
- **Phylotaxy** - real liofe leafs arangement
  - opposites / alternting
  - whorlde - steps + childrens of step
  - bifurcation - spliting on curvature (nothing will happen without noise) usefull, natural but unpredictable


#### **Gen**
 - Frequency - how many
 - Spred - noise on each step
 - Spiral - rot steps
 - boundaries start - end
 - position (biass to start-end)
 - scale - global scale
 - sink - z-depth  


#### **Spine**
- Length -
- Orientation
  - Start angle - Angle of branch
- Shape
  - Gravity
- Noise
- Break - >???

#### **Skin**
- .

#### **Displace**
- .

#### **Segments**
- .  

## Leafs / Cards


..
Batch leaf generator !!!!! <

1. Create Branch
2. Window properties > screenshot safe frame > [x] - save frame
3. Leaf mesh generateor (to acces every leaf)
tips: to much collisions may look like solid from distance
-  File > export material.

4. create new material
5. Open mesh editor which is tide to material

...


## Free Hand
- Vertex Editing - minor ver change
- Bending - without  
- Click Place - clone
- Hand Drawing  - <<< !!!! )(space)
- Paint Displacement - move
- Paint Vert - move
- Paint Vert Col - color

## Photogrametry
- add geo > photo branch generator
- space bar and RMB

## Forces

## Collision
On toolbar
- low - will remove intersect other on same level
- midium - will remove intersection with parent
- high -

## Material / Wind

-----------------

# Foliage


#### Grass
grass - https://www.artstation.com/artwork/qQVZqR

- off specular on bottom
-


#### Moss

lot more porous, with a
massive amount of self-shadowing, ambient occlusion, and transmitted light. The
moss itself tends to have a lighter color at the tips than deeper towards the base.
And there’s a strong viewing-angle dependency – when viewed straight on, you can
see down into the shadows between the fibers, and while viewed from an angle, only
the tips are visible.



### Tools
- SpeedTree https://www.youtube.com/c/SpeedTreeMiddleware
- H GrowInfinite 1.2.19  https://fxmode.gumroad.com/l/GrowInfinite  
- H Simple Tree Tools 2.6    https://www.youtube.com/watch?v=0VqA99bpGHc
- H Labs https://www.youtube.com/watch?v=IZ5uJYg0ELM&list=PLXNFA1EysfYkiIWvM3CBXO-TsYE1H42dK   https://www.sidefx.com/tutorials/tree-generator/
- B The Grove3d  https://www.thegrove3d.com/releases/the-grove-release-6/ Blender  https://www.thegrove3d.com/
https://www.youtube.com/c/RickBanks/videos


[houdini tree HDA](https://youtu.be/abQtNpUUdGw)

https://youtu.be/pVKDfZMffpc
NIE OPISANE: z liści high składamy zbrushowa roslinke  
