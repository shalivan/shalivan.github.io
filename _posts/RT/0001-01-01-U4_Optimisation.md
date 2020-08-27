---
title: Unreal Optimization
description: .
categories:
 - RT
tags:
- Rendering 
- Real Time
- Unreal
- Design
- Games
- Tech
---

check:
- precise uv
- colision setup
- affect navmesh
- shadow distances and turn off for small

# Render pipeline  



##### Game thread
game logic and transforms movement spawning physics
ticks !!!

##### Draw thread
Frustrum culling  - in cam    
hardware occludion from  scene buffers   
Too many obj canm hit performance

##### GPU thread


---
Before render: CPU game context   
Before render: CPU (mostly) what to render  
Render: GPU  render pixel on screen


1) vertex shader   
2) tessalation   
3) geometry shader  
4) pixel shader  

#### Passes    

| pass |  | dependences:
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
`Base pass` G-buffers (compo) | Fog, Dbuff-decals| Trixcount + Shader complexity, num of mats.  
`Translucency` | | Area of translucy, overdraw, (in FSR: light count)  
`PartilceSimulation / Injection` | Scene depth collisions.| num of particles  
`PostProcessing` | Temporal, Exposure ..| PP features, and  blendables   
`RenderVelocities` | |Num of moving objects and tri-count!
`ScreenSpaceReflectiion` ||  (cost increaase with rough),

---
## Light and shacows  


# Botlenecks
1. Check if time of frame is bigger from CPU or GPU. (ause threads must wait one for another)


shader complexity on *Opacity* -    
*Draw Calls* - command send     
overshading  *Quad Overdraw* - small or thin triangles (because it perform operation in bigger tile)  (watch for tessalarion)    
*Shadow Casting* -    
*Splits on uv's* cound on vertex count - (memory and disk space)    
*Too many texture samples* - use bandwith (compression and texture packing to channels help)   
affect navmesh   
tick  

---

# Debug

####  Prepear for Drbug

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

## Developer Tools

##### Show commands


```
ShowFlag.StaticMeshes
ShowFlag.SkeletalMeshes
ShowFlag.Particles
ShowFlag.Lighting
ShowFlag.Translucency
ShowFlag.ReflectionEnvironment
ShowFlag.InstancedStaticMeshes
show landscape
show fog
show MotionBlur
```
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


##### Stat unit

Frame (FPS)  
Game - CPU code
Draw - CPU graphic   
GPU - GPU usage  

```
Stat fps
StartFPSChart / StopFPSChart
Stat Unit
Stat UnitGraph
```


##### CPU

```
stat game -- generaly how things rticks on CPU
```

##### GPU
`Ctrl` + `Shift` + `,` -  GPU Visualiser window (Single frame on gpu)  you can dump it to log  
```
ProfileGPU
```

