---
title:  UE Volume
description: Fluid Ninja, Clouds
categories:
 - RT
tags:
- Unreal
- Rendering
- Real Time
- Game Dev
- Tech Art
permalink: /ue_volume/
---

# Fluid Ninja

# Fluid Ninja Live


The rendering pipeline uses 8 RenderTargets for a single simulaon container by default: 1 four-channel [ RGBA, for **CollisionPainter** ], 5 single channel [ R, for **Density** and **ScalarFields** ] and 2 bi-channel [ RG, for **VectorFields** ] - all set to 16 bit precision.  
(te set resoluon, bit depth, channel usage)

## Merge

#### Project Setings
 - ##### Add custom trace channel
    - /Edit /Project Sengs /Collisions /Trace Channels
    - "Set New trace channel" Name> **FluidTrace**, DefResponse> **Ignore** (all objects will be transparent for NinjaLive line tracers - except dedicated TraceMeshes in NinjaLiveComponent owners.), Trace Channel Index does not maer
 - ##### UV from Hit
    - /Edit /Project Sengs /Engine /Physics /Opmizaon


#### Copy files & Compile
   - /Content/FluidNinjaLive to the /Content folder of the target project
   - /Content/FluidNinjaLive/NinjaLive.uasset Compile”, then “Save”.
   - /Content/FluidNinjaLive/NinjaLive.uasset (“TraceChannel” and “CollisionChannel” variables to “FluidTrace”).  “Compile”, then “Save”
   - In the level editor, select any NinjaLive Actor on a level. Select NinjaLiveComponent
(see HOW). Check the “Live Compability” group: the top 3 input fields should be set to
“FluidTrace”.


#### Spawn  
- NinjaLive fluidsim Actors at your levels -
- or add NinjaLive fluidsim Component to your own object classes. To make fluidsim Component work properly



#### Low Level Setings  
to the host actor class
in your Actors, apply the directly specified

- **Actor Details** - Acvaon, Interacon, Debug, ComponentOverrides.
- **Component Details** - Acvaon, MemoryManagement, Performance, Compability, Debug, Generic, Interacon,
BrushSengs, Raymarching



## Parts

#### NinjaLiveComponent "sim component"
ActorComponent class object that should be added to a "owner".

Run autonomously (loading its default preset, creang RenderTargets for itself) or  connect to the interface Preset Manager and to the Memory Manager.
- sim component does _not_ have built in overlap detecon funconality - and for this reason, interacts only with predefined owner components (eg. Bones, Sockets, StacMeshComponents... ).

/Content/FluidNinjaLive.

####  NinjaLive  "sim container" / "sim area"  (RED)  
Actor class object, dedicated owner  
embedding "NinjaLiveComponent" and adding two important features to its core feature set:
1. **Acvaon volume** (usually much larger than the sim area): the proximity of any user
defined agent could switch the sim component between wake/sleep states.
2. **Interacon volume** (usually same size as the sim area): detecng overlapping / colliding
objects and forwarding the spatial informaon + velocity to the sim component. Using the
interacon volume, anything could interact with the simulaon (eg. Stac/Dynamic Meshes,
SkeletalMeshes, PhysicsBodies, Destrucbles)

/Content/FluidNinjaLive



#### NinjaLive_MemoryPoolManager (BLUE)


#### NinjaLive_Utilities  (GREEN)
 Utilities

#### NinjaLive_PresetManager

 /Content/FluidNinjaLive/NinjaLive_PresetManager


####  "Collision Painter"


 custom GUI,Memory Manager, and Interface Controller.

------------



# Unreal Volume



`r.VolumetricFog.GridPixelSize 8`   
`r.VolumetricFog.GridSizeZ 128`   
`r.VolumetricFog.TemporalReprojection 1`   
`r.VolumetricFog.Jitter 1`   
`r.VolumetricFog.HistoryWeight`   

## Volume material
Volume, Additive



Volume texture: VectoreDisplacementmap(RGBA8)

Volume advanced output: volumetric adv input >>> extinction
- optimize vonservatriveDensity



[ Inside Unreal (Expand Your World With Volumetric Effects)](https://www.youtube.com/watch?v=R2RQm_Bu81I) - [forum thread ](https://forums.unrealengine.com/t/inside-unreal-expand-your-world-with-volumetric-effects/148624)



http://asher.gg/

 VOLUME GFAKE 6 point lightmap 

Cool! You can also output these directional lightmaps automatically in ue4 using the Volumetrics plugin along with the motion vectors. I have been meaning to post about that.
https://twitter.com/Vuthric/status/1286796950214307840

------


## Niagara




## Volumetric Clouds

When you near could be repleaced with vol fog

[Unreal Docs](https://docs.unrealengine.com/en-US/BuildingWorlds/LightingAndShadows/VolumetricClouds/index.html)

three-dimensional volume texture that is ray-marched
This effect of light is called multiple scattering, and it is what defines the distinct appearance of clouds. In a cloud, the droplets that make up the cloud usually lead to an albedo that is close to a value of 1, meaning that light is almost never absorbed within the volume. Light that is not absorbed passes through the volume making the scattering effect very complex in the process.

OCTAVES  (for games 1 )
by tracing multiple octaves (or steps) of light transmittance in the volume material. The Volumetric Advanced Material Output expression enables you to set the number of octaves used along with the amount of multiple scattering contribution, occlusion, and eccentricity that happens.

IN MATERIAL
Contribution and low Occlusion values on the Volumetric Advanced Material expression in your cloud material to similar effect without impact to performance.



https://sergeneren.com/2019/08/21/creating-low-altitude-clouds/

https://gumroad.com/l/sFTCY/Clouds6m52fv


### Volume Ray Marching and Shadow Maps


 Ray Marched     
 Beer Shadow Maps (BSM)   

### Directional Light Interactions and Shadowing
