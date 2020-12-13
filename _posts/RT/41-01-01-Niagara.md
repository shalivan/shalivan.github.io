---
title: Unreal Niagara Syntax
description: Unreal Niagara.
categories:
 - RT
tags:
- Unreal
- VFX
- Rendering
- Real Time
- HLSL
- Game Dev
- Niagara
permalink: /niagara/
---

Niagara 16 params can send to material
U can accse only depth buffer can read  

Niagara can intreract with:  
- Triangles  - u must point to spoecific mesh in query  
- Phys Volumetric  
- Scene Depth  - niestety: 2d, wiec nie ma info co jest za  
- Distance Fields  - !





# Parameters, Attributes


##  Name Space

| Name Space | R | W | Define | Share within |
|--- | --- | --- | --- | ---|
|`System` | Yes | System | Persisted f2f | System
|`Emitter` | Emitter / Particle  | Emitter  | Persisted f2f | Emitter instance / color ect...
|`Particles` | Particle | Particle |  Persisted f2f  |  Per-particle (@point)
|`Engine` |  Y | N | Runtime for Niagara itself | Fundamental Attribs from unreal
|`Module` | Module | Module | Module | expose a module input to the System and Emitter Editor
|`Module Locals` | Module | Module | not persist f2f, or between stages| Transient values.
|User
|INPUT.|Y||| Use inside of module for promoted Parameters
|LOCAL.|||| Truly local for function !
Output ||Y|| pay for calculate but not for adding it to emiter (parameter writes)

name space modifiers:

- module - insert module name as namespace so if u have x modules u have x different params
- initial -  initial value of attribute (from eg in particle spawn)





----


# Script



## Script types




##### Module Script


<img align="right" src="/src/ue/niagara/module.png" width="250" >  

-  you can see read/writes in finished module


##### Function Script

<img align="right" src="/src/ue/niagara/script.png" width="250">
.


##### Dynamic Input Script

<img align="right" src="/src/ue/niagara/dynamic.png" width="250">

.





## Module usage flags

- `Function` - fn to use in modules
- `Module` - particle , emitter, system scripts
- `Dynamic Input` - particle , emitter, system scripts
- `Particle Spawn Script` - on spawn
- `Particle Update Script` - every frame
- `Particle Event Script` - In response to event
- `Particle Simulation Stage Script` -
- `Emitter Spawn Script` - once on spawn
- `Emitter Update Script` - Tick
- `System Spawn Script` - on system spawn
- `System Update Script` -


`System state` -   
`Emitter` - do what system (optimal to set for multiple emitters) do or define.   
`Particle` -   




----------





# Coordinates, Space & Phisics
Simulation, World, Local   
Mesh Tri Coordinates > Bary Coords  

#### Alignment
Sprite  - `SpriteAlignment` , `SpriteFaceing` , `SpriteRotation`    
Ribbon - `Particles.RibbonFaceing`, `RibbonLinkOrder`, `RibbonTwist`  
FlipBook - `SpriteUVScale`, `SpriteSubimageIndex`    
(in particles.)






---


# HLSL
## Expressions

- `/* Custom HLSL! */`  
- `sin(Emitter.Age *0.3) /2 +0.5` - 0-1 time x 0.3
- `cross(Particles.RandomVector, float3(0,8,0))` - cross   
- `rand(1.5f) + 2.2f` - random   
- `length(Particles.Position - Emitter.InitialPosition)` - length   
- `saturate()` - fast clamp 0-1  
- `frac(Emitter.Age *0.3)` - 0-1 loop in time x 0.3   
- `float3(0.0f, 0.0f, Emitter.ZOffset) *0.2f)` - Add Z  
- `Particles.Position + float3(0, 0, (sin(Engine.Time) * 0.3f ))` - Add Z sin to actual pos    

.
- `float3(Particles.UV,0)` - make vector from uvs  
- `(Particles.Position-Particles.PreviousPosition)/Engine.DeltaTime` - render velocity

.
- `Emitter.InitialPosition + Particles.RandomVector`  
- `Particles.NormalizedAge`  
- `Particles.Position - Emitter.InitialPosition`  

.
- `(1.0f-(abs((Particles.RibbonLinkOrder)-0.5f)*2.0f))*50.0f` - Ribbon radious  

###  Conditioning  

`Particles.NormalizedAge<0.3 ? float4(1,0.1,0.1,1):Particles.NormalizedAge<0.5 ? float4(1,1,1,1):float4(1,1,1,1)`

```hlsl
Particles.Position.z > Emitter.InitialPosition.z - Emitter.ZOffset
  ? Particles.Position
  : float3(Particles.Position.x, Particles.Position.y, Emitter.InitialPosition.z -Emitter.ZOffset)
```






## Map Attributes

#### Time:

`Engine`. `DeltaTime` / `InverseDeltaTime` / `Owner.TimeSinceRendered` / `RealTime`    
`Emitter.Age`  
`System`. `Age`/ `TickCount`  
`Time` -    
`Particles.Age` -  
`Particles.NormalizedAge` - 0-1  
`Particles.Lifetime` -     
`Module.DeltaTime`  
`Module.LifeTime`  
`Module.LoopParticlesLifetime`  

#### Translation

`Particles.Position` - @P  
`Particles.Scale`- @pscale (mesh)  
`Particles.SpriteSize`- @pscale (sprite)   
`Particles.RibbonWidth` - Ribbon width  

`Particles.Owner.Position` `/Rotation` `/Scale`  - Owner Transform  

#### Physics

`Particles.Mass`  
`Particles.Velocity` - @v  
`Particle.PreviousVelocity` - @v  
`Engine.Owner.Velocity`  
`Physics.Force`  
`Physics.DeltaTime`  

#### Render

`Particles.MaterialRandom` - Float  
`Particles.Color` - Linear Color  
`Particles.DynamicMaterialParameter` - Vector 4  
`Particles.CameraOffset`  
`Particles.UVScale`  
