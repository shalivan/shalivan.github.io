---
title: DOP RBD

categories:
 - HOU
tags:
- DOP
- Houdini
description: RAW! Houdini solver.
permalink: /rbd/
---




- work with packed geometry  
- to wiev subframes: in global anim options  (global subs?) And Time is float turn off /  solver substeps (expensive when stacking obj)  / constrain substeps  


`rotational stifness` // how much object will spin (how much object inherites rotation when hit by another object), 0 - means no rotation  
`bounce` // how much energy conservation there is when two objects collide, this is multiplication between the two objects (e.g. sphere and the ground)  
`friction` // how difficult is to move object from rest. 0 - no resistance at all  
`dynamic friction` // multiplier for objects that are already moving  

## `Rigid Body Solver`   

>The RBD engine uses volumes and is useful for complicated, deforming, stacked, geometry. The Bullet engine offers simpler collision shapes and is suitable for fast, large-scale simulations.
(RBD Solver is unable to enforce glue constraints between RBD Objects and Static Objects. You can work around this limitation by using constrained RBD Objects (perhaps with some RBD Pin Constraint DOPs) instead of a Static Object)


### OBJECT
`objects`  
### PRE-SOLVE
`pop forces` - apply pop forces in RBD in dop: plug pop forces into middle input    
### POST-SOLVE
`sop solver` - will take geometry and transform it  

## `Bullet solver`
>bullet likes pieces between 0.1 and 100 if you need smaller pieces, scale up and boost gravity proportionally  
### OBJECT
### DATA STREAMS

## `Multi solver`  
- multisolver is for pops (and rigid body)  

## `Static solver`

## `SOP Solver`
- dop geo impact and feadbacks and gve tou also import merge geo.

https://youtu.be/aAbXLK26Tok
---

# RDB Objects:  

### `Static object`
moze byc jako kolizyjna ruchoma geometria w dopach (Simulating a Splashdown in Houdini - Escape Studios Free Tutorial)  
if its plane turn off volume based collision
**Vdb collision source:**
- mode: collision intersect to volume source
- proxy volume: vdb path  

Invert sign - reverse collision

### `RDB Object`  
Also use for collision in flips  flips  (FLIP Fluids https://vimeo.com/116176349)
- increes density


### `RDB Packed Object`
rotation for packed RDB :  dop angular momentum ? ??? or use POP torque !  

# Constrains:
`s@constraint_name` (prim)    
`s@constraint_type` (prim)  
`broken` (prim}group will be ignored by solvers on subsequent frames.   
`next_constraint_name`  
`next_constraint_type`   
`i@propagate_iteration`	Detail   

### [Soft Constrain]
Use it a lot (ony bad case is lot of oscilation with small dumping witch require lot of substeps) not enough subs can cause unexpected damping  
`stiffness` - (mass indep.) frq (nr of iter per sec) 1 > 100 stiffer > to infi. (will bend anyway, oyu can increase substeps)   
`damping ration` - (mass indep.) 0 - bedzie oscylowac zanim wroci, 1 soft return to standard pos. Over >1 can incresse even more      

### [Spring Constrain]
`strenth` - string constant (mass dep.)   
`damping ` - damping coeficient (mass dep.)    

### [Hard Constrain]

### [Glue Constrain]
halftime - remove impact pwer (decay over time)  
propagation rate - 1  - will spread evn to naaighb.   
propagate iteration (same as solver iteration ovveride on other consrains) `-1 `< use default value /`1` propagate. Override it in SOP as prim attrib `propagationiterations`   
```cpp
- Unpack
- Adjectconnectedpieces
- Primwrangle:
s@constraint_name="YoName";
s@constraint_type="position";
```
---

# Collision
- spheres collision over convex !!!!!!


```cpp
- Volume collisions support
- Sphere collision for bullet ! Super fast  // on object use 'compound' collision  /// + BAKE ODE in SOP
- Convex decompositon // can be slower than spheres
```



---

#  magia jakaś:





`@name` - name pieces   
`@v` - velocvity   


STATES:  Key for states: Na spakowanegj geo przed solverem: //active = solve //  deforming: Anim > Pack  // animated: Pack > Anim  
```cpp

i@active=0;  
i@deforming=0;
i@animated=0;  ```
` set i@active=0 after packed primitives in SOP's
in dopnet create multiple solver
connect sop solver
in sop solver make group (box) selection of the geometry
animate the selection
attrib wrangle on the group to change i@active to 1`
```
Key frame active  // node
Physical params  // Set Attributes in DOPs
Apply Data  // apply attributes in DOPs
```
