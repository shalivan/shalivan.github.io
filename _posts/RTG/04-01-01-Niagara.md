---
title: Niagara
description: Paradigm
categories:
 - PXL
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




### Interaction spaces
  - **Triangles**  - u must point to specific mesh in query  
  - **Phys Volumetric**  -  
  - **Scene Depth**  - 2d buffer, don't penetrate behind first depth  
  - **Distance Fields**  -

### Paradigm  
  - **Modules** - graph paradigm  
  - **Emitters** - stack paradigm  
  - **Systems** - stack and Sequencer timeline

### Calculation stages   

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


----


# Scripts

## Dynamic Input scripts
Dynamic Input scripts by Usage flag:

#### Module
Use as module in particle emitter.      
Read/Writes parameters will appear in module.      
Can be used with: `particle` , `emitter`, `system scripts`    
IN: `Map` OUT: `Module`   

#### Dynamic Input
Use as expression in parameter value. Almost the same as creating modules, but can be selected and dropped into the stack without actually creating new modules.  (extensibility for inheritance. Instead of acting on a parameter map, dynamic inputs act).   
Can be used with: `particle` , `emitter`, `system scripts`    
IN: `Map` OUT: `Module`      

#### Function
Function to use inside module.     
IN: `Input` OUT: `Function`      

---





# Attributes


##  Name Space






| Name Space | R | W | Define | Share within |
|--- | --- | --- | --- | ---|
|PARTICLES. | Particle | Particle |  Persisted f2f | Loaded as  payload. Per-particle (@point)
|INPUT.|Y|N|| Module input. Use inside of module for promoted Parameters
|Module | Module | Module | Module | expose a module input to the System and Emitter Editor
|LOCAL. | Module | Module | Not persist f2f | Transient values.  Truly local for function ! Transient values.
|EMITTER. | Emitter, Particle  | Emitter  | Persisted f2f  | Emitter instance / color ect...
|SYSTEM. | Y | System | Persisted f2f  | System
|ENGINE. |  Y | N | Runtime for Niagara itself | Fundamental Attribs from unreal
|USER. | Y | N
|OUTPUT. |N (An output in Particle Spawn cannot be accessed in Particle Update) |Y| Not persist f2f  | pay for calculate but not for adding it to emitter (parameter writes)  useful helpers included in the modules which are not yet written to the particle payload, but are available for use.
|TRANSIENT. | from any module |from any module | Not persist f2f  | Local only to a given stack context (like Particle Update)

Name space modifiers:

| Name Space | R |
|--- | --- |
.MODULE. | insert module name as namespace so if u have x modules u have x different params
.INITIAL. |  initial value of attribute (from eg in particle spawn)

Particle attributes vs Transient outputs:
- **Transient** - Not persist f2f and between stages, **not written to the payload**, which means they don't cross stack boundaries  and are recalculated from scratch every frame  
- **Particles** -  Persisted f2f (memory and performance cost)



# Orientation


## Mesh

#### Set Orientation
Inexpensive constant rotation rate. (rotational drag, an option on the drag module) has no effect.
set: `Particles.MeshOrientation`


`Update Mesh Orientation` Module -  
`Orient Mesh To Vector` Module - Can be after solve forcces  





#### Rotational Force
Paradigm which factors mesh scale, mass, density, and drag into the model.  larger meshes have a tendency to resist rotation  due to their mass, and rotational drag can be used to control the acceleration/deceleration.  `Transient.PhysicsRotationalForce`


`"Mesh Rotation Force"` Module in Particle Update -
`Solve Rotational Forces and Velocity` Solver -    
`Drag`   


Need "Initial Model Dimensions" and mass > "Calculate Size by Mass"





#### Rotational Velocity / Drag

Rotational Forces accumulate into a `Particles.RotationalVelocity` variable and persist from frame to frame. Here we give the particles an initial "kick", by applying a Rotational Force and then applying those forces to the Rotational Velocity. We use this method as it factors mass into the initial rotational velocity.

This then gets solved by the solver in update, and rotational  drag eventually slows the particles down.

If you want the initial "kick" to not factor in mass, you can use an "Add Rotational Velocity Module" to directy set a rotation speed.


`Mesh Rotation Force` Module in Particle Spawn  -
`Apply Initial Forces` Module

`Inheret Velocity` - In Update,  magnify velocity of root (have limit)
`Static Mesh Velocity`  with `sample static mesh` - will have velo of mesh Normal
`Vortex velocity`


