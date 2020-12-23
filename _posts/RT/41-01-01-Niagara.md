---
title: Unreal Niagara Paradigm
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

- Niagara 16 params can send to material
- U can accse only depth buffer can read  
- Niagara can intreract with:  
 - Triangles  - u must point to spoecific mesh in query  
 - Phys Volumetric  -  
 - Scene Depth  - niestety: 2d, wiec nie ma info co jest za  
 - Distance Fields  -
- Use: Inheritance. You can always reparent  
- Niagara paradigms:
 - Modules - graph paradigm  
 - Emitters - stack paradigm  
 - Systems - stack and Sequencer timeline


# Parameters, Attributes


##  Name Space

| Name Space | R | W | Define | Share within |
|--- | --- | --- | --- | ---|
|`Engine` |  Y | N | Runtime for Niagara itself | Fundamental Attribs from unreal
|`User`| Y | N
|`Module Input`|Y|N|| Use inside of module for promoted Parameters
|`Output` |N|Y|transient ?| pay for calculate but not for adding it to emiter (parameter writes)
|`System` | Yes | System | Persisted f2f | System
|`Emitter` | Emitter, Particle  | Emitter  | Persisted f2f | Emitter instance / color ect...
|`Particles` | Particle | Particle |  Persisted f2f  |  Per-particle (@point)
|`Module` | Module | Module | Module | expose a module input to the System and Emitter Editor
|`Module Locals` ??? | Module | Module | not persist f2f, or between stages| Transient values.
|`Local`|||| Truly local for function ! Transient values.
|`Transient` | from any module |from any module | dont persist f2f and between stages

####  Name space modifiers:
  - module - insert module name as namespace so if u have x modules u have x different params
  - initial -  initial value of attribute (from eg in particle spawn)





----


# Script



## Script types


#### Module Script


<img  src="/src/ue/niagara/module.png" width="350" >  

You can see read/writes in finished module
- Module usage flags  
  - `Module` - particle , emitter, system scripts

#### Function Script

<img  src="/src/ue/niagara/script.png" width="350">

- Module usage flags
  - `Function` - fn to use in modules


#### Dynamic Input Script
Dynamic inputs have almost the same power as creating modules, but can be selected and dropped into the stack without actually creating new modules.

Dynamic inputs are built the same way modules are built.
extensibility for inheritance.
Instead of acting on a parameter map, dynamic inputs act on a value type.

<img  src="/src/ue/niagara/dynamic.png" width="350">  

- Module usage flags  
  - `Dynamic Input` - particle , emitter, system scripts

## Stages
#### System

- Module usage flags  
  - `System Spawn Script` - on system spawn
  - `System Update Script` -

#### Emitter
Do what system (optimal to set for multiple emitters) do or define.

- Module usage flags  
  - `Emitter Spawn Script` - once on spawn
  - `Emitter Update Script` - Tick

#### Particle

- Module usage flags  
  - `Particle Spawn Script` - on spawn
  - `Particle Update Script` - every frame
  - `Particle Event Script` - In response to event
  - `Particle Simulation Stage Script` -

#### Spawn
#### Update
----------





# Coordinates, Space &
Simulation, World, Local   
Mesh Tri Coordinates > Bary Coords  




#### Alignment
Sprite  - `SpriteAlignment` , `SpriteFaceing` , `SpriteRotation`    
Ribbon - `Particles.RibbonFaceing`, `RibbonLinkOrder`, `RibbonTwist`  
FlipBook - `SpriteUVScale`, `SpriteSubimageIndex`    
(in particles.)


# Collision
post soft collision    

# Physics

### Solve Dorces and velocity



force1


<img  src="/src/ue/niagara/force1.png">  
<img  src="/src/ue/niagara/force2.png">  

```
R:
`Engine.DelatTime`    
`Engine.Owner.Position`    
`Emitter Local Space`  
Masss Position  Previous.Position, Velocity, Previous.Velocity,
Transient.PhysicsDeltaTime
Transient.PhysicsDrag
Transient.PhysicsForce


W:
Position, Velocity
Presolve pos, velo
presolv physic forces
Transient  Physics Drag
Transient PhysiocForce

```

# Events
# Dynamic inputs


---


# HLSL
## Micro Expressions

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

- `Engine`. `DeltaTime` / `InverseDeltaTime` / `Owner.TimeSinceRendered` / `RealTime`    
- `Emitter.Age`  
- `System`. `Age`/ `TickCount`  
- `Time` -    
- `Particles.Age` -  
- `Particles.NormalizedAge` - 0-1  
- `Particles.Lifetime` -     
- `Module.DeltaTime`  
- `Module.LifeTime`  
- `Module.LoopParticlesLifetime`  

#### Translation

- `Particles.Position` - @P  
- `Particles.Scale`- @pscale (mesh)  
- `Particles.SpriteSize`- @pscale (sprite)   
- `Particles.RibbonWidth` - Ribbon width  
- `Particles.Owner.Position` `/Rotation` `/Scale`  - Owner Transform  

#### Physics

- `Particles.Mass`  
- `Particles.Velocity` - @v  
- `Particle.PreviousVelocity` - @v  
- `Engine.Owner.Velocity`  
- `Physics.Force`  
- `Physics.DeltaTime`  

#### Render

- `Particles.MaterialRandom` - Float  
- `Particles.Color` - Linear Color  
- `Particles.DynamicMaterialParameter` - Vector 4  
- `Particles.CameraOffset`  
- `Particles.UVScale`  
