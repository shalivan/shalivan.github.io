---
title: Modeling - Hard Surfaces
categories:
  - ART
tags:
  - Art
  - 3D
  - CG
description: RAW
permalink: /modeling/
aliases:
  - modeling
---
>  [[17-01-01-Modeling_Foliage]]  [[16-01-01-Sculpting]] [[21-01-01-Art]]

------------
quads - only for anim and subdiv (also better uvs).
for games - preserve shiluete

good uv layout is important !!!   - directional and logicly connecterd  
make it easy
TRIMSHEETS - uv for reuse

# Splines

|name |cont|tangents|interp|usecase|
|-|-|-|-|-|
|Linear | C0 |
|Bezier | C0/C1 | manual | some | shapes, fonts, vectro graphics
|Hermite | C0/C1 | explicit  | all | animation, physics sim , interpolation
|Catmull-Rom | C1 | auto | all | animation, path somoothing
|B-Spline | C2 (acceleration smooth)| auto | none | curvature -sensitive shapes, animation (like cam path)
|NonUniform B-Spline (NURBS) | C2 | |changing weigths

https://youtu.be/jvPPXbo87ds?t=3713



- polygonal
- box - old from box / in sculpt better
- bool
- sculpt
- nurbs - splines - bezier - oldest -industrial design smooth organic surf
- parametric max
- procedural h
- kit bash

# Basics

## Uniformize
- Scale  in m. 
- orientation - relative to world and default pose
- Time / frames
- Texel density
- Detail Density sweet spot / 
- 3 levels of detail 
[Pipelines](/pipes/)   
[Resolutions](/res/)    

- Mirrors symmetry  
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
https://twitter.com/delaneykingrox/status/1506594473979310093

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

**uv**
- uv for high. bake by uv
- make uvs straight for simulation and texturing (the direction of the fibers)

[Drape sim](/vellum/)
[Characters](/characters/)


# Subdivision

**Catmull-Clark sub**
- [Catmull–Clark subdivision surface](https://www.sidefx.com/tutorials/pragmatic-vex-1-limit-surface-sampling-introduction-opensubdiv-patches/) - using Quads casue it can optimize [YT](https://youtu.be/vTm-q-Ff7qU)
- Loop - work with triangles (remesh)








===============

ice

https://80.lv/articles/a-look-at-ice-shader-made-for-destiny-2/