## Sprite


#### Orient Mesh along vector

####  Alignment

` Particles.SpriteFaceing` - is the vector variable  which controls which direction a particle faces  

`SpriteAlignment`  
`SpriteRotation`      


`SpriteUVScale`  
`SpriteSubimageIndex`      
(in particles.)

---

# Velocity

[Add Velocity] / [Add Velocity from point] / [Add Velocity in cone]- in particle spawn  (ever frame if in update)



# Coordinates & Space
Simulation, World, Local   
Mesh Tri Coordinates > Bary Coords  

---

# Physics


## Solve Forces and velocity

#### Write to intrinsic properties
Choose whether or not to write to intrinsic properties


```
ENGINE.DelatTime    
ENGINE.OWNER.Position    
Emitter Local Space  
Masss Position  Previous.Position, Velocity, Previous.Velocity,
TRANSIENT.PhysicsDeltaTime
TRANSIENT.PhysicsDrag
TRANSIENT.PhysicsForce
```

- (time) Fractional updates based on collision equations
-  (Init copy:)
  - `TRANSIENT.PhysicsForce` > `LOCAL.PhysicsForce`, `OUTPUT.MODULE.IncomingPhysicsForce`
  - `PARTICLE.Velocity` >  `OUTPUT.MODULE.Velocity`
  - `PARTICLE.Mass` > `LOCAL` /
  - `PARTICLE.Position` > `OUTPUT.MODULE.Position`
-  copy to > `PARTICLES.PRESOLVE`
- (Apply mass  to phys)
  - (1/`LOCAL.Mass`) * `LOCAL.PhysicsForce` > `LOCAL.PhysicsForce`
- (Apply forces to velo) (copy drag irrespective of Mass)
  - `OUTPUT.MODULE.Velocity` * `LOCAL.DelatTime` *  `LOCAL.PhysicsForce` > `OUTPUT.MODULE.Velocity`
  - `TRANSIENT.PhysicsDrag` >  `OUTPUT.MODULE.IncomingPhys`
- limit velko and acc
-  (Apply velo to pos)
  - `OUTPUT.MODULE.Velocity` * `LOCAL.DelatTime`* `OUTPUT.MODULE.Position`  >  `OUTPUT.MODULE.Position`  
-  [T] copy
 - `OUTPUT.MODULE.Position`/ > `PARTICLE.Position`/
 - `Velocity` >  `Velocity`
-  If Forces/Drag have been converted to Velocity, zero out
 - [T] 0 > `TRANSIENT.PhysicsForce` / `PhysicsDrag`

```
PARTICLE.Position
PARTICLE.Velocity
Presolve pos, velo
Presolve physic forces
TRANSIENT.PhysicsDrag
TRANSIENT.PhysicsForce
```

## Point Attraction Force
```
EMITTER.LocalSpace
PARTICLE.Position
PARTICLE.Velocity
TRANSIENT.PhysicsForce
```
...

```
TRANSIENT.PhysicsForce
```

## Point Force

```
EMITTER.LocalSpace
PARTICLE.Position
TRANSIENT.PhysicsForce
```
...

```
OUTPUT.POINTFORCE.Withinrange
OUTPUT.POINTFORCE.NormalizedFallof
OUTPUT.POINTFORCE.NormalizedDistance
TRANSIENT.PhysicsForce
```


## Limit Force


## Drag



## Acceleration, Avoid, Gravity, Line Attraction, Linear, Mesh Rot, Spring, Vector Noise, Vortex, Wind


## Houdini Combine Forces


```
.
```

- Copy
 - `PARTICLES.NiagaraForce` > `TRANSIENT.NiagaraForce`
 - 0 > `TRANSIENT.PhysicsForce`
- Lerp
 - Lerp `PARTICLES.Velocity` or (`PARTICLES.HOUDINI.Velocity` or `PARTICLES.HOUDINI.GoalPosition`) > `PARTICLES.Velocity`
- Apply
 - `PARTICLES.NiagaraForce` > `TRANSIENT.PhysicsForce`

```
PARTICLES.NiagaraForcesMultiplayer
PARTICLES.Velocity
TRANSIENT.PhysicsForce
```



# Render




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




Tips
  - Niagara 16 params can send to material
  - U can access only depth buffer can read  
  - Use: Inheritance. You can always reparent  
