---
title: Rendering
description: Rendering
categories:
- PXL
tags:
- Tech Art
- Rendering
- CG
- Light
- Shaders
permalink: /rendering/
---


# Rendering
*Defered* - more lights is ok    
*Forward Rendering* - bneter with translucency   
[Lighting](/ulight/)  
[Light](/light/)  
[Camera](/camera/)     
[Algebra](/algebra/)  
[Unreal Material](/umat/)   
Book :  Phisical based rendering From theory to implementatnio


# Rasterization

Real time mostly. Wievport or games.
- Shooting rays from cam (primary rays), and sample shaders. Rays are inddependend (GPU friendly )
- from point, ray to light and check angle to determine shading (hard shadow)
- for soft shadows must eveluate more rays (distributed light trac),  soft shad, bluty reflect (hard reflection need one sample, blury more) , dof, motion blur
- expensive to calculate GI (indirect illumination)

https://fgiesen.wordpress.com/2011/07/09/a-trip-through-the-graphics-pipeline-2011-index/





# Path Trace
Offline recently and now with RTX in realtime features
Full indirect illum :  Recursively evaluate hemisphere of multiple rays of each point we hit geometry.

### Ray trace
- trace from camera
- if hit surface shoot ray to lightsource and evaluate shadow and reflections  and refractions
- indirect illumination (hard cost) we have to trace multiple rays depend of type of mat. Those patrhs not depend on eachother so we can calculate it independly (gpu).
- light decay :(shoot trace from geo to light) and
   - tradfitional: shoot ray to light
   - path trace: (full indir illum) multiple rays and recursyvly calculate for each additional hits .




# Shaders & Mateirals

everything has fresnel
## Materials

- **Subsurface** (BSSRDF) -
- **Conductors** Spec and glossy refl, in conductors typicaly metlas. dep on wave len (yellow gold) (reflect most light and turn non reflected into heat)
- **Dielectrics** - (BTDF shader ie) reflected and refracted (IOR,bend ing rays on medium change) sometimes scatter (as subsurf) and flat ss is difuse
(BSDF) -
Fresnel effect in reflections.


## Shader Rendering
reflect refract & scatter ...
`BRDF` - bidirectional reflection distribution fn.  
hemisphere for mat / and directional spike for reflectivces. More blury reflection more direction samples > longer rendering
`BTDF` - transmision (reflectiw + (refracted + iro)) (so dielectric render slower ) (transmited scattering distribution (distribution is every time medium is changed )
`BSSRDF` -SubSurfaceScarttering  scattering. Diffuse is SS on tiny area !!!!!!!!!
`BSDF` - bidiirectional scatering



## Shader
### VS Vertex shader    
### PS Pixel shader (old fragment)    

grid of pixels that work paralel


### Compute shader   
in paralel on gpu
subdivisions workgroups and in each group divisions


### Mesh shader    
Mesh Shaders    
- for new tessalation


### Task shader
 call based of cam frustrum   

## Material (ray tr ?)

###
`Conductors` - (tyupicly reflect depend on wave leng. give color)  
`Dielectrics` - (refl + refract + scatter refracted (subsurf but rather difuse ))   
Refl + refr >> have fresnel.

http://filmicworlds.com/blog/everything-has-fresnel/






### Camera simulation


### Light
`CRI` color rendering index  
if iluminated point id to 5x dist from light we can aprox as point light
directional aprox to (rownolegle)
dome light - `hdri light`





Each thread is not just blind but also memoryless.
Shader Language has a single main function that returns a color at the end.



# UE

 Gi
 ddgi -dynamic direct gi -  proby

 https://www.youtube.com/watch?v=ZefvmV1pdP8&t=121s


 https://www.pbr-book.org/3ed-2018/contents

 -----------------


 aproximation on physic lighting


 sampling is costly    
 combinig textures to one help with streaming  

 ### assembly
 https://interplayoflight.wordpress.com/2021/04/18/how-to-read-shader-assembly/
