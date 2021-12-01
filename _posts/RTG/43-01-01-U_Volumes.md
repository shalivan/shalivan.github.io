---
title: U Volume
description: Fluid Ninja, Clouds
categories:
 - PXL
tags:
- Unreal
- Rendering
- Real Time
- Game Dev
- Tech Art
permalink: /uvolume/
---



[pxl.ink Unreal Rendering Features](/ue_rendering_features/)   
[pxl.ink Unreal Light](/ulight/)  - Lighe and atmosphere

(blur is expensive, you need render targets)

------------
ray matching -
ray trace - array of features

# [Unreal Volume](https://docs.unrealengine.com/4.27/en-US/RenderingAndGraphics/Textures/VolumeTextures/CreatingVolumeTextures/)

Unreal CVars:    
`r.VolumetricFog.GridPixelSize 8`   
`r.VolumetricFog.GridSizeZ 128` - how many planes   - 32 -  128 Can trade distance for quality   
`r.VolumetricFog.TemporalReprojection 1` - Temporal smooth  
`r.VolumetricFog.Jitter 1`   
`r.VolumetricFog.HistoryWeight`   0.1 -flickering layers / 0.9 - ghosting  /== how smooth vs how responsive .6/.7 ?  




##### Volume material
Volume, Additive. Use texture: Vector Displacement map (RGBA8)
Volume Texture, Created from source texture






# [Volumetric Clouds](https://docs.unrealengine.com/4.27/en-US/BuildingWorlds/LightingAndShadows/VolumetricClouds/ )
When near will be replaced with volume fog




1. eneble volume plugin
2. Drag `Volumetric Cloud` from actors
3. In engine content: `VolumetricsContent/tools/CloudCompositing`
 - `BP_CloudMask_Object`  -  Scale and move away  its asset with single cloud. Have debug plane to create shape
 - `BP_CloudMask_Generator`  
4. Assign Material: `VolumetricsContent/Content/Sky/Materials`
5.



`r.VolumetricCloud.ReflectionRaySampleMaxCount`   
`r.VolumetricCloud.Shadow.ReflectionRaySampleMaxCount`  

`r.VolumetricCloud.SampleMinCount`  
`r.VolumetricCloud.DistanceToSampleMaxCount`  

### Cloud Component
Layer
- `Layer Bottom Altitude` -
- `Layer Height` -
- `Tracing Start Max Distance` -
- `Tracing Max Distance` -
- `Planet Radis` -

Cloud Tracing (balance visual nad perf) **!!!! Sample Count**
- `View Sample Count Scale` -  Clamped by: `r.VolumetricCloud.ViewRaySampleMaxCount` -  Sample Count
- `Refraction Sample Count scale` - rózowy ziomek miał na 1
- `Shadow View Sample Count` - !! perf
- `Shadow Refraction Sample Count scale` - rózowy ziomek miał na 1
- `Shadow Tracking Distance` - !! perf - range of shadow













## Material

Advanced output:
- `Phase G` -
- `Phase G2` -
- `Octaves` -
- `Multi Scattering Contribution` - How much Contribution from every octave
- `Multi Scattering Eccentricity`  - How much contribution will be removed
- `Multi Scattering Occlusion` - How much became isotropic


### Octaves
`Multiple Scattering Approximation Octaves` 1- for real time. -
- Fake Octaves: Contribution - high Eccentricity/Occlusion - low.


### Shadow
Volumetric Advanced Material Output expression to your material graph. With the node selected, toggle the Ray March Volume Shadow checkbox from the Details panel to switch between two types of shadowing.
- **Volume Ray Marching** uses secondary ray marching to get sharp colored shadows but is limited in distance that shadows can be traced due to the limited number of samples that can be used. Ray-marched shadows are good for ground to sky to space transitions even though they are more expensive.
- **Beer Shadow Maps (BSM)** use cascaded shadow maps to support far shadow distances for clouds and casting shadows on the ground. They are also faster to render, but are less accurate and lack volumetric self shadow color. Beer shadow maps are usually enough for clouds viewed from the ground.
For console platforms, such as Xbox One and PlayStation 4 or other systems using similar specifications, Beer shadow maps are recommended for cloud shadowing.

