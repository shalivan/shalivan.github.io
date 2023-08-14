---
title: DOP Vellum SOP

categories:
 - DOP
tags:
- DOP
- Houdini
- Simulation

description: SOP's Solver
permalink: /vellumsop/
---



[Vellum SOP.hiplc](/src/hip/DOP_VellumSOP.hiplc)  


<!-- more -->

# Geometry
Configure  Parameters  

#### Geometry


|| low | ||
|-|-|-|-|
|**Mass** |  0 - mass inactivete  || Can set from param or calculate
|**Thickness** | | |( `edge len scale`- multi for thick)  Can set from param or calculate

- check thickness. should be smaller than distas between points


#### Drag
Slow down motion





### Stretch
For cloths, curves or constraints (like attach)


||low |high ||
|-|-|-|-|
**Stiffness** | 1 - stretchy (spandex) | 1e +10 rigid (leather)   | How stretchy material is (default infinite)  
**Rest Lenght Scale** |0 - to snap all points in one | 1.1 - 10% larger after sim | Rest of edges (default 1)  
**Compression Stiffness** | 10 - paper remain curled | 1000 - rubber (hi resistance )| How much can compress material (lower distance between points)  
**Stiffnes Dropoff** ||Stop bounce|  On distance (m) or angle
**Damping Ratio** ||| Lit more energy from sim  if too lively  (dont change) too much destory    
**Plsticity** ||| Will return to rest pos.   

- wrinkliness (with low res sim lower param help to remove jagginess) / (if compress how likley it stay compressed)  more is more likely stay  (decrease more smooth look and dont enforce wrinkles)  
- `f@restlength = f@restlengthorig + fit(f@mask,1,2);` - restlength by param.   
- `i@group_pin = @mask < chf("mask");` and add to 'constraints stream (op2)' by copy attribute > promote point to prim

### Bend

||low |high ||
|-|-|-|-|
**Stiffnes** | 0.01 - soft and bandy (silk) | 1000000 - more rigid (plastic))) |  How much resistant to unroll or bend   
**Rest Lenght Scale** |
**Plsticity** | will return to rest bend || / treshold -  below toehold will return to shape  / rate - how fast become plastic / hardening  while deform incresse
**Treshold** | enter new config easy and quick   ||  
**Rate**|| | make harden over time of banding  
**Hardening** || | make harden over time of banding     



# Constraints
Constraints are geometry attributes. Add in sop and edit it in `velum Constrains Properties` inside vellum solver to modify constr dynamicly

### UI
`Constrain  Browser` - window ! to chceck constraints


## Types


### Base

|| Effect | |When to use||
|---|---| ------------------------------------------------------------------------|---|-|
**Distance** |   Stretch | Keep distance Along Edges by Stiffness and Damping | basic
**Bend**  | Rotation |  Keep angle Across Trix  | basic
**Slide**  | Slide |  H18  |
|-|-|-|-|
**String**  | Distance + Angle  | Cheaper than hairs  |
**Hair**  | StretchShear + BendTwist |  Use polyline or L-sys as input (its like distance bend and twist)
|-|-|-|-|
**Cloth** | Distance + Bend  |  
|-|-|-|-|
**Pressure** |  |  Compresable Volume  (enforce volume depending on stiffness) (fstr than tetra)  | Air   
**Tetra** |  | Uncompresable Volume Tetrahedral fwm  (requiure tetrah geo: solid conf SOP)   |  Liquids
**Struts** |  Stretch Body| Conect opose sides. Good for stftb. that does not stiff tu much   


### Hard
- Hard - Geometry point attributes
- Direct update
- Create / remove by setting point attribute

|[Direct update]|Hard |  Create / remove by setting point attribute | -||
|---|---| ------------------------------------------------------------------------|---|-|
**PinHard**   | Geometry point attributes  | Set type: permament/stopped.  `stopped`, `pintoanimation`  |Pin to Target position |  ![](/src/vellum/pinhs.png)  
**Weld**  | Geometry point attributes   | Threat pts as one point and will look like 1 object  Can break at stress level.  (add bend across weld for smooth normal) Autobreakable (pre-tearing)  `weld`, use pointid or groups ! | Same @P (fuse), Fractured cloth |   ![](/src/vellum/welds.png)

### Soft
- Soft -
- Solvable
- Create / remove by `vellumconstraintproperty` DOP node.
- [plasticity / autobreakable]


|[Solvable]|Soft |   Create / remove by `vellumconstraintproperty` DOP node.   | [plasticity / autobreakable]||
|---|---| ------------------------------------------------------------------------|---|-|
**PinSoft**  | Constraint primitive | Pin to Target  position (remove manualy constr) / stiffness(magnes) |  Magness, Pin to own anim to get detail in existing movement   | ![](/src/vellum/pinss.png)
**Stich**  |Constraint primitive|  Soft or Stich Weld.  Points with in 2 groups that are far - keeping them apart. Can stitch to poligon instead point. SLIDE (remove manualy constr) plasticity. Can have spaces between points | Additional cloth pieces, keep distance  | ![](/src/vellum/stitchs.png)


|Name | Effect | |When to use||
|---|---| ------------------------------------------------------------------------|---|-|
**Glue**  | Constraint primitive  |  Glue source to target distance treshold (check: nr constr per pt)(remove manualy constr) plasticity | Anim,  2 pieces
**Attach**  |  |  Stick to closest point on geometry & keep distance    |  Anim objects


Connect cloth to body = cloth + attach
fix attach from nearest with interactive tool !! https://youtu.be/5s8I2fs8kMs?t=2081   

### Pin To Animation

submenu Wystepuje w curves lub pin to target


