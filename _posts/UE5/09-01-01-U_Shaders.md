---
title: U Render pipelines / optimization / compression
description: RAW
categories:
  - PXL
tags:
  - Rendering
  - Unreal
  - Tech
  - Rendering
  - RealTime
  - GameDev
permalink: /uoptimizationshaders/
aliases:
  - uoptimizationshaders
---
> Obsidian: [[05-01-01-U_BP]] [[05-01-01-U_Code]]  [[09-01-01-U_Optimisation]] [[11-01-01-U_Rendering]]


https://calvinatorrtech.art.blog/2023/12/20/optimizing-shaders-in-unreal-engine/
https://ryandowlingsoka.com/unreal/hanging-vertex-animation/

(blur is expensive, you need render targets)


# Material



## Translucent in Deffered problems


## Motion Blur
Visualise > motion blur (in simulate) (colored in motion)    
Bufer visualitsation > Velocity     
`Accurate velo` in settings !

PP@cam can ovveride
- per object setting - will exclude from MB (not working if acucurate velo is enable in settings)

type of object
- sequence - (just work)
- BP set actor location - (just work)
- Verte offset material - (in project settings + material:  support accurate velo from vert deform)
- in particle system - material: Particle motion Blur Fade !!!!!(cascade override, and transulcent only on gpu)
- on spline - material: preview frame switch

https://youtu.be/r1BCJt22oHY



Separate translucency


## Compression

#### Textures used
`Window/Statistics/..` - Used texture    

#### Unreal Textures Compression:
| Unreal | DirectX |   | | | | |4096 x RGB|
| --- | ---  | ---  | ---|---|---|---|---|
| Default  (sRGB)| DXT1| BC1 | RGB(4bit) + A(1bit) |  |  Most efficient Has a maximum color resolution of 16 bits (as old VGA adapters.)  | 8:1| 11Mb |
||DXT1|BC2|RGB(4bit) + A(4bit)|||6:1 |11Mb|
| Default  | DXT5 | BC3 | RGB(4bit) + A(8bit) |Color+Height | BC1/DXT1 for the RGB part and BC4 for A (8BPP) This gives you better transparency.| 4:1 |11Mb
| Mask (RGB)| DXT1 / DXT5 | |  |  |  Alpha channel is half of the data ! (1/2 memory for alpha)|4:1| 11Mb
| Grayscale |  | BC4  |R  (8bit) | 'R' channel| Single channel  'R' uncpmpressed | - | 21.8Mb
| NormalMap | DXT5  |BC5 | | Normal specific | Extremely well on the gradient D3D11-more complex  |(2xBC4)|  21.8Mb
|| |BC7 | BGR A (4/16bit)|  |Higer quality but compressed|4:1 | 21.8Mb
| Displacement ||| R (8/16bit) |Displacement|  | - |  21.8Mb
| Vector Displacement | || BGR (8bit)  | 3d Displacement | | - | 87.4Mb
| HDR Compres (RGB)  | | BC6 H | Float RGBA (8/16bit) ||  | | 21.8Mb
| HDR (RGB) |  |BC6| Float RGBA  | IBS, Skybox|  HDR D3D11 - more complex | - |  175Mb
https://youtu.be/3H-HGlsC0NY


# Shader Optimisation 
[Site: Shader optimisation](https://calvinatorrtech.art.blog/2023/12/20/optimizing-shaders-in-unreal-engine/)

#### Platform Stats tool inside the Material Editor

-  vertex shader for a skeletal mesh is going to be a lot heavier than a static mesh!
- use Vertex interpolators  (depend on platform can use up to 16)


|   |   |   |   |
|---|---|---|---|
|Instruction|Assembly|Cycles|Notes|
|* (operator)|mul|4||
|+ (operator)|add|4||
|– (operator)|–|–|Seems to be free to flip a value to negative|
|/ (operator)|mul, rcp|20|Compiled to multiply by reciprocal (16 cycles)|
|pow|exp|16|If constants are used this will vary into a string of muls|
|sqrt|sqrt|16||
|sin|sin|16||
|cos|cos|16||
|tan|sin, mul, rcp, cos|52|Compiled to use identity of tan = sin/cos, where the divide is a mul rcp like a regular divide, making this one of the most expensive instructions!|
**Finding the distance between two points** on the can be a fairly expensive operation – because the distance is just the length of the delta vector!  AB == B – A, so distance(A, B) == length(AB)! Getting the length of a vector is determined by sqrt(x^2 + y^2 + z^2) Getting the distance/length costs us ~28 cycles!

|   |  <br>  |   |   |
|---|---|---|---|
|length(A)|sqrt(x^2 + y^2 + z^2)|sqrt, mul, mac, mac|28 cycles|

comparing distance values we can just use distance squared! (just square your comparison value if it’s a regular distance value) If we’re building a (signed) distance field or doing this in a loop then we can do this using distance squared too, and then sqrt the result, so we only need to sqrt once! Obtaining the distance squared can be done with the dot product, i.e. dot(x, x) – this is just a very easy way of returning the distance squared.




# Virtual texturing  streaming
New aproach to mips.  Divided in to tiles
- memory optimisation where we pay a small amount in performance.  
- better granularity
- load smaller part of image

1. Project settings > Engine Rendering > Enable
2. Enable Virtual Texture Streaming in texture options (or convert to vertual texture)
3. Sample type in material to: Virtual Textura

cost of normal sample even more gpu instructions (2 tez samples: 1 per stack and 1 per each  )
Virtual texture stack: - using same uvs  (see in material stat)

there is bulk convert on texture in browser to convert many at once

# Virtual texture runtime
same tech in runtime at GPU  (shading cash)
not change frame to frame
- performance optimization not memory
- frame to frame read cache
- camera position independend ()
- decoding cost small
1. create virtual texture asset.
2. use node runtime virtual texture

```
r.VT.borders 1
```
- stack as much with same uv  (base color spec ... nm )
