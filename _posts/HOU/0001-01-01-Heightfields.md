---
title: Heightfields

categories:
 - HOU
tags:
- Houdini
description: Houdini landscape 2d fields.
---



# Landscape modeling principles
Make in passes from:
- Low Massing: make a volume (bigger than end result)
- Low Add obstacles and disturbance for better erosion
- Low Layers to Erosion   
- Low erosion for massive (mid range) sculpts  
- Med geological formations like terracing
- High Erosion

#### Mix layers

|-|-|-|
|-|-|-|
|Add Subtract | masks, good transitions  | TOP: gradient , bottom pattern
|Overlay |  Smoother than addsub. less useful for mask, for blend height| car about 50%, bottom gradient
|Min, Max | boolean in heights | cz wspola/ Blend!!!

---

# Modeling
#### Building
- noise  
- project  
- distort : by noise or layer  
- terrace
- FlowLines:  - Simple version that create Water flow  - Wain Amount / dendity  Spread Smooth  (Adjust Height - Add to H.)

#### Masking
- by features - Slope/Heighr/ Peaks / Dir / Occlusion   
- mask by object  

#### Layers

### Export

heightfield_output > convert to image   
convert  

---

# Erosion
Erosion create Voxel grids: `mask`, `sediment` (osady), `bedrock` (podłoże), `debris`, `water`    
**Erodability** -    
**Erosion rate** -    

## Hydro
**Bank Angle** - Treshold angle. (Low values will make erosion on flatter planse more erosion with longer slopes and expanded riverbed)  
**Spread Itterations** - (high: longer slopes and expanded riverbed)    

#### Hydro Advanced  
**Removal Rate** - How much of debris to remove (-1 Acumulate a lot), (1 - Cuts but not debre)    
**Max Depth** - Stop when debris reach level     
**Grid Bias** - (-1 Sand on the Ground), (1- Leave sand on clifs/slopes) Bias angles    

##### Erodibility Adjustment
**Ramp-up Iterarions** -  How many itters before full erosion (0 - Imidietly)     
**Initial factor** - Strenght of erosion in initial movement     
**Slope Factor** - (0 - Everything, will erode),  (0.8) Less erosion (stip lot of, shallow little)     

##### Riverbed  (koryto)
**Erosion Rate Factor** -     
**Deposition Rate** - Removal rate     
**Sediment Capacity** -  How much debris can be cary by sediments down (pojemność osadów)  

**Riverbank:** (brzeg)

## Thermal  
Heat based. mostly about mountaintops    
**Cut Angle** -  Treshold angle. (Angle grater than value will be considered as erobdable )(0 for more sand soft tops, 90 low erosion)   

#### Thermal Advanced
**Remove Rate** - (-1 - Add more debris , +1 Remove debris )  
**Max Debris Depth** -   
**Grid Bias** - change values per angle (- debris remain on ground + debris remain on slopes )  (lowwer : more on bottom)   

#### Precipitation (opad)
**Precipitation** - How much water.  High to erode quicker.  (AMOUNT)   
**Density** - how much   low: more lines hi: wide and rear lines - High to wrode quicker  (AMOUNT)   
**Evaporation rate** - how much water to sink    

#### Water Flow


#### Debris Flow
**Spread Itter** - 4 low -fine lines , 15-20 - is middle ,   hi - large chunks of sand   (AMOUNT)   
**Max Height** - how height debry can build up - high value can create interesting clif pattern (bolders?)  

lobes - płaty  
