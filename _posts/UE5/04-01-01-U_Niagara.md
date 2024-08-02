---
title: Niagara
description: Paradigm
categories:
  - PXL
tags:
  - Unreal
  - VFX
  - Rendering
  - HLSL
  - Niagara
  - RealTime
  - GameDev
  - NodesGraph
permalink: /niagara/
aliases:
  - niagara
---
> Obsidian: [[04-01-01-U_FluidNinja| Fluid Ninja]] [[16-01-01-VFX|VFX]]



https://youtu.be/vOSXl7-2vd0
https://80.lv/articles/drawing-locations-to-a-render-target-in-unreal-engine-5-1/
https://youtu.be/3fW5xjiDm-A


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
Functions to use inside module.     
IN: `Input` OUT: `Output`      



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

# Velocity

[Add Velocity] / [Add Velocity from point] / [Add Velocity in cone]- in particle spawn  (ever frame if in update)



# Coordinates & Space
Simulation, World, Local   
Mesh Tri Coordinates > Bary Coords  


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




# Interfaces 

`The Kill Particles` module at spawn - acts as a form of "Rejection Sampling". We sample the texture and then kill the newly spawned particles on their first frame if the sampled texture alpha equals 0.

Because Interpolated Spawn is unchecked in the emitter properties, newly spawned particles do not run both their spawn and update scripts on the frame they were born, making this technique quite inexpensive.


`Particles.VisibilityTag` - Render Visibility - can change renderer dynamicly


## Ribbons

```
`NiagaraRibbonRendererProperties` module.  


##### Ribbon Render

Ribbon - `Particles.RibbonFaceing`, `RibbonLinkOrder`, `RibbonTwist`  


##### more ribbons

`SetRibbonIDByExecOrder` - get the particles execution index, make a Niagara ID and assign the execution index to the ID index, and then set `Particles.RibbonID` in the Map with our new ID.

-

`Particles.RibbonLinkOrder` is the variable which determines how particles of a given `RibbonID` link up with each other.

The Spawn Beam module establishes the order based on the new particles as they are spawned in a burst, and assigns a new unique `RibbonID` to each new set of particles so they stay as separate beams instead of one large interconnected ribbon between all particles in the emitter.

From there, normal particle simulation takes over, and because the ribbon ID and link order are not changing from frame to frame, the beams stay stable.

```

---
```
## Events
push  
Will be 2.0! cause of fixed payloads (could be arbitrary )  
```

## Location Event  
CPU  

### Leader emitter
###### Particle update
`Generate Location Event`


### Follower emitter

###### Event Handler
`Event Handler Properties` - Event Handler  
`Recive Locaation Event` - Event Handler


Which runs after the event is received. This needs to include a "Receive X Event" Module  to handle the event, and then other modules can be placed inside to have additional effect on the particles which receive events, for example an additional location module to provide an additional offset from the received event position.


## Attribute Reader
GPU  
`Spawn Particles From Other Emitter` and `Sample Particles From Other Emitter` modules which utilize the Particle Attribute Reader. Listen to other emitter (events not push, but pull directly) - bats, flock, swarming bugs, Flight Orientation


`Get by ID` - niagara unique particle qttribute     
`Get Vector by index` -- get attribute (like Color) by Index (order particle responce)     
`Get Spawned ID at Index` > `Get Vector by ID`  

- can use it on yourself every particle can ask of neighbour pos (phys line)
- can integrate with otherforces (like cable component in niagara)
 and

`newParticleAtributeReader`   

## Constraints


## Vector Fields
.fga  
add an Acceleration Force module under our Sample Vector Field, and then bind the value `SampleVectorField.SampledVector` to the Acceleration value
`VectorFieldSize`

http://andy.moonbase.net/archives/1499

## Distance Field
Sample Distance Field


## Collision



### CPU
Expensive, should be used sparingly.

- can optionally generate events using the "Generate Event"
(Receive collision event)

`Collision`- Ray Traced
`Generate Collision Event `   
### GPU  
Direction and D-buffer sampling

- can sample the scene depth, or the global distance field.

`Collision`- GPU Distance field / GPU Depth Buffer. Can be used at the end of particle update (before solvere) or special collision module.

##### Collision module  

- Place a Solve Forces and Velocity module at the end of particle update. Ensure that the "Write to Presolve Parameters" checkbox is set to true.

- Place a Collision module in a final simulation stage.

The simulation stage should operate on "particles" and perform 1 iteration.

- A second "Solve Forces and Velocity" module should be placed immediately after the collision module. That module's "Write to Intrinsic Properties" Bool should be driven by [Transient]CollisionValid.

## Neighbor Grid 2D GPU
Sampling image -  value to sample the texture as if it were a UV.

`Spawn Particles In Grid` - Emiter up   
`Grid Location`  
`Sample Texture`  

## Neighbor Grid 3D
special position cash when a lot of particle need global comunication



