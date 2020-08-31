---
title: DOP FLIP

categories:
 - HOU
tags:
- DOP
- Houdini
description:  Houdini solver.
---

Fluid Implicit Particle - Based on Navier–Stokes equations, implemented in OpenCL (can combine with vellum) hybrid solver. All fluid data is stored in the particles (with pscale) and only particles need to persist frame to frame, However, the pressure projection step is done on a volume.   

- Size sensitive: use units as meters.  
- Time sensitive: (but why?)  

Viscosity   
Surface Tension  - Deip drops, Crown Splash, Suction, Avoidance
Divergence   

---   


<img src="/Sources/flip/flipsolver.png" width="406">



# `FLIP Solver`


1. OBJECT
   - `Flip Object` - mandatory    
2. PARTICLE VELOCITY  
   - `Pop VOP` / `Pop Wrangle` - @viscosity=   
   - `Pop Force` (can be merged)  
   - `Pop Curve force` (Illume Jeff I ) // input curve    
   - `Pop Solver` / `Sop Solver` // access any sop (cmi)   
3. VOLUME VELOCITY    
   - `Gas Field VOP` // taki volume from sim  (Illume Jeff II )  
   - `Source Volume` -  fluid source as velocity field   
4. SOURCE    
   - `Volume Source` (initialize source flip) (with SOP link to: `Flip Source` SOP) If not will use op1 Flip Object    
   - `Heat Volume`  // can spread temp  // lave cool rate   
   - `Gas Temp Update`   
   - `Pop Color`  

## Sub steps:
Time Scale !+  
- timestep = (divide 1 frame to few)  
- substep = (add steps in 1 framie) Fluid dont need it exxeption are: fast moving fluid that collides with other objects and Surface tension.


## Particle Motion:
### Behavior
`Collision detection` Move Outside Collision is the fastest collision handling method and provides the smoothest splashes, however it is not as accurate with fast-moving collision geometry. It is also the only collision method that works with Volume Source based collisions. the Particle method only works when a collision is represented by an actual DOP object.  

`Default velocity scale` for Volume Source is 1.5, which will cause larger splashes by default, but for moving containers this should be set to 1.
### Reseed:
`Reseed` - You’ll get an uneven distribution due to numerical error, especially with Reseed Particles turned off.  
### Separation:  
-

### Droplets:  
`Droplets` - Tend to clamp toghether when partic drop below certain density turn to droplets more likely. After blend back to fluid: `Blend` / `Merge` / `Kill`

### Vorticity:
For chaos & white water.  
`Preservation rate` -  (how much vorticity should rename of end of second) (decay value) retain swirling motion.  


## Volume Motion:  
`Velocity transfer` Kernel -  `Splashy` >> `Swirly`  is not as noisy and turb. (Houdini 16 Masterclass) and keep vorticity better  
`Smoothing`
### Volume Limits:  
`Waterline` - (semi open boundaries)(above open, below close) it should be on water level.    
`Use boundary layer` - (adv waterline) (velocity volume - at volume boundaries) (surface volume control geo in boundary padding) if both not connected it will use warterline options. (Houdini 16 Masterclass)  
### Collisions:  
`Stick on collision` -  [viscosity free solutions!: ]( simualte sth like (free slip condition) but inbverse)   

### Viscosity:    
Adhesive force which resist motion (lava).  Measured in: (centi)Poise.  
To control locally use `@viscosity` attribute on points