- `Permament` Hard - Is storet as geo point attrib  - not solving constr, update pos directly.  mass = 0 (cannot be move by constsr)   
- `Stop` Hard - mass not changed but `i@stopped = 1` prevent to inf;luence from constraints(same in pop)  
- `Soft` - constr peimitives (pin stitch glue)  (inheret Strech Stif Parameters) can have varying stiff and breaking threshold         
- `Orient Pin` - for hairs    
- `Match to Animation` - animate with object    `i@pintoanimation = 1`

### Breaking

Weld have stress threshold
Different types by: Stress or Ratio  (sensitive, low values)
normalize stress on solver -  to normalizes for sub steps change


---

# Collision

Surfeca colider You dont need VDB  
You can ad per point `friction` attribute  



---

# Solver (DOP Forces)


1. OBJECT
2. CONSTRAINT
3. COLLISION

## [Velum Constraint Properties] DOP
Change constraints properties  (can animate here )
- use groop to affect only one

## [Velum Constrains] DOP
Set constraints here (change from 1'st to each frame creation)  


#### Remove Pin Constraint
Unpin for soft constraints
- (create output group in vellum constraint and use it in [Remove Pin Constraint] )
- and check box REMOVE > 1
- set time/frames

(WHEN u have animation, animate after constraints and before solver )

## [Vellum Rest Blend] DOP
Blend 2 meshes to change rest position    
There are two nodes SOP one and DOP one !!!!


### Rest Blend SOP

 
### Rest Blend DOP

https://youtu.be/_wFjD0xkM-E




## [Pop Force]  DOP

## [Geometry Wrangle]  DOP


Unpin for hard pin (Type: Stopped):

```cpp
if (@Frame > 10)
{
  i@stopped = 0;
  i@pintoanimaion = 0;
}
```
Unweld

```cpp
if (@Frame > 10)
{
  i@weld = -1;
}
```

Initially set Stress Type to None(0) (never break)

```cpp
if (@Frame > 10)
{
  s@breaktype = "stretchstress";
}
```

Inputs (link to group node with group animation) and check if is in group:

```cpp
if(inpointgroup(0,"unweld",@ptnum))
 i@weld = -1;
```


# Setups

### Set Target

**Avoid time dependences** - set  when pining top not fetch animation to solver  
![](/src/vellum/vellumtargetsmall.png)



## Grain
- [Vellum Configure Grain]
   - Increase substeps 5+
`@breaktreshold` / `@isgrain = 1` / `@mass` / `@pscale` / `@v` -   

can set up to fluid !!


- `attraction weight` - clumpy sand  
- `repulsion wetight` - used only  When U want prevent grain+fluid to mix togheter (make softwr grain collision so not make sense for only grains)
- `phase` - particle is velum fluid (if non 0).  Same phase = same fluid.
  -

   ========When solving viscosity and surface tention -

## Rigid Grains
by shape matching
1. `configure grain pieces`
2. after sim:  `vellum xformm pieces` -


## Water Grains





## Balloon
- [Vellum Configure Baloon] = cloth Constraint + Pressure Constraint     
- anim stretch on pressure constraint
- change volume setup: - `rest length scale`    
 - `Stretch Stiffness` on Cloth  and pressure.  low - jellow , high stiff ,
 - `Bend Stiffness` - Cloth  more bandy soft bodies,
 - `Damping ratio` - cloth stretch section  

Expose output group in pressure  `@pstretch` - @VellumsconstraintProperty inside solver forces
`cluster points` - to glue constrain


## Soft Body
`[Vellum Configure Soft Body]`
= cloth + struts     

## Hair / Grass
!!!!!!!!

plasticity


## Guided Animation
Use:  Vellum Rest Blend

## Tertahedral
use model: scale invariant ARAP ! new 19.5
(used in muscles)

there are grain collision options !
and open CL !

---



# Post Process

##  [Vellum Post Process] SOP
Spply Welds - Weld geometry that have cuts  and in theory should stick together   
Visualize - !    

##   [Detangle] SOP
run in for loop with feedback.   
- rest position as previous position   
- pscale   

---  





---
# Drape

##  [Vellum Solver drape] SOP
To create drape from patches.  
`welding frame` - where it start to fuse  (maby work on frame 1 ?)   
`forces` - increase velocity damping and air drag if cloth move to much  

Drape solver help resolve cloths  

`Weld Points` - create constraint, glue drapes by points.  (breaking treshold)  
`planar patch from curve` - from curves   
`planar patch` - only simple shapes   
`planar pleat` - make patterns   

### Mirroring cloth:

`*_L*`  
`*_R*`  

`Name_RB` -   Right Back  
`Name_RF` -   Right Front  
`Name_LB` -   Left Back  
`Name_LF` -   Left Front  

---------------


https://www.sidefx.com/tutorials/vellum-nodes/ - quick tuts
https://youtu.be/NwabG-znu9Y?t=5745 - H 17 advanced wath end
https://www.youtube.com/watch?v=zPQZ8KJTjzo - H 18
https://www.youtube.com/watch?v=iHtdex9kM-A - grab constr
https://youtu.be/qAraO2E-v84 - megaplex part 1 (part 2 on gum)
https://www.youtube.com/watch?v=8ge2W7KKwf8&t=163s - entagma stitches
https://youtu.be/rQw2UZGWP-0 - rozwijanie płachty


---
https://www.youtube.com/watch?v=km2uXhfvWvk
https://www.sidefx.com/tutorials/vellum-nodes/  

----------------------


# H 19.5

Spatial Sort Interval. - Sot grain fluid  particles  in memory. It sould change particle count !!!!! (help with speed of grain fludi sim )