## PBD


## Mesh Reproduction Static

Set position from static mesh   
Set UV by Dynamic material  


## Mesh Reproduction Skeletal
`initialize mesh reproduction`


#### Particle Update
`update mesh reproduction`

#### Material
- add Niagara mesh reproduce uv's



---



## Houdini Point Clouds


### Houdini

#### Niagara ROP

Export pointcloud as: **.hjson**, **.hbjson** - bin quicker    
 - `i@id`  per particle  same for one particle   
 - `f@time` of pop-up / arrival time // just normalize time before export!  check length from a to b and set time  
 - `@type` group   
 - `@life` Life set for first point
 - `i@dead = 1`  
 -  `NID` - niagara id attrib CREATED BY SAMPLE MODULES  
no `Force` ?

hardcoded attributes -


### Unreal

### Emitter Spawn
`InitHoudiniPointCache`  - Initialize  


<img align="right" src="/src/ue/niagara/houdiniinit.png">

.
```
W:  
emitter.Houdini.LastSpawnTime - 0.0  
emitter.Houdini.LastSpawnTimeRequest - 0.0  
emitter.Houdini.LastSpawnedPointID - 0  
emitter.Houdini.RestSpawnState - [V]  
```


### Emitter Update
`SpawnParticleFromHoudiniPointCache` - Spawn only   

- `GetPointIDTospawnAtTime` - create spawn data: deltaTime, InterpStart, Delat, Count

<img align="right" src="/src/ue/niagara/houdinispaenfrompointcloud.png">  
.

```
R:    
engine.DeltaTime
emitter.LoopedAge  

R/W:  
emitter.Houdini.LastSpawnTime - 0.0   
emitter.Houdini.LastSpawnTimeRequest - 0.0   
emitter.Houdini.LastSpawnedPointID - 0  
emitter.Houdini.RestSpawnState - [V]   

W:
emitter.Houdini.MaxIndex  
emitter.Houdini.MinIndex  
emitter.Houdini.ASpawnParticlesFromHoudiniPoinCache.SpawnData   
```



### Particle Spawn
`SampleSpawnHoudiniPointCache` - sample data not set! (similar to sample niagara mofules )


- Creat `NID` - Particles.Houdini.NID: This is not the same value as the original ID attribute. This is the persistent Niagara ID that should be used for attribute lookups.  
- `GetPoint...AtTime` -   
- `Transform...` - Local to sim for: P, N, v

<img align="right" src="/src/ue/niagara/houdiniparticlespawn.png"> .  

```
R:
engine.Owner.SystemLocalToWorld
engine.Owner.SystemLocalToWorldNoScale
engine.Owner.SystemWorldToLocal
engine.Owner.SystemWorldToLocalNoScale

emitter.Houdini.MinIndex   // optimistaion > NID
emitter.LocalSpace
emitter.LoopedAge

R/W:
particles.Houdini.NID   

W:
particles.Lifetime
particles.Houdini.Alpha   // f@Alpha
particles.Houdini.Color   // v@Cd
particles.Houdini.Impulse  // @impulse
particles.Houdini.Normal  // v@N
particles.Houdini.Orient // 4@orient
particles.Houdini.Position // v@P  
particles.Houdini.Pscale  // f@pscale  
particles.Houdini.Type  // type  
particles.Houdini.Velocity  // v@v  
```

### Particle Update  
`SampleHoudiniPointCachce`

- `GetSampleIndexesForPointAtTime` - get sample index and BlendAlpha
- `Get... ` - and LERP
- `NF Transform Vector` (Local to Sim) + `NF Initial Particle Postition` (engine.Owner.Position)

<img align="right" src="/src/ue/niagara/oudinipointupdate.png">.


```
R:

engine.Owner.SystemLocalToWorld
engine.Owner.SystemLocalToWorldNoScale
engine.Owner.SystemWorldToLocal
engine.Owner.SystemWorldToLocalNoScale

engine.Owner.Position

emitter.LocalSpace
emitter.LoopedAge
particles.Houdini.NID  
particles.Houdini.CSVIndex

W:
particles.Houdini.Color   // v@Cd
particles.Houdini.Force   //
particles.Houdini.Normal  // v@N
particles.Houdini.Orient // 4@orient
particles.Houdini.Position // v@P  
particles.Houdini.Velocity  // v@v  
```

- set `particle.position` > `particle.Houdini.position` - drag  and assign houdini particle positiopn    
- set `Color` > `vector and float` > `Particles.Houdini.Color`    
- set `KillParticles` > (see custom script)    
`CombineForce`  



---


### Custom attributes script
New niagara module script: custom attributes:

Map get > [Get Vector Attribute By Name] > set `Input.HoudiniCache`    

(in parameters)
[EmiterAttribute] > Input.HoudiniCache >    
[ParticleAttrbute] > Particles.int32 (right namespace add modify to: Particles.Houdini.NID )
[EmitertAttribute] > Emiter.Age