GPU - Small table     If not working (https://youtu.be/SXLYy6D1y80?t=603).       


```
Stat GPU

```
RHI - memory and so on...   affected by editor!    

```
Stat RHI
r.rhicmdbypass 1
r.rhithread.enable 0
r.showmaterialdrawevents -1
```



##### Stats
SceneRendering - Call count and ms table with: *Draw calls*, *Triangle count*, *Light count*, *Translucency*
```   
Stat SceneRendering    
Stat SceneUpdate  
Stat SceneMemory   
```



##### Shadows and reflections
Shadow quality (`sg.ShadowQuality 0..4`).     
Screen space reflections: Quality `r.SS.MaxRoughness 0.0..1.0` `e.SSR.Quality 0..4`    


##### Textures used

Window > Statistics - Textures used   

#####  Session Frontend
>*CPU* + *GPU* same time, (you can load files from sessions)  
Window > DevTools > `Session Frontend`     

---
#### Unreal Insights
Standalone profiling system

---

#### Intel Frame Analyzer   

1. You need to package game
2. Run Graphic monitor andd click analyse application
3. Enable in U4: `ToggleDrawEvents`
4. `Ctrl` + `Shift` + `C` - to capture
5. Enable in U4: `ToggleDrawEvents`

https://software.intel.com/en-us/gpa/graphics-frame-analyzer

---

#### Nsight graphic

- frame debuger
- frame profile (similar but more like profiling than debuging)
- generate C++ capture - collect frames   
- gpu trace  


`Timeline` API calls as events   
`Resource view`.: textures and bufffers in scene (tak buttobn to find)   
`API inspector` stages : input assembler , VS, PS  
`API statistic` !!! view. > shaders wiev by comlexity and times      
`Shader view`: ??? Linked ptograms view   
`Range Profiler`: time ing using low lvl metrics (bottleneck) hi lvl overview.   



https://developer.nvidia.com/gameworksdownload    

---

## Textures

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

---

## UE4 CVars:  

http://www.kosmokleaner.de/ownsoft/UE4CVarBrowser.html // list    






### Notes:
------  
>The only way to group meshes into one draw call is by using instanced meshes. Meshes using the same material/instance will still take one draw call each. However, they are drawn in an order that is grouped by material/instance, to reduce the number of render state changes, kinda like this:
- 3 meshes using the same material: set shader, draw mesh #1, draw mesh #2, draw mesh #3
- 3 meshes using a different material each: set shader #1, draw mesh #1, set shader #2, draw mesh #2, set shader #3, draw mesh #3
From Eric Ketchum https://answers.unrealengine.com/questions/127435/using-instanced-meshes-doesnt-reduce-draw-calls.html:

>Instanced meshes will reduce the draw call overhead on the CPU but will not reduce the GPU cost. In fact the GPU time can increase when using instancing. Allow me to get a little technical for a moment: This process has to do with the limitations of the CPU vs. GPU and how the API (OpenGL or DirectX) tries to maximize this limitation through batching. Instancing being a special case of batching. With a scene rendered with many small or simple objects each with only a few triangles, the performance is entirely CPU-bound by the API; the GPU has no ability to increase it. More precisely, "the processing time on the CPU for the draw call is greater than the amount of time the GPU takes to actually draw the mesh, so the GPU is starved." [Moeller, Real Time Rendering, 708]. So Batching attempts to allow the CPU to combine a number of objects into a single API call. In the case of Instancing it is the one mesh and the number of times you are drawing with a separate data structure for holding information about each separate mesh.

From a Rendering Engineerer:
>"On meshes and material IDs, let me present a hypothetical situation to try to explain the situation more clearly. Let's say you have a mesh that has three materials: wood, chrome, and leather. Now let's say you place 100 of these meshes in your level. Ignoring other passes (shadow, depth only), this will result in 300 draw calls: one per-ID, per-instance. You can see this by looking at the section counts in the primitive stats window.

>First thing to keep in mind: some draw calls are more expensive than others. The renderer sorts by material. So in this hypothetical scene we will draw the 100 wood elements first, the 100 chrome elements next, and the 100 leather elements last. Once we draw a wood element, the cost of drawing another wood element is not so high because we are rendering using the same shader and with mostly the same textures. But once we switch materials to draw the chrome we incur a high cost. That's why the renderer sorts by material.

>Compare that situation to another scene where you have the same mesh instanced 100 times but each mesh has its own unique material. The scene is still 300 draw calls but the renderer incurs the material switch cost for every draw call. Instancing a mesh provides performance benefits even if the total number of draw calls does not reflect that"

>To really see the performance boost in using Instances bring up the Stat UNIT and watch the DRAW versus GPU (CPU vGPU) and notice when you instance a mesh the CPU time remains fairly consistent depending on the additional information you are wanting to pass to each instance, while the GPU will increase. All of these numbers are still dependent on the size of your mesh and the type of material setup and the ultimate limitations of your CPU and GPU.

>Check - Garbage Collector times in options  

-------------
Tech Art Aid  
https://youtu.be/UZH4vZ0NDAw  


P4\Game\Saved\Logs     
P4\Game\Saved\Config\Windows\EditorPerProjectUserSettings.ini    
