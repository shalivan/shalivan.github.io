---
title: DOP  PYRO

categories:
 - DOP
tags:
- DOP
- Houdini
- Simulation

description:  Solver
permalink: /pyrodense/
---

```
velocity voxel (sccale down ) - will be fast
```

PYRO Dense is not using Sparse!

| PYRO Fields |
| --- |
|Fuel - `fuel`       
|Burn - (only temporary field) recalc evey frame and if you cut out fuel it desaper.     
|Flames - `heat`  dep on: `fuel`, `butnrate`- Heat is the intersection of fuel and temperature fields).  
|Smoke - `density`    is like a mask    dep on:  `fuel`, `butnrate`, `smoke amount `  
|Expantion - `divergence`  dep on: `fuel` `burntrate`, `gas released`    
|Temperature - `temperature`  dep on: `fuel`, `burnrates`, `flame contribution`, `burn ccontrib` (may exist anywere).     

`pressure` / `confinment` / `pump` / `sink` / `vel`    (dop pyro name of source volume:v, target field: vel)    

- know your max density values !!! For shading
- use open CL (advanced in solver)  



### Combustion:

| Combustion model |
| - |
|0 Source emit fuel > which is ignited > produce flames and smoke > expand flames    
|1 Check if temp is high enough to ignite (shelf will set up) (how fast smoke and flames will rise )        
|2 Set burn = `fuel * burn rate` (how fast consume 1 is 1sek. have effect in amount of smoke/flames)     
|3 Generate smoke  = `burn * sooterate`     
|4 Set heat - `max(heat*burn)`   
|5 Divergence =  `burn * gad release * burn influence`   gad release - how rapidly smoke expand  
|6 Increse temp `burn*heatoutput`    
|7 Reduce fuel by `burn*(1-fuelinneffciency)` fuelinneffciency - how much fuel is actually burned   

---


# Solver
## [PYRO Solver] DOP

1. OBJECT   
2. PRE-SOLVE   
3. VELOCITY   
4. ADVECTION    
5. SOURCE   


### Simulation:
`Temperature difusion` - how temperature blur  
`Bouyancy`  - lift up



#### Flame
`Flame height` - Control flame culling (high values bigger flames  
`Culing field` > `temperature` - Fine adjustment   
#### Smoke
no smoke - no density .   
`create dense smoke` - for vulcans. Heavy smoke, higher than one    
`source` - default from `heat`  
`smoke amount` - 1    
`heat cutoff` - smoke is produced onlyh in tip where heat is low. Higher value, , more smoke in between    

**Gas**   - `combustion` - for expantion    
**Temperature** - `contribution`    
#### Fuel
`Slow affect fuel` - can be lift by flames and burn in the air    
### Shape:

#### dissipation
make smoke evaporate (  higher > quicker)   
#### disturbance
detail noise to velocity. blocklsize-size of detail   
#### turbulence
 general noise on whole  sim  sizae i H units   
#### shredding   
stretch small - y big - x of gradien temp    
#### sharopnes  
#### confinement  
vortex like sworl motion       


### Color:



#nodes
## [Smoke Object]  DOP
- container that stroe volumes  set SOP paths  for vdb (fog) volumes


temperature  (temp needed for ignition)
fuel
Div...
Burn
Heat
Velocuty
	 - you can override scale o fvolume

# Source
## [Source Volume]
- source somoke
- set sop path: `opinputpath("../",0)`

#### apply data (1op:)
- op 1 pod smoke obj znajdziesz ja za pomoca `sop geometry` wpietym w bar po prawej   
- need to change apply in all frames (constantly): Initial, set always, set default, set never (should fetch )


# Microsolvers

## [Gas resize fludi dynamic] DOP  
2op   
- voxel that have almost 0 will delete and clean / initialisation dynamic when should follow moving source.   
- automatic sim bounds

## [Gas Dissipation]  DOP
3op - znikanie   
- diffusion is blur
- evaporation rate. is: Substarct (1 - remove 100% smoke in a 1sec (0.7 liuve a littlebit ))

## [Gas Disturbance]  DOP  
3op  
take edges of sim and disturb to get granual details.
- cutoff - how low of density or other reference volume shoud be in value to make it active

## [Gas resize fluid dynamic]  DOP
2op  




# Sourcing


## [Pyro Source] SOP

- initialize
 	- sourse fuel
	-source smoke will add  `density` and  `temperature`fields
- mode
	- from surface
	- keep input if points

### rasterize attributes  

### trails sop
- compute velocity

NEW SOURCE :
vdb with Fog volume named: density
http://www.sidefx.com/docs/houdini/pyro/pyro_look.html  
https://ceyhankapusuz.com/2017/01/09/houdini-micro-solvers-1/