#### Light Interactions and Shadowing
#### Sky Lighting Cloud Ambient Occlusion
#### Sky Light Cloud Reflections Quality
#### Achieving Cinematic Quality
lot of Cvars

- `Light Shaft Occlusion `
- `Cast Shadow On Clouds`
- `Cast Shadow On Atmosphere`
- `Cloud Shadow map Resolution Scale` - - heavy

https://sergeneren.com/2019/08/21/creating-low-altitude-clouds/

https://gumroad.com/l/sFTCY/Clouds6m52fv



## Niagara



-------



# Fluid Ninja Live



### Setup

1. **Add custom trace channel**
    - `Edit > Project Sengs > Collisions > TraceChannels` (“TraceChannel” and “CollisionChannel” variables to “FluidTrace”)
    - "Set New trace channel" Name> `FluidTrace`, DefResponse> `Ignore` (all objects will be transparent for NinjaLive line tracers - except dedicated TraceMeshes in NinjaLiveComponent owners.), Trace Channel Index does not maer [if we have a trace channel:
    delete it
    add fluid trace
    and readd old trace channel]
    -  For fps shooter: it have hidden trace channel !!! named Projectiles invisible in options : CHECK: FAQ issue5
    Config/DefaultEngine.ini have  `+ default channel responses` should be game trace channel 1
2. **UV from Hit**
    - `Edit > ProjectSettings > Engine > Physics > Optimization` - help convert 3d data to 2d fluid spcae
3. Enable **Apex** Destructions
4. **Copy conternt** - `/Content/FluidNinjaLive` to the `/Content` folder of the target project. (And recompile NinjaLive.uasset)
5.  In the level editor, select any NinjaLive Actor on a level. Select NinjaLiveComponent. Check the “Live Compability” group: the top 3 input fields should be set to “FluidTrace”.


## Fluid Ninja (manula)


Inputs: Texture. Mat. Scene capture. geometry , (SM Bones sockets Phys Bodies Destructy)
``` for real time:  1-2 high res area fx and 3-6 character fx  - 1k is high res ```
6 buffers:

- Paint Buffer
- Divergence buffer - shockwawe like
- Pressure buffer - shockwawe like
- Velocity Buffer
- Density


The rendering pipeline uses 8 RenderTargets for a single simulaon container by default:
- 1 four-channel [ RGBA, for **CollisionPainter** ],
- 5 single channel [ R, for **Density** and **ScalarFields** ] and
- 2 bi-channel [ RG, for **VectorFields** ]
All set to 16 bit precision.  
(te set resoluon, bit depth, channel usage)


2d fluid sim
- using volume to track Pos and Vel > to Linetrace form cam to 2d
- display on cam facing plane


```
NinjaLive allocates memory mainly for RenderTargets. The rendering pipeline uses 8 RenderTargets for a single simulation container by default: 1 four-channel [ RGBA, for CollisionPainter ], 5 single channel [ R, for Density and ScalarFields ] and 2 bi-channel [ RG, for VectorFields ] - all set to 16 bit precision. The pipeline could be reconfigured many ways (resolution, bit depth, channel usage).

A 256x256 fluidsim container with default settings allocates 1664 Kilobytes of memory - this could be crunched or expanded, depending on the needs. Similarly: 512x512 area = 6656 Kbytes, 1024x1024 area = 26624 Kbytes, 2048x2048 area = 106496 Kbytes. Of course, the sim area could be non-square (eg. 128 x 512), mem consumption is changing accordingly.

Link1: See Help.uasset /Chart2 /RenderTargets for more details on possible RT configs.
Link2: Select any actor containing the sim component, and switch on "/Component Details /LiveDebug /ShowMemoryManagement" for dynamic, on-screen report on actual memory consumption of a given container.

```

![](/src/ue/ninja/ninjaloop.png)

- Red are processing mat
- Blue are outs to render target rrnder buffer

