---
title: U Optimization
description: RAW
categories:
 - PXL
tags:
- Rendering
- Real Time
- Unreal
- Game Dev
- Tech Art
- Rendering
permalink: /uoptimization/
---

Separate translucency

1000 ms in 1 sek = 1000/30 = 33,3 ms to render frame


[Unreal Optimisation Guide](https://unrealartoptimization.github.io/book/pipelines/forward-vs-deferred)

It's the pass where all meshes (this includes landscapes, skeletal meshes etc) are drawn into the G-buffer.
---


# Deferred Render pipeline  


All lights are applied deferred in Unreal Engine 4, as opposed to the forward lighting path used in Unreal Engine 3. Materials write out their attributes into the GBuffers, and lighting passes read in the per-pixel material properties and perform lighting with them.

1. Before render: CPU game context   
2. Before render: CPU (mostly) what to render  
3. Render: GPU  render pixel on screen

Check if time of frame is bigger from CPU or GPU. (cause threads must wait one for another)

`StartFPSChart` / `StopFPSChart`    
`Stat fps` / `Stat Unit` / `Stat UnitGraph`    

Garbage Collector

###  Render passes  

| Render passes |  | dependences
| -- | -- | -- |
`LightCompositionTask_PreLighting`| | Decal count, PP AO radious    
`CompositionAfterLighting` |SS profile | Screan area of SSS   
`ComputeLightGrid` | | Movable lights count   
`Light-ShadowedLight` | | Lights count&rad , trix of shadow-casted       
`FilterTranslucentVolume` | | Lights count     
`ShadowDepths` | Depth maps | Lights count&rad, trix of mov objects, quality    
`ShadowProjection`|
`PrePass_DDM` opaque Early depth| AO, culling, DBuffers.| Tricount of opaque, early-z settings   
`HZB` hierarchical Z-buffer|   Culling and SSRT (refl, AO)  | huge in editor cost !!
`Base pass` G-buffers (compo) | Fog, Dbuff-decals| Trixcount + Shader complexity, number of mats.  
`Translucency` | | Area of translucency, overdraw, (in FSR: light count)  
`PartilceSimulation / Injection` | Scene depth collisions.| number of particles  
`PostProcessing` | Temporal, Exposure ..| PP features, and  blendables   
`RenderVelocities` | |Num of moving objects and tri-count!
`ScreenSpaceReflectiion` ||  (cost increaase with rough),



## Game thread
CPU code - Game logic , Tick and transforms movement spawning physics, positions, AI.

`Stat game` - generally how things ticks on CPU
 - World Tick - check actors ticking in scene  consider timers, toggling, reduce intervals, use dispatchers. Move to C++
 - Blueprints - construction script > longer time to spawn

`dumpticks` - command to show detailed tick list



## Draw thread
CPU graphic render thread. Will cull things not in cam,  create list. critical in open enviros.
(10-15+ k obj can cause problem)   
- Frustum culling  - in cam
- Hardware occlusion from  scene buffers   

`Stat SceneRendering`     
 - RenderViewFamily -
 - GatherRayTracingWorldInstances -  
 - InitViewa -
 - DynamicShadow -  
 - RenderQuery Resoult -   

`Stat SceneUpdate `  
 - UpdatePrimitive -  

`Stat SceneMemory`    
 - PrimitiveMemory -  
 - SceneMemory -
 - Rendering Mem stack memory -

### Draw calls
Fixed cost per call. bigger then polycount.

Instancing a mesh provides performance benefits even if the total number of draw calls does not reflect that

Using Instances bring up the Stat UNIT and watch the DRAW versus GPU (CPU vGPU) and notice when you instance a mesh the CPU time remains fairly consistent depending on the additional information you are wanting to pass to each instance, while the GPU will increase. All of these numbers are still dependent on the size of your mesh and the type of material setup and the ultimate limitations of your CPU and GPU. [src](https://answers.unrealengine.com/questions/127435/using-instanced-meshes-doesnt-reduce-draw-calls.html)  
Instanced meshes will reduce the draw call overhead on the CPU but will not reduce the GPU cost.
- only way to group meshes into one draw call is by using instanced meshes
- Meshes using the same material/instance will still take one draw call each
 - 3 meshes using the same material: set shader, draw mesh #1, draw mesh #2, draw mesh #3  
 - 3 meshes using a different material each: set shader #1, draw mesh #1, set shader #2, draw mesh #2, set shader #3, draw mesh #3  



> Instancing being a special case of batching. With a scene rendered with many small or simple objects each with only a few triangles, the performance is entirely CPU-bound by the API; the GPU has no ability to increase it. More precisely, "the processing time on the CPU for the draw call is greater than the amount of time the GPU takes to actually draw the mesh, so the GPU is starved." [Moeller, Real Time Rendering, 708]. So Batching attempts to allow the CPU to combine a number of objects into a single API call. In the case of Instancing it is the one mesh and the number of times you are drawing with a separate data structure for holding information about each separate mesh.







## GPU thread
GPU graphic render thread. Draw final frame.

1. vertex shader   
2. tessellation   
3. geometry shader  
4. pixel shader  


`Stat GPU`

basepass. canvasDrawTile, Post, Shadow Depths. Prepass< DLSS  Global DistanceFieldUpdate, Volumetric Fog, DOF, Translucency, Lights, Comp Prelight,


`ProfileGPU` -  `Ctrl` + `Shift` + `,` -  GPU Visualizer window (Single frame on gpu)  you can dump it to log      

- **PrePass** -
- **EarlyZPass** - (default: partial z pass). DBuffer decals require a full Z Pass `r.EarlyZPass` (more draw calls, less overdraw during base pass).
- **Base Pass** - When using deferred, simple materials can be bandwidth bound. Actual vertex and pixel shader is defined in the material graph. There is an additional cost for indirect lighting on dynamic objects.
   - StaticOpaqueNoLightmap - Cost of rendering meshes with Opaque material and dynamic light.
   - StaticMaskedNoLightmap - Cost of rendering meshes with Masked material and dynamic light.
   - StaticOpaqueLightmapped - Cost of rendering meshes with Opaque material and static lightmap textures.
   - StaticMaskedLightmapped - Cost of rendering meshes with Masked material and static lightmap textures.  
- **Shadow map** -  Actual vertex and pixel shader is defined in the material graph. The pixel shader is only used for masked or translucent materials.
- **Shadow projection/filtering** - Adjust the shader cost with r.ShadowQuality.Disable shadow casting on most lights. Consider static or stationary lights.
- **HZB** - Occlusion culling occlusion has a high constant cost but a smaller per object cost. Toggle `r.HZBOcclusion` to see if you do better without it on.
- **Deferred lighting** - This scales with the pixels touched, and is more expensive with light functions, IES profiles, shadow receiving, area lights, and complex shading models.
- **Tiled deferred lighting** - Toggle `r.TiledDeferredShading` to disable GPU lights, or use `r.TiledDeferredShading.MinimumCount` to define when to use the tiled method or the non-deferred method.
- **Environment reflections** - Toggle `r.NoTiledReflections` to use the non-tiled method which is usually slower unless you have very few probes.
- **Ambient occlusion** - Quality can be adjusted, and you can use multiple passes for efficient large effects.
- **Post processing** - Some passes are shared, so toggle show flags to see if the effect is worth the performance.
- Translucency  
- Lights
- Fog [Oskar, fix stat gpu](https://youtu.be/SXLYy6D1y80?t=603)   




 Turn off features to profile:

 |||
 |--|--|
 `Show StaticMeshes` |
 `Show SkeletalMeshes` |
 `Show Particles` |
 `Show Lighting` |
 `Show Translucency` |
 `Show ReflectionEnvironment` |
 `Show InstancedStaticMeshes` |
 `Show Landscape` |
 `Show Fog` |
 `Show MotionBlur` |
 `Show ScreenSpaceReflections` | Toggles screen space reflections, can cost a lot of performance, only affects pixels up to a certain roughness (adjusted with r.SSR.MaxRoughness or in postprocess settings).
 `Show AmbientOcclusion` |
 `Show DirectionalLights PointLights SpotLights` |
 `Show DynamicShadows` |
 `Show GlobalIllumination` |
 `Show LightFunctions` |
 `Show PostProcessing` |
 `Show ReflectionEnvironment` |
 `Show Rendering` |
 `Show Tessellation` |


### Shader Complexity

### Light Complexity

`ShowFlag.LightComplexity` -
minimize radii
Watch stationary light overlap
- Cull lights and shadows

## Memory


 RHI - memory and so on...   affected by editor!    

 `Stat RHI`   
 `r.rhicmdbypass 1`   
 `r.rhithread.enable 0`   
 `r.showmaterialdrawevents -1`   


cache   
cpu upload mem  
disk  
steraming pool    



---



# Bottlenecks


https://zhuanlan.zhihu.com/p/36851846  


Game thread:    
- more complicated construction script more expensive to spawn!
- Animation fast path,. more lighting icons in anim BPO better.

Draw Thread:   
- **Draw Calls** - command send , combine models, not too big cause: occlusion, collision, memory  
- number of obj  (10-15+ k obj can cause problem)      

GPU:  
- Over shading  **Quad Overdraw** - small or thin triangles (because it perform operation in bigger tile)  (watch for tessellation)  
- Shaders complexity on **Opacity**    
- **Shadow Casting** -  
- **Too many texture samples** - use bandwidth (compression and texture packing to channels help)   

Assets:  
- **Splits on uvs** adds to vertex count - (memory and disk space)
- **Too many vertex attributes** - (extra UV channels)
- precise uv
- colision setup
- affect navmesh
- shadow distances and turn off for small
- tick  

---


# Forward Render pipeline  

...


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


## Unreal  

### Textures used

Window > Statistics - Textures used   

###  Session Frontend
*CPU* + *GPU* same time, (you can load files from sessions `stat Startfile`, `stat Stopfile`)  
Window > DevTools > `Session Frontend`     



### Visual Logger
[VisLog](https://docs.unrealengine.com/4.26/en-US/TestingAndOptimization/VisualLogger/)

---

## Unreal Insights
Standalone profiling system. Smaler impact on execution.


---

## Intel Frame Analyzer   

1. You need to package game
2. Run Graphic monitor andd click analyse application
3. Enable in U4: `ToggleDrawEvents`
4. `Ctrl` + `Shift` + `C` - to capture
5. Enable in U4: `ToggleDrawEvents`

https://software.intel.com/en-us/gpa/graphics-frame-analyzer

---

## Nvidia Nsight graphic

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

https://developer.nvidia.com/gameworksdownload    

## RenderDoc

## Intel GPA
Graphic performance analyzing
Tools for doebug:
- 'Graphic frame analyzer' is fro unreal can capture fragment of stream.
  - download from github
  - copy to plugins to ue install
  - enable in project




https://youtu.be/KuF4OTH9WjA
---

# UE4 CVars:  


[CVar list](http://www.kosmokleaner.de/ownsoft/UE4CVarBrowser.html)   


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




---

# Compression

#### Unreal Compression:

Unreal | Compression |   | ||
--- | ---  | ---  | ---||
Default  | DXT1, BC1 |  | (DX11) | (sRGB) no alpha
Default  | DXT5, BC3 | | (DX11) | (sRGB) with alpha
NormalMap | DXT5 BC5 | | (DX11) | (RGB) Nm
Mask | DXT1/5 |  || (RGB) Linear Color
 | BC7 | B8G8R8 A8| (DX11) |
Grayscale | R8, RGB8 | G8 || (sRGB) B&W masks
Displacement | R8 |8/16bit || surface displacement
Vector Displacement  | BGR8| Standard 8bits  | | 3d displacement
HDR |  | Float RGBA  | | (RGB) Linear Color IBS, Skybox
Alpha | BC4 |   |(DX11)| (RGB) Linear Color
HDR Compres  | BC6H | Float RGBA  |(DX11) | (RGB) Linear Color


#### Block Compressions: ####

. | Compression |  | |
--- | ---  | ---  | ---  
BC1 | RGB + A(1bit)| 4  |   
BC2 | RGB + A(4bit)| 4  |
BC3 | RGBA | 4 + 8A | BC1 for the RGB part and BC4 for A col+Hmap
BC4 | R | 8 | height maps
BC5 | RG | 8  | 2xBC4
BC6 | RGBA(Float) | 8-16 | can natively store HDR D3D11-more complex
BC7 | RGB / RGBA | 4-16 | xtremely well on the gradient D3D11-more complex

#### DirectX Compression: ####

. | | |
--- | ---   | ---    
DXT1 | RGB + A(1bit)| 4BPP bits per pixel, and has a maximum color resolution of 16 bits (as old VGA adapters.)  6:1
DXT3 | RGBA | Better use 5 alpha channel (only 4 bits)
DXT5 | RGBA | 8BPP  4:1 uses DXT1 for the color part, but adds another 4 bits per pixel of alpha. This gives you better transparency.


-------------

Sources  
Tech Art Aid   

https://youtu.be/UZH4vZ0NDAw  


P4\Game\Saved\Logs     
P4\Game\Saved\Config\Windows\EditorPerProjectUserSettings.ini    
