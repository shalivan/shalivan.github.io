---
title: Unreal Niagara
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
permalink: /niagara/
---

Niagara can intreract with:  
Triangles  - u must point to spoecific mesh in query
Phys Volumetric
Scene Depth  - niestety: 2d, wiec nie ma info co jest za
Distance Fields  - !


# States

`System state` -   
`Emitter` - do what system (optimal to set for multiple emitters) do or define.   
`Particle` -   


https://youtu.be/3wcTor5rwmE - pre particle no force  
https://www.youtube.com/c/UnrealSimon/featured


-----



# Parameters, Attributes


###  Name Space

| Name Space | R | W | Define | Share within |
|--- | --- | --- | --- | ---|
|`System` | Yes | System | Persisted f2f | System
|`Emitter` | Emitter/Particle  | Emitter  | Persisted f2f | Emitter instance / color ect...
|`Particles` | Particle | Particle |  Persisted f2f  |  Per-particle (@point)
|`Engine` |  Y | N | Runtime for Niagara itself | Fundamental Attribs from unreal
|`Module` | Module | Modules | Within a module | expose a module input to the System and Emitter Editor
|`Module Locals` | |  | | Transient values that can be written to and read from within a single module. Transient values do not persist from frame to frame, or between stages.
|
|INPUT.|Y||| Use inside of module for promoted Parameters
|LOCAL.|||| Truly local for function !
Output ||Y|| pay for calculate but not for adding it to emiter (parameter writes)

name space modifiers:

- module - insert module name as namespace so if u have x modules u have x different params
- initial -  initial value of attribute (from eg in particle spawn)





### Map Attributes

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


----


# Script



## Script types




##### Module Script


<img align="right" src="/src/ue/niagara/module.png">  

-  you can see read/writes in finished module


##### Function Script

<img align="right" src="/src/ue/niagara/script.png">
.


##### Dynamic Input Script

<img align="right" src="/src/ue/niagara/dynamic.png">

.

#### Module usage flags

- Function - fn to use in modules
- Module - particle , emitter, system scripts
- Dynamic Input - particle , emitter, system scripts
- Particle Spawn Script - on spawn
- Particle Update Script - every frame
- Particle Event Script - In response to event
- Particle Simulation Stage Script -
- Emitter Spawn Script - once on spawn
- Emitter Update Script - Tick
- System Spawn Script - on system spawn
- System Update Script -




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
#### Expressions

- `/* Custom HLSL! */`  
- `sin(Emitter.Age *0.3) /2 +0.5` - 0-1 time x 0.3    
- `frac(Emitter.Age *0.3)` - 0-1 loop in time x 0.3   
- `float3(0.0f, 0.0f, Emitter.ZOffset) *0.2f)` - Add Z  
- `Particles.Position + float3(0, 0, (sin(Engine.Time) * 0.3f ))` - Add Z sin to actual pos    
- `float3(Particles.UV,0)` - make vector from uvs  

`(Particles.Position-Particles.PreviousPosition)/Engine.DeltaTime` - render velocity  

`Emitter.InitialPosition + Particles.RandomVector`  
`Particles.NormalizedAge`  
`Particles.Position - Emitter.InitialPosition`  

`cross(Particles.RandomVector, float3(0,8,0))` - cross   
`rand(1.5f) + 2.2f` - random   
`length(Particles.Position - Emitter.InitialPosition)` - length   
`saturate()` - fast clamp 0-1  

### HLSL Functions  






###  Conditioning  

`Particles.NormalizedAge<0.3 ? float4(1,0.1,0.1,1):Particles.NormalizedAge<0.5 ? float4(1,1,1,1):float4(1,1,1,1)`

```hlsl
Particles.Position.z > Emitter.InitialPosition.z - Emitter.ZOffset
  ? Particles.Position
  : float3(Particles.Position.x, Particles.Position.y, Emitter.InitialPosition.z -Emitter.ZOffset)
```


Ribbon radious

```
(1.0f-(abs((Particles.RibbonLinkOrder)-0.5f)*2.0f))*50.0f
```


------

# Houdini Interface
files:  
Houdini niagara - ue plugin   
Houdini Extras - ue plugin   

