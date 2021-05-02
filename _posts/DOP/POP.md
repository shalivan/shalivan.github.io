---
title: POP

categories:
 - DOP
tags:
- DOP
- Houdini
description: Houdini solver.
permalink: /pop/
---

```
FEM !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
https://youtu.be/GHjopp47vvQ
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
```



Vex based solver.  green inputs have wired into them POP microsolvers.  
Multisolver is for POP and rigids.    
Order in dops: from solver upward to each end of stream from left to right and then throu each streams from up to solver.  
microsolvers have always binding on which geo it operate.     


[Basic pop](/src/hip/DOP_POP.hiplc)

# Solver

## [POP Solver] DOP

1. OBJECT (gray)
      - `pop object` - mandatory pop object. Its just container  
2. PRE-SOLVE (Purple connection - only order of executed   )
      - `Pop VOP` / `Pop Wrangle` - @viscosity=x;   
      - `Pop Force`, `Pop Curve force` (can be merged)  
      - `Pop Solver` / `Sop Solver` - access any sop (cmi)   
3. SOURCE ( Purple connection - only order of executed   (some nodes are stream generators: POP Source))   
  - `pop source` - mandatory create `Geometry` stream // sop solver aadding point to container. // (birth / activation)   
  - `pop force` - curl noise   
  - `pop group` -    
  - `pop vop`      
  - `pop kill` - `if (@age>1) dead = 1;`   
  - `pop interact` - interaction between particles  
  - `pop interact` - advectbyvolume  




#### Collision:
#### Sleeping:

---

## [POP Object] DOP

Bucket for particles
Physical parameters: `Bounce`, `Friction`, `Temperature`


---

### [POP Source] DOP

source types: set to all points for points in.  
impulse count (per frame) / constant birth (for time) / life  
attribtes > velocity > inherent (default!) from param: v@v  
attribtes > velocity > for the first frame
Emission Attribute - ATTRIBUTE TO EMIT PARTICLES (float 0-1)
#### Sourcing
(source obj) `debricesource` // for RBD ingeret vel   
(source obj) `fluidsource` // volume source from point   



---

## Forces DOP's
`[popforce]` - basic with VOP  
`[popwind]` - stop accumulating v when reaching given speed    
`[popattract]` - (to point or geometry)  if bouncing increase Air Resistance  
`[popaxies]`  rotate around axies  (use suction speed to not let go too far)  
`[fireworks]`  

`[popdrag]`   
`[popvop]` - sam mozesz zrobic force, np ( vel +=  noise)   
`[popcurveforce]` - podpinasz krzywa i leci   
`[popcolision]` - (stick/ bounce)     

####orient:  
`[poptorque]` - like a force adding every frame  
`[popspin]` - spin at constant speed  (+`popDragSpin`) (`W` - rotation velo, + `oriten`)   
`[popLookat]`  

####po solverze:
`[gravity]`
`[field force]` + (`sopvectorfield`) - tam gdzie grawitacja  (Vector Fields)   








---

## [POP Fluids]
> `popfluid` PBD fluid make intersection - maintain Particle Separation (node from white water) Can make cohesion and basic surface tension (https://vimeo.com/295491505 Lewis Orton).   

- `Constrrain iteration` 20+  (50?)
- `Constrain stifnes` // up do sich particles.
- `Viscosity` // up even to 1
- `Tensile Str.` // up to 0.01 even more to not break so easly.

## [POP Grains]
>Are just proper collisions for pops   
`POP Grains` - set next after source   
- particle sep should be same as grain source  
- for test you can lower constrain itters  
Friction:  
- static treshold  
- scale kinetics (accelerate friction and stop to scatter on collision)  
Clumping: make stick particle toghether  
Break constraint treshold:  

# Source
### `[Grain Source]` SOP
- export points with pscale  >> `[POP Source]` DOP
>emit from all points (if you are using constrains from geometry)

[POP Solver] changes:  
- itterations 10
- max speed - can change speed scale to decrees forces  
https://vimeo.com/132847114  


# Velocitty
Go this far every second in units. (by default distance is divide per 24 frames).   
Apply it by forces or inheret v@v - create from motion by trail sop!   

`v` - velocity   
`w` - rotation Velocity   
`dead` = 1  


### `[POP Wrangler]`
@dead = 1; // kill (pop solver > update > reap particles)  
@id (insteda of ptnum)  

length of the velocity vector and if it exceed a threshold, remove pt
```
float threshold = 0.1;  
if(length(v@v)>threshold){removepoint,0,@id,0);}
```
same with location  
```if (length(@P-@rest_P)>threshold){removepoint(0,@id,0);}```

---
```


# Setups  

#### Condensation - Shelf tool

***Adhesion parameter*** is creating force with collision geo. (meniscus {wklęsły i wypuły :]})
- `Strength Multiplier` parameter on the Geometry Wrangle (adhesion_force).    
- `Friction` parameter on the POP Object Control how slowly the liquid flows over the object make the liquid drip off the object quicker
- pop fluids parameters to set fluid.
--
- Limit Refinment iteration  at  (particle fluid surface)  
Source:  
- `add emision scale` - max value zmniejsz zeby zmniejszyc ilesc klatek w ktorych jest emisja ()  
- `fade` - how long emiting from one spot. (less, smaller ) (Wywill kernel - for not conecting so much) (ew. distance treshold)
- `scatter` - po lewej wiekszy daje ci strumien, po prawej wiecje ptk daj droplety
 (https://www.youtube.com/watch?v=yQoWgVuLXo8)    

#### White Water

(h17 core of new water solver in future maby with vellum).  
```
Constrain Iteration -  20
Constrain Stiffness - 100 (stay toghether )
Viscosity - higher value to sticky durfaces
Tensile Strengh - keep distance between particles 0.01 - larger make
```
https://vimeo.com/323269227 (Entagma)