[Manual](https://drive.google.com/file/d/1I4dglPjeXLcNkSGxGok8sQCy59qgYcF9/edit)
[FAQ](https://drive.google.com/file/d/17oVPVEoaW6Y6YKNISr4S0uUJY4_Yx_FM/edit)

---


----

***TRACE LINES***

use custom line trace:   
- normaly projecting from camera to billboard plane .
for rotationali fixed sim contianers . !!!

`use custome trace position` on component. lvl 21

------


### RenderTarget
- this is what we call "Collision Painter".


The switch is located at NinjaLiveComponent Details /Live General /SimplePainterMode (at the very bottom)

## Parts



####  Ninja Live  (RED)  
Actor class object BP - "sim container" / "sim area".   Details: `Activation`, `Interaction`, `Debug`, `ComponentOverrides`.

Filter interactions, change material.

- `Activation volume` (usually much larger than the sim area): the proximity of any user defined agent could switch the sim component between wake/sleep states. For example: a player pawn is entering the 1000 meter range of a sim area, area wakes up, initializes, acquires pre-generated render targets from the memory manager, and gets ready to encounter the player.
-  `Interaction volume` (usually same size as the sim area): detecting overlapping / colliding objects and forwarding the spatial information + velocity to the sim component. Using the interaction volume, anything could interact with the simulation: Static- and Dynamic Meshes, Skeletal Meshes, Physics Bodies.


#### Ninja Live Component
Actor Component class "sim component" - more parameters (sim presets / materials) Details: `Activation`, `MemoryManagement`, `Performance`, `Compatibility`, `Debug`, `Generic`, `Interaction`, `BrushSettings`, `Raymarching`

#### Ninja Live Memory Pool Manager (BLUE)

#### Ninja Live Utilities (GREEN)
Can add to actor


#### Ninja Live Preset Manager (BLACK)


####  "Collision Painter"

Custom GUI, Memory Manager, and Interface Controller.


----------------

###### Material
Ray matching    
paralax occlusion





## Noise


A better strategy is stacking 3 layers of lower resolution 3D noises (128^3 for example) instead of 2 high resolution. And because the 3 layers have aggressively larger scale, they make up for low resolution:

|||instr pre level|lookup table|||
|-|-|-|-|-|-|
| Regular Texture
|Fast Gradient| 3d tex |~16 | 1 | High quality but not for bumps (baked to a volume texture) | Always tiles  
|Value | Computational | ~53-118 || Low quality but computational | yes
|Gradient |Tex Based |~61-74 | 8 | High Quality |always but <=128
| Samplex ||~77 |4  | High Quality | no
|Gradient |Computational|~80-143   | | High Quality  | yes
|Voronoi Q1 | 8 cells x20| ~160  |
|Voronoi Q2 | 16 cells x20| ~320 |
|Voronoi Q3  | 27 cells x20 | ~540 |
|Voronoi Q4  | 32 cells x20| ~640 |


Tiling Noise > Repeat Size  (Repeat Size matches the sampled size that you will be baking out.)


```
##### Low Level Settings  
to the host actor class
in your Actors, apply the directly specified

- **Actor Details** - Activation, Interaction, Debug, Component Overrides.
- **Component Details** - Activation, Memory Management, Performance, Combability, Debug, Generic, Interaction,
Brush Settings, Raymarching


##### Spawn  
- Ninja Live fluid sim Actors at your levels -
- or add Ninja Live fluid sim Component to your own object classes. To make fluid sim Component work properly
```

# Pseudo-Volume

## SDF
VDB SDF Sparse volume that define distance to surface. (How far away from edge (positives outside cause its distance )). Black at 0. so can see if in/out.
- `ray matching` Take big step and check how big next step should be. cause in fsd u know how far you are.




### VOLUME FAKE 6 point lightmap

Cool! You can also output these directional lightmaps automatically in ue4 using the Volumetrics plugin along with the motion vectors. I have been meaning to post about that.
https://twitter.com/Vuthric/status/1286796950214307840



pseudo volume smoke houdini   
https://viktorpramberg.com/smoke-lighting

------

https://www.youtube.com/watch?v=739NOjhLVnI, http://asher.gg/, Inside Unreal (Expand Your World With Volumetric Effects)](https://www.youtube.com/watch?v=R2RQm_Bu81I) - [forum thread ](https://forums.unrealengine.com/t/inside-unreal-expand-your-world-with-volumetric-effects/148624)
[volume fog layers nice](http://asher.gg/?p=2600)
