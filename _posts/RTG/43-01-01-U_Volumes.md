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

(blur is expensive, you need render targets)

------------

## SDF
VDB SDF Sparse volume that define distance to surface. (How far away from edge (positives outside cause its distance )). Black at 0. so can see if in/out.
- `ray matching` Take big step and check how big next step should be. cause in fsd u know how far you are.


# [Unreal Volume](https://docs.unrealengine.com/4.27/en-US/RenderingAndGraphics/Textures/VolumeTextures/CreatingVolumeTextures/)


Unreal CVars:    
`r.VolumetricFog.GridPixelSize 8`   
`r.VolumetricFog.GridSizeZ 128`   
`r.VolumetricFog.TemporalReprojection 1`   
`r.VolumetricFog.Jitter 1`   
`r.VolumetricFog.HistoryWeight`   

## Volume material
Volume, Additive. Use texture: VectoreDisplacementmap(RGBA8)


Volume Texture, Created from source texture !!!!!!!!



https://www.youtube.com/watch?v=739NOjhLVnI



```
Volume advanced output: volumetric adv input >>> extinction
- optimize ConservatriveDensity
```

[volume fog layers nice](http://asher.gg/?p=2600)

[ Inside Unreal (Expand Your World With Volumetric Effects)](https://www.youtube.com/watch?v=R2RQm_Bu81I) - [forum thread ](https://forums.unrealengine.com/t/inside-unreal-expand-your-world-with-volumetric-effects/148624)




https://docs.unrealengine.com/4.27/en-US/BuildingWorlds/LightingAndShadows/VolumetricClouds/    





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


## Niagara




## Volumetric Clouds
When near will be replaced with volume fog

##### Steps

[Unreal Docs](https://docs.unrealengine.com/en-US/BuildingWorlds/LightingAndShadows/VolumetricClouds/index.html)

1. eneble volume plugin
2. Drag `Volumetric Cloud` from actors
3. In engine content: `VolumetricsContent/tools/CloudCompositing`
 - `BP_CloudMask_Object`  -  Scale and move away  its asset with single cloud. Have debug plane to create shape 
 - `BP_CloudMask_Generator`  
4. Assign Material: `VolumetricsContent/Content/Sky/Materials`
5.


#### Material
Volumetric additive - three-dimensional volume texture that is ray-marched
- **Octaves** 1- for real time. Multiple scattering - light is almost never absorbed within the volume. Light that is not absorbed passes through the volume making the scattering effect very complex in the process. By tracing multiple octaves (or steps) of light transmittance in the volume material. The Volumetric Advanced Material Output expression enables you to set the number of octaves used along with the amount of multiple `scattering` contribution, `occlusion`, and `eccentricity` that happens.

```
**IN MATERIAL**
Contribution and low Occlusion values on the Volumetric Advanced Material expression in your cloud material to similar effect without impact to performance.
```


https://sergeneren.com/2019/08/21/creating-low-altitude-clouds/

https://gumroad.com/l/sFTCY/Clouds6m52fv


### Volume Ray Marching and Shadow Maps


 Ray Marched     
 Beer Shadow Maps (BSM)   

### Directional Light Interactions and Shadowing




-------



# Fluid Ninja Live

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



----

***TRACE LINES***

use custom line trace:   
- normaly projecting from camera to billboard plane .
for rotationali fixed sim contianers . !!!

`use custome trace position` on component. lvl 21

------


### Setup

1. **Add custom trace channel**
    - `Edit > Project Sengs > Collisions > TraceChannels` (“TraceChannel” and “CollisionChannel” variables to “FluidTrace”)
    - "Set New trace channel" Name> `FluidTrace`, DefResponse> `Ignore` (all objects will be transparent for NinjaLive line tracers - except dedicated TraceMeshes in NinjaLiveComponent owners.), Trace Channel Index does not maer [if we have a trace channel:
    delete it
    add fluid trace
    and readd old trace channel]
2. **UV from Hit**
    - `Edit > ProjectSettings > Engine > Physics > Optimization` - help convert 3d data to 2d fluid spcae
3. Enable **Apex** Destructions
4. **Copy conternt** - `/Content/FluidNinjaLive` to the `/Content` folder of the target project. (And recompile NinjaLive.uasset)
5.  In the level editor, select any NinjaLive Actor on a level. Select NinjaLiveComponent. Check the “Live Compability” group: the top 3 input fields should be set to “FluidTrace”.

----

6. !!! For fps shooter: it have hidden trace channel !!! named Projectiles invisible in options : CHECK: FAQ issue5
Config/DefaultEngine.ini have  `+ default channel responses` should be game trace channel 1






![](/src/ue/ninja/ninjaloop.png)

- Red are processing mat
- Blue are outs to render target rrnder buffer

[Manual](https://drive.google.com/file/d/1I4dglPjeXLcNkSGxGok8sQCy59qgYcF9/edit)
[FAQ](https://drive.google.com/file/d/17oVPVEoaW6Y6YKNISr4S0uUJY4_Yx_FM/edit)

---


## Parts



####  Ninja Live  (RED)  
Actor class object BP - "sim container" / "sim area".  

Filter interactions, change material.



#### Ninja Live Component
Actor Component class "sim component" - more parameters (sim presets / materials)
1. should be added to a "owner".

- Run autonomously (loading its default preset, creang RenderTargets for itself) or  connect to the interface Preset Manager and to the Memory Manager.
- sim component does _not_ have built in overlap detecon funconality - and for this reason, interacts only with predefined owner components (eg. Bones, Sockets, StacMeshComponents... ).

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

```
Actor class object, dedicated owner  
embedding "NinjaLiveComponent" and adding two important features to its core feature set:
1. **Acvaon volume** (usually much larger than the sim area): the proximity of any user
defined agent could switch the sim component between wake/sleep states.
2. **Interacon volume** (usually same size as the sim area): detecng overlapping / colliding
objects and forwarding the spatial informaon + velocity to the sim component. Using the
interacon volume, anything could interact with the simulaon (eg. Stac/Dynamic Meshes,
SkeletalMeshes, PhysicsBodies, Destrucbles)
```
# Pseudo-Volume


### VOLUME FAKE 6 point lightmap

Cool! You can also output these directional lightmaps automatically in ue4 using the Volumetrics plugin along with the motion vectors. I have been meaning to post about that.
https://twitter.com/Vuthric/status/1286796950214307840



pseudo volume smoke houdini   
https://viktorpramberg.com/smoke-lighting

------


http://asher.gg/
