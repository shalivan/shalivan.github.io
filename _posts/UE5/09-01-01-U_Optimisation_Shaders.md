---
title: U Render pipelines / optimization / compression
description: RAW
categories:
  - PXL
tags:
  - Rendering
  - Unreal
  - Tech
  - Art
  - Rendering
  - RealTime
  - GameDev
permalink: /uoptimizationshaders/
aliases:
  - uoptimizationshaders
---
[[05-01-01-U_BP|ubp]]
[[05-01-01-U_Code|ucode]]



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








---

# Debug

####  Prepper for Debug

- Measure performance in **ms**    
- project settings > disable **smooth framerate**
- Turn off **VSync** (r.vsync 0)
- play in **standalone**, with minimized editor  


#### Options

- **G buffer**  high res normals
- **D buffer** pass for decal otherwise are in lioght pass defered
- **early Z psas**  for opaque and masked - bufffer for Opacity
- extended tonmemaping  EV  w exposure
- accurate velocity from degormer - have cost, for better foliage anim with Temporal AA  

---

# Tools

`Asset audit.`      
`Size map` - take in accound hard refs.   
`Reference viewer` -     

#### Visual Logger
[VisLog](https://docs.unrealengine.com/4.26/en-US/TestingAndOptimization/VisualLogger/)


#### Render Resource Viewer (5.2: Experimental) - 
The Render Resource Viewer is a tool that gives full visibility into GPU memory allocations and render resources—such as Vertex Buffers and Index Buffers—and which assets they come from, like Static and Skeletal Meshes. This provides artists and developers with information needed to optimize GPU memory and keep their projects within their rendering budget.


## Unreal  

### Session Frontend
can manage and test daand legacy profiler but better is uInsights   
*CPU* + *GPU* same time, (you can load files from sessions `stat Startfile`, `stat Stopfile`)  
Window > DevTools > `Session Frontend`     

### Unreal Insights
Analyze memory allocation
Standalone profiling system. Smaler impact on execution.

LLM - `Low level memory tracker ` (in unreal insights)

## [Intel Frame Analyzer](https://software.intel.com/en-us/gpa/graphics-frame-analyzer)

1. You need to package game
2. Run Graphic monitor andd click analyse application
3. Enable in U4: `ToggleDrawEvents`
4. `Ctrl` + `Shift` + `C` - to capture
5. Enable in U4: `ToggleDrawEvents`



## [Nvidia Nsight graphic](https://developer.nvidia.com/gameworksdownload )

- frame debuger
- frame profile (similar but more like profiling than debuging)
- generate C++ capture - collect frames   
- gpu trace  


`Timeline` API calls as events   
`Resource view` textures and bufffers in scene (tak buttobn to find)   
`API inspector` stages : input assembler , VS, PS  
`API statistic` !!! view. > shaders wiev by comlexity and times      
`Shader view` ??? Linked ptograms view   
`Range Profiler` time ing using low lvl metrics (bottleneck) hi lvl overview.   

1. Point to exe file
2. Run



## RenderDoc

## Intel GPA
Graphic performance analyzing
Tools for doebug:
- 'Graphic frame analyzer' is fro unreal can capture fragment of stream.
  - download from github
  - copy to plugins to ue install
  - enable in project

[Interl GPS Epic YT](https://youtu.be/KuF4OTH9WjA)


Gauntlet - automate testing

---

# [UE4 CVars](http://www.kosmokleaner.de/ownsoft/UE4CVarBrowser.html)   


`ToggleAllScreenMessages`  


##### Show commands


```
r.screenPercentage
r.SetRes 1920x1080f
r.defaultfeature.antialiasing 0
```
```
freezrendering
show bounds
show collisions
```



##### Shadows and reflections
Shadow quality (`sg.ShadowQuality 0..4`).      
Screen space reflections: Quality `r.SS.MaxRoughness 0.0..1.0` `e.SSR.Quality 0..4`     


-----


Scalability settings >
