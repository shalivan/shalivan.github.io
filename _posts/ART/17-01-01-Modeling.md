---
title: Modeling
categories:
- ART
tags:
- Art
description: RAW
permalink: /modeling/
---



https://twitter.com/delaneykingrox/status/1506594473979310093

- poligonal
- box - old from box / in sculpt better
- bool
- sculpt
- nurbs - splines - bezier - oldest -industrial design smooth organic surf
- parametric max
- procedural h
- kit bash

# Basics



## Uniformize
- Scale  / orientation / time/fremes -
- Texel density
- Detail Density sweet spot / 3 poziomy density
[Pipelines](/pipes/)   
[Resolutions](/res/)    

## Workflows

- Procedural stuff for variations easly  [Procedural](/procedural/)      
- mesh wire -  games/subdivs.
-  how to textures
    1. Baked -
    2. Generic + detial, repeat - for large assets / can blow up texture calls
- meterial workflow
    - procedural repeates / reuse


   

# Common problems
- parts for bake and uvs overlaps
- symmetries
/material ID bake
- pivots        
- General meshes with equal triangles behave better: rendering performance (overdraw) / simulations (`Delanunay` max minimal angle (tend to 60) ! - smoothes interpolation but less approximation of surface when long trix better define edges)

---        


[SOP](/sop/)   
[LAB](/lab/)   

# Hard surface

## Props
    - elements should be `grounded` in scene  
    - barnacling small things around,
    - footing - awareness of  intersecting,
    - greebling materialing
    - sense of scale - 3d tend to minimize things > no sense of scale
---

# Fabric
Best simulated

- Tailoring (amount of material)  
- Material properties >  (stretch, bend, weight)    
- Grain of fabric. (weakness of cross cuts)  

- **uv**
- uv for high. bake by uv
- make uvs straight for simulation and texturing (the direction of the fibers)

[Drape sim](/vellum/)
[Characters](/characters/)

---
https://www.raywenderlich.com/6314-creating-interactive-grass-in-unreal-engine-4

# Vegetation
rośliny - kawałki z których składamy całość i do tego dodajemy na całość atrybuty  
NIE OPISANE: z liści high składamy zbrushowa roslinke  

- **References**    
 - Silhouettes - different sizes and shapes  (grass, plants, bush , tree)
 - Characteristic elements: Leaf band, Beginning, Gravity, Grouping (higher leafs more vertical change shape)
 - Characteristic behaviour: Growth towards the sun, Not vascular plants growth in shadows  (to not dry out). Moss mostly 'N' in North hemisphere.

- **Low poly model** (parts)
 - Parts (leafs, stamp)
 - Symmetry
 - Direct leaf to create planes good for view

- **Low poly cards** (for more optimised or lods)

- **Early uv** unvrap on low
 - 2 sided leaf  for detail u can apply different textures (shifted on backside)


- **Sculpt** think before sculpt if its what u need
 - Derive thickened and subdivided model from low poly.
 - Material id's for parts
 - sculpt


- **Low poly refine**
 - Check how big cutoff could be to get optimal visible part without alpha, and avoid overdraw
 - Triangulation sometimes needs to be refine.


- **Bake**
 - Bake by uv's (like cloths).


- **Compose** plants. Arrange and deform  
 - ... >?
 - Simulate to refine final shape
 - Set per object attributes


- **Export**
 - Prepare Vertex Anim. (Vertex color for movement  (main branch, leafs and thin edges ))
 - ... >?  Normals. On bush:  Custom Vertex normals - transfer normal from vdb tree form.


- **Painting**
 - Spots with color variations (some blurry)
 - Use also sharp lines
 - Paint masks: sss,
 - Veins and celular patterns
 - Vines to subsurface mask!


- **Material**
 - color
  - fuzzy shading
 - normal
  - to camera ? bottom up ?  
  - rotating normals towards camera instead of pointing them up, is a good supplement to unify grass shading, while not causing uniform ugly white sheen
  - if tangent space normals are enabled in material, your normal will be flipped for backface. While it is desired behavior for grass cards with default normals,
  - if you are using foliage with edited normals, the backfaces will have incorrect normals. Using foliage with edited normals implies disabling disabling tangent space normals and handling normals yourself in the material using two-sided sign.
  - You’d want every grass blade to have some sort of distinct specular highlights, preferably corresponding to grass blade orientation, supported by normal map. (not pointing grass normals straight up)
  - normal map is in use, it also helps if its intensity is high enough to shift surface-subsurface balance from card level to grass blade level.
- vertex anim **movement**  
  - wind and interaction, bend grass near player
   - wygiac przy playerze cardsy troche do kamery  
   - scale anim and size on distance to betere disappear LOD
   - scale grass down on last lod
   - how fast move depend on scale `smooth ramp =x*(in+1))/(x-in)`
- sss
  - SSS color should not differ considerably from albedo.
  -  SSS is obtained by sampling environment cubemap in the direction, opposite of the normal. If your grass cluster normals are pointing upwards, they will sample the skylight from bottom part. Needless to say, that if skylight is set to use black for lower hemisphere, you won’t get any subsurface from indirect light.
 - shadows ... ?

- **Placement**
 - cluster foliage, procedural placement system
 
- **Engine optimization**
 - 2 sided foliage option
 - Early z pass   

- **Lighting**

-  balance between skylight and directional light intensity. In case, when latter is overly strong, there will be distinct separation between zones of dominant subsurface and surface It feels that tweaking subsurface intensity separately for direct and indirect light we pretty good thing to have, but this one would be only tweakable per light, not per material.


[houdini tree HDA](https://youtu.be/abQtNpUUdGw)





# Subdivision

**Catmull-Clark sub**
- [Catmull–Clark subdivision surface](https://www.sidefx.com/tutorials/pragmatic-vex-1-limit-surface-sampling-introduction-opensubdiv-patches/) - using Quads casue it can optimize [YT](https://youtu.be/vTm-q-Ff7qU)
- Loop - work with triangles (remesh)