SideFx  
[2020 04 SideFx Niagara(frompluginContent) / Demo2020](https://www.sidefx.com/tutorials/houdini-to-ue4s-niagara/)  (water Paul)   
[2020 11 SideFx](https://www.sidefx.com/tutorials/realtime-fx-with-niagara-ue4/)  -  [YT - to samo co wyzej](https://www.youtube.com/watch?v=jA3uAxT5FhM)  
Unreal  
[2018 11]](https://youtu.be/GIzwxwrM9Mk)  
[2020 04 Inside Unreal - Houdini workflows](https://www.youtube.com/watch?v=LHFN8ccf_8o&t=3449s)  / paul / crowd / chains   
[2020 05 Unreal - Building advanced effects in Niagara Unreal Engine](https://youtu.be/syVSRDQxrZU)    character   
[2020 05 Unreal  talk](https://www.youtube.com/watch?v=tMPwXotnl5I)      Wyeth  
[2020 08 Unreal tut](https://youtu.be/oX6uiPWXJDY) inteligent sys    
[2020 11 Advanced Niagara Effects  Inside Unreal](https://youtu.be/31GXFW-MgQk) popcorn    



RTVFX  
- [Particle Location Module Mini Tutorial](https://realtimevfx.com/t/niagara-4-25-particle-location-module-mini-tutorial/13133)    
- [Near Surface Location Mini Tutorial](https://realtimevfx.com/t/niagara-4-25-near-surface-location-mini-tutorial/14247)  
- [Using splines for GPU particles](https://realtimevfx.com/t/niagara-4-25-using-splines-for-gpu-particles/13728)  
- [Spline Location Mini Tutorial](https://realtimevfx.com/t/niagara-4-25-spline-location-mini-tutorial/15252)  
- [Rope Physics Mini Tutoria](https://realtimevfx.com/t/niagara-4-25-rope-physics-mini-tutorial/13305)  
- [Near Surface Location Mini Tutorial](https://realtimevfx.com/t/niagara-4-25-near-surface-location-mini-tutorial/14247)  
- [Ribbon Trail Mini Tutorial](https://realtimevfx.com/t/niagara-4-25-ribbon-trail-mini-tutorial/13043)  
- [UE4 Niagara Audio Visualization (passing data from BP to Niagara)](https://realtimevfx.com/t/ue4-niagara-audio-visualization-passing-data-from-bp-to-niagara/6902)   
- RTVFX pack https://realtimevfx.com/t/vfextra-resource-pack/14503/6  

tuts
- [Fluid ninja 80](https://80.lv/articles/tutorial-driving-niagara-with-flowmaps-and-baked-fluidsim-data/) / [Fluid ninja pdf](https://drive.google.com/file/d/15IHebBnjuEzYKT8iwVnUQ5Rbzi5h21ws/edit) / [Fluid ninja YT]()
- [YT BTM series tutki](https://www.youtube.com/channel/UC11aPU7wAuBgvr6srciBpFw/videos)  




## Niagara ROP
- Export pointcloud as: **.hjson**, **.hbjson** - bin quicker  
 - `i@id`  per particle  same for one particle   
 - `f@time` of pop-up / arrival time // just normalize time before export!  check length from a to b and set time  
 - `@type` group   
 - `@life` Life set for first point    
 - `i@dead = 1`  
 -  `NID` - niagara id attrib CREATED BY SAMPLE MODULES  
no `Force` ?

hardcoded attributes -

## Unreal
### Emitter Spawn  - `InitHoudiniPointCache`  
Initialize  

```
W:  
emitter.Houdini.LastSpawnTime - 0.0  
emitter.Houdini.LastSpawnTimeRequest - 0.0  
emitter.Houdini.LastSpawnedPointID - 0  
emitter.Houdini.RestSpawnState - [V]  
```


### Emitter Update - `SpawnParticleFromHoudiniPointCache`
Spawn only   

- `GetPointIDTospawnAtTime` - create spawn data: deltaTime, InterpStart, Delat, Count

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



### Particle Spawn - `SampleSpawnHoudiniPointCache`
sample data not set! (similar to sample niagara mofules )


- Creat `NID` - Particles.Houdini.NID: This is not the same value as the original ID attribute. This is the persistent Niagara ID that should be used for attribute lookups.  
- `GetPoint...AtTime` -   
- `Transform...` - Local to sim for: P, N, v

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

### Particle Update  - `SampleHoudiniPointCachce`

- `GetSampleIndexesForPointAtTime` - get sample index and BlendAlpha
- `Get... ` - and LERP
- `NF Transform Vector` (Local to Sim) + `NF Initial Particle Postition` (engine.Owner.Position)

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


---

# Mesh Reproduction Static

Set position from static mesh   
Set UV by Dynamic material  

---

# Mesh Reproduction Skeletal
`initialize mesh reproduction`

#### Particle Update
`update mesh reproduction`

#### Material
- add Niagara mesh reproduce uv's




---

# Ribbons
`NiagaraRibbonRendererProperties` module.  

##### more ribbons

`SetRibbonIDByExecOrder` - get the particles execution index, make a Niagara ID and assign the execution index to the ID index, and then set Particles.RibbonID in the Map with our new ID.

---

# Constraints


---

# Communication between emitters
>one emmiter as about partikiel  np: flocking

`newParticleAtributeReader`   
`get Vector by Index` - get attribute (like Color) by Index (order particle responce)   
`get by ID` - niagara unique particle qttribute   


---

# Location Event  
##### Particle update
`Generate Location Event` - Add to leader  

##### Event Handler  
`Event Handler Properties` - Add to follower  
`Recive Locaation Event` - Add to follower


---

# Vector Fields
.fga  
add an Acceleration Force module under our Sample Vector Field, and then bind the value `SampleVectorField.SampledVector` to the Acceleration value
`VectorFieldSize`

http://andy.moonbase.net/archives/1499

---

# Camera Interface
`newCameraquery` > `GetCameraProperties`   
`newCameraquerry` > `PropertiesGpu`   
`getFieldOfView`    
`getViewSpaceTransformGpu`  
(in input)  

---

#  Audio Interface
`AudioOsciloscope` - Direct access to waveform. high/low freq 1:1 waveform mapping   
`AudioSpectrum` - Buckets fft


---

#  Occlusion
`NewOcclusionQuery` / `OcclusionFactorWithCirclegpu` / `OcclusionFactorWithRectangleGpu`     

---

# Collision query
>direction and d buffer sampling

---

# Sample Distance Field

---

# Neighbor Grid 3D
>special position cash when a lot of particle need global comunication


# PBD
---

# Flocks

Flight Orientation







# OLD

```
## Execution Index / Point ID:
- Execution Index - GPU ?   - ArrayIndex != ExecIndex (you can verify this by writing out Particles.MyExecIndex)  
make a Niagara ID and assign the execution index to the ID index, and then set Particles.RibbonID in the Map with our new ID
#### Execution Index / ID
`Engine.ExecutionCount` -   
`Engine.Owner.ExecutionState` -   
`Particles.ID` -   
`Particles.RibbonID` -   
`Particles.UniqueID` -   

--------------
## HOUDINI CHAIN HOW TO:
engine.deltaTime

### Emitter Spawn
Emmiter.Houdini.StartTime - 5  
Emitter.TimerAttribute - 0  
+ ini

### Emitter Update
+ trigger
Time.MoveToStart
Time.ToRest
Time.Cache
+ spawn from cache [static pos]

### Particle Spawn

+ sample
set anim time:  emitter.HoudiniCacheTime
+ position `H pos`

### Particle Update
+ Sample Cache [anim pos]
GoalPosition -  `houdini pos` - `pos`
+ Combine forces

`Houdini Quaternion to Unreal Quat` -  

##### Shorts
BP: set niagra variable   
`?` - refire particles in level   
Scratch module > draft local for system module. transient.  

not valid anymore

| Name Space | R | W | Define | Share within |
|--- | --- | --- | --- | ---|
|`User` |  Yes | No | In component or through blueprints | All Out Data
|`NPC` |  Yes | No | In parameter collection |
|`Local` | Script | | Hidden from modules
|`Output` |||| You can use but is not attached to particles
|`Temp` |  Script | Script |  Not persisted in any way | Script type that you are on
|`Transient`



```
