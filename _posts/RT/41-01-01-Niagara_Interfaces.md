---
title: Unreal Niagara Interfaces
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
permalink: /niagaraintrerfaces/
---

# Houdini Interface
files:  
Houdini niagara - ue plugin   
Houdini Extras - ue plugin   

SideFx  
[2020 04 SideFx Niagara(frompluginContent) / Demo2020](https://www.sidefx.com/tutorials/houdini-to-ue4s-niagara/)  (water Paul)   
[2020 11 SideFx](https://www.sidefx.com/tutorials/realtime-fx-with-niagara-ue4/)  -  [2020 11 SideFx YT - to samo co wyzej](https://www.youtube.com/watch?v=jA3uAxT5FhM)  
Unreal  
[2018 11]](https://youtu.be/GIzwxwrM9Mk)  
[2020 04 Inside Unreal - Houdini workflows](https://www.youtube.com/watch?v=LHFN8ccf_8o&t=3449s)  / paul / crowd / chains   
[2020 05 Unreal - Building advanced effects in Niagara Unreal Engine](https://youtu.be/syVSRDQxrZU)    character   
[2020 05 Unreal  talk](https://www.youtube.com/watch?v=tMPwXotnl5I)      Wyeth  
[2020 08 Unreal Fest Online 2020](https://youtu.be/oX6uiPWXJDY) dek kart  
[2020 11 Advanced Niagara Effects  Inside Unreal](https://youtu.be/31GXFW-MgQk) - popcorn    



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
- [creative unreal table](https://youtu.be/3wcTor5rwmE    
- [YT BTM series tutki](https://www.youtube.com/c/UnrealSimon/featured)  






## Niagara ROP

- Export pointcloud as: **.hjson**, **.hbjson** - bin quicker  
 - `i@id`  per particle  same for one particle   
 - `f@time` of pop-up / arrival time // just normalize time before export!  check length from a to b and set time  
 - `@type` group   
 - `@life` Life set for first point
 .    
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
on gpu more control. on cpu only on simulate will work

`input.newCameraquery` > `GetCameraProperties`   - gpu/cpu properties
`newCameraquerry` > `PropertiesGpu`   
`get Field Of View`    
`Get View Space Transform GPU ` - tarnsforms
`View Properties GPU`
(in input)  

---

#  Audio Interface
`AudioOsciloscope` - Direct access to waveform. high/low freq 1:1 waveform mapping   
`AudioSpectrum` - Buckets fft


---

#  Occlusion
GPU
Occlusion of point in time can do for point ()  
`NewOcclusionQuery`  -  
`Occlusion Factor With Circle / Rectangle GPU` - compare to depth bufer    

---

# Collision query
direction and d buffer sampling

---

# Sample Distance Field

---

# Neighbor Grid 3D
special position cash when a lot of particle need global comunication


# PBD
---

# Flocks

Flight Orientation

# Events
push
Will be 2.0! cause of fixed payloads (could be arbitrary )
# Attribute Reader
Listen to other emitter (events not push, but pull directly) - bats, flock, swarming bugs.

`Get Vector by index` -
`Get Spawned ID at Index` > `Get Vectro by ID`

you can use it on yourself every particle can ask of neighbour pos (phys line)
can integrate with otherforces (like cable component in niagara)
 and

 Is better then events in some way



```

Future:
- ray matching particle sprites/ meshes
- accum light in particle
- vdb