`Slip on collision`   
 - 0 take vel from collider (Can't slip) Sticky    
 - 1 to completely slide fluid on collider Slipy (can slip (tangentially)) (fluid vel = no impact of collider tangential velocity). [Its opposite to: stick to collision]. (Houdini 16 Masterclass)


### Density:   
By default, the fluid has uniform density as set on the Physical tab of the FLIP Object.
### Air:  
Enforce Air Incompressibility on the FLIP Solver. This feature prevents air pockets from collapsing
### Divergence:  
Divergence is measure of imbalance. `Scale` component is using pressure field  
Incompresive fluid - have not "scale factor" still have : swirl , shear and translate factors



### Surface Tension:     
- *In small scale it can be unstable*  
- `Adhesion` - menisk wklęsły   `Cohesion` - menisk wypukły

Property of warte molecules that are attracted to each other (cohesion). it is on surface, where molecules have space to stronger their bonds forming a tension that is absent in rest position. Measured in: **Pa * s**.  

Creating the surface pressure field. Fight against gravity trying to put particles in to drop (bostly in places where curvature of shape is bigest).


Bigger value, liquid tend to min. surface area. Blurring shape. Create oposeing forces on large changind curvature.



## Narrow Band:   
Work only with reseed  


---

# `Flip Object`


`Particle separation` -  Point separation (seed density) Increasing will lower the resolution  
`Particle radius scale`  - actual radius of every particle    
`Grid scale` - Volume scale // higher for sharper // fat crona >> thinner splash  ()  
`Closed Boundaries` -
### Initial Data:
Input type:   
   - Surface sop
   - Particle field
   - Narrow Band  

### Physical:
Physical behavior : `Bounce`, `Friction`, `Temperature`, `Density`, `Viscosity` (if viscosity by attribute in solver is checked and there is point attribute at sop viscosity will be multiplied)


---
# `Volume Source`
`Initialize` -  type
   - Source FLIP - default path to `FLIP Source` SOP  
   - Sink FLIP - sink point  (size depend speed of sink)

`Input` - path    
`Name source volumes` -  volume name  

---

<img src="/Sources/flip/flipsource.png" width="406">

# `FLIP Source` SOP
(for Volume Source DOP)- converts its input geometry into a volume that can be used to control simulations. For instance, the generated volume can be used to inject liquid into a FLIP simulation or act as a sink in a smoke simulation.   
[volume operations] set behaviour (add/overide velo)      
[velocity volumes] source attributes - we can sample it from N or sth.
[container settings] - velocity

---

# `Flip Tank` SOP

`Points From Volume` (for source volume  DOP) // source from points (change[Initial Data] input to *particle field*)  
`Oceane Source` (for flip object  DOP) (particles(points)+volume for: sop path and surface volume) //  (change [Initial Data] input to *narrow band*) Fluid Tank ?    

`Limit Refinment iteration` - can remove glitches, use only in small scale (good for visc droplets ect...)    (particle fluid surface)  

---

<img src="/Sources/flip/flipimport.png" width="406">



# `DOP I/O` SOP
Points + 4volumes. For further processing.    

`DOP Network` - path to DOP Node  
`DOP Node` - path to `Flip Object`  

Choose volumes from preset or import custom volumes     


# `Fluid Compress` SOP
 before cache

# `Fluid Surface` SOP
to get fluid surface  

---
# `DOP import` SOP         
Import Points  

`Particle Fluid Surface` - limit refinement if unstable. / Change surfacing > surface output > from surface polygons to Surface VDB !!
For emitting large numbers of particles, the Volume Source DOP can be much faster than the Particle Fluid Emitter DOP.

---

# Collisions
 Deforming Object shelf tool

**Volume Source based collisions**: Work only with  **Move Outside Collision** method for particle collisions, because the Particle method only works when a collision is represented by an actual DOP object.

**Move Outside Collision** is the fastest collision handling method and provides the smoothest splashes, however it is not as accurate with fast-moving collision geometry.

`static object` with collision mode to: volume sample {DeformingGeo shelf}   
- Enabling Collision Separation on the FLIP Object and setting this value to the Particle Separation or smaller will create a higher-resolution collision field
- Accurate velocities for moving collision objects are extremely important.
- {Deforming Object} shelf tool to set up deforming geometry as a FLIP collision object.
- SOP `Collision Source` -  interpolate deforming geometry, calculate point velocities, and create VDB. Usually used in conjunction with a Static Object DOP.


---

# VEX
`i@stopped`   - You can stop the particles in a flip sim with  
`v@v` => vel  
`@viscosity` -

---

## Velocity1
you can create `velocity field` > `source volume`


## Populate containers  
Can work with flips   
`Pump from ` - create volume velocity (like)  

 ---

 Divergence | . |
 --- | --- |
 `-` | Clump them together.
 `0` | For Incompressive fluid
 `+` | Cause particles to spread out

Viscosity - how much tend to be solid   
Enable in `Flip solver` and set value at `Flip Object`  

 Viscosity | value at CentiPoise (at room temp ~21°C (70°F)) |
 --- | --- |
 Water | 1
 Milk | 3
 Motor Oil  SEA 10 | 85-140
Motor Oil  SEA 30 | 420 - 650   
Motor Oil  Castrol | 1000
 Honey | 3000- 10 000
 Chocolate | 25 000
 Ketchup| 50 000
 Mustard | 70 000
 Sour Cream | 100 000
 Peanut Butter | 150 000 - 250 000  
 Sanitary Silicon | 5M - 10M





---
# Setups  
**Crown Splash**
```
Flip tank with bounadary layer
Velocity transfer Splashy >> Swirly  
Surface tenssion 48 // high value less motion for
Grid scale // fat /thin 1.5
In self they reduce gravity
Substeps up!!
```
Gravity reduced in  Drip and crown to have small scale !   
depend on velo of obj  / scale
depend on grid scale (grid to create surface and measure curvature )  
Substeps up 5+

surface tension ON   


**Droplet**

- if small flip is unstable if smaller increase substeps minim 5 -6
- Surface tenssion 48000
- grid scale tez wpływa
- reduce gravity for slow moving slow scale

**Suction**
- op2 antigravity (opose gravity around object)
- op3 suctionforce. strength + gradient on distance sometimes you need to keyframe it  
- collision source on geometry (velocity, volume out) + interior exterior distance for gradient



**floating RDB:**   DOP>flipsolver>Volume Motion>solver change Feedback Scale from 0 to 1.  
 https://vimeo.com/116176349#at=158  
 https://youtu.be/JzxXjHgkIIc

```
Merge: rigidbody solver + flip solver
Check density of object (mass)    
Bullet solver with rdb object is working as well
```
**Pyro > Fluid**  
https://vimeo.com/157944287  
```
Sim Pyro > Import > Points from volume
Flip Object > change sop path to points
Cration frame spec sim frame check
```

**Pyro > Fluid**  
https://vimeo.com/296410457  

**Fluid Follow Curve**    
https://forums.odforce.net/topic/31596-fluid-follow-curve/   

**Mix Colors**  
https://youtu.be/DWxcfZMsZW8    


www.sidefx.com/docs/houdini/nodes/dop/flipsolver.html     
www.danenglesson.com/images/portfolio/FLIP/rapport.pdf    





http://igorfx.com/hou_adaptive_flip/   