### Houdini trigger

```
R:
`engine.DeltaTime` -
`emmiter.TimerActive`


R/W:
`emitter.DistanceToPlayer`
`emmiter.HoudiniCacheTime`
`emmiter.MoveToStartTime`
`emmiter.NiagaraForcesMultiplayer`
`emmiter.T3.Execute`
`emmiter.T4.Execute`
`emmiter.T5.TriggeredOnce`
`emmiter.TimeToRest`
`emmiter.TriggeredOnce`

W:
`emmiter.T1.Execute`
`emmiter.T2.Execute`
`emmiter.T5.Execute`
`emmiter.TriggerSomething`

```


## Sources   
Houdini niagara - ue plugin   
Houdini Extras - ue plugin   
[UNREAL FOR ALL CREATORS zobacz](https://youtu.be/3wcTor5rwmE) -
SideFx  
[2020 04 SideFx Niagara(frompluginContent) / Demo2020](https://www.sidefx.com/tutorials/houdini-to-ue4s-niagara/)  (water Paul)   
[2020 11 SideFx](https://www.sidefx.com/tutorials/realtime-fx-with-niagara-ue4/)  -  [2020 11 SideFx YT - to samo co wyzej](https://www.youtube.com/watch?v=jA3uAxT5FhM)  
Unreal  
[2018 11](https://youtu.be/GIzwxwrM9Mk)  
[2020 04 Inside Unreal - Houdini workflows](https://www.youtube.com/watch?v=LHFN8ccf_8o&t=3449s)  / paul / crowd / chains   
[2020 05 Unreal - Building advanced effects in Niagara Unreal Engine](https://youtu.be/syVSRDQxrZU)    character   
[2020 05 Unreal  talk](https://www.youtube.com/watch?v=tMPwXotnl5I)      Wyeth  
[2020 08 Unreal Fest Online 2020](https://youtu.be/oX6uiPWXJDY) dek kart  
[2020 11 Advanced Niagara Effects  Inside Unreal](https://youtu.be/31GXFW-MgQk) - popcorn    



RTVFX  
[Particle Location Module Mini Tutorial](https://realtimevfx.com/t/niagara-4-25-particle-location-module-mini-tutorial/13133)    - [Near Surface Location Mini Tutorial](https://realtimevfx.com/t/niagara-4-25-near-surface-location-mini-tutorial/14247)  - [Using splines for GPU particles](https://realtimevfx.com/t/niagara-4-25-using-splines-for-gpu-particles/13728)  - [Spline Location Mini Tutorial](https://realtimevfx.com/t/niagara-4-25-spline-location-mini-tutorial/15252)  - [Rope Physics Mini Tutoria](https://realtimevfx.com/t/niagara-4-25-rope-physics-mini-tutorial/13305)  - [Near Surface Location Mini Tutorial](https://realtimevfx.com/t/niagara-4-25-near-surface-location-mini-tutorial/14247)  - [Ribbon Trail Mini Tutorial](https://realtimevfx.com/t/niagara-4-25-ribbon-trail-mini-tutorial/13043)  - [UE4 Niagara Audio Visualization (passing data from BP to Niagara)](https://realtimevfx.com/t/ue4-niagara-audio-visualization-passing-data-from-bp-to-niagara/6902)   - [RTVFX pack](https://realtimevfx.com/t/vfextra-resource-pack/14503/6)

tuts
- [Fluid ninja 80](https://80.lv/articles/tutorial-driving-niagara-with-flowmaps-and-baked-fluidsim-data/) / [Fluid ninja pdf](https://drive.google.com/file/d/15IHebBnjuEzYKT8iwVnUQ5Rbzi5h21ws/edit) / [Fluid ninja YT]()
- [YT BTM series tutki](https://www.youtube.com/channel/UC11aPU7wAuBgvr6srciBpFw/videos)  
- [creative unreal table](https://youtu.be/3wcTor5rwmE)    
- [YT BTM series tutki](https://www.youtube.com/c/UnrealSimon/featured)  


## Camera Interface
on gpu more control. on cpu only on simulate will work

`input.newCameraquery` > `GetCameraProperties`   - gpu/cpu properties
`newCameraquerry` > `PropertiesGpu`   
`get Field Of View`    
`Get View Space Transform GPU ` - tarnsforms
`View Properties GPU`
(in input)  

##  Audio Interface
`AudioOsciloscope` - Direct access to waveform. high/low freq 1:1 waveform mapping   
`AudioSpectrum` - Buckets fft

`Play Audio` module


##  Occlusion
GPU
Occlusion of point in time can do for point ()  
`NewOcclusionQuery`  -  
`Occlusion Factor With Circle / Rectangle GPU` - compare to depth bufer    


```
Future:
- ray matching particle sprites/ meshes
- accum light in particle
- vdb

