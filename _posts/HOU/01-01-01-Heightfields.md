---
title: Heightfields

categories:
 - HOU
tags:
- Houdini
- SOP
description: Houdini landscape 2d fields.
permalink: /heightfields/
---




[Lanscape.hiplc](/src/hip/SOP Lanscape.hiplc)



---

# Principles
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
- FlowLines:  - Simple version that create Water flow  - Wain Amount / density  Spread Smooth  (Adjust Height - Add to H.)

#### Masking
- by features - Slope / Height / Peaks / Dir / Occlusion   
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



<img src="/src/hou/heightfields/021.png" width="350" align="center"  >  
<img src="/src/hou/heightfields/015.png" width="350" align="center"  >  
<img src="/src/hou/heightfields/016.png" width="350" align="center"  >  




## Hydro


<img src="/src/hou/heightfields/021.png" width="350" align="center"  >  
<img src="/src/hou/heightfields/hydro/018.png" width="350" align="center"  >  
<img src="/src/hou/heightfields/hydro/017.png" width="350" align="center"  >  


**Bank Angle** - Threshold angle. (Low values will make erosion on flatter planes more erosion with longer slopes and expanded riverbed)  
**Spread Itterations** - (high: longer slopes and expanded riverbed)    

#### Hydro Advanced  
**Removal Rate** - How much of debris to remove (-1 Accumulate a lot), (1 - Cuts but not debris)    
**Max Depth** - Stop when debris reach level     
**Grid Bias** - (-1 Sand on the Ground), (1- Leave sand on cliffs/slopes) Bias angles    

##### Erodibility Adjustment
**Ramp-up Iterarions** -  How many itters before full erosion (0 - Immediately)     
**Initial factor** - Strength of erosion in initial movement     
**Slope Factor** - (0 - Everything, will erode),  (0.8) Less erosion (stip lot of, shallow little)     

##### Riverbed  (koryto)
**Erosion Rate Factor** -     
**Deposition Rate** - Removal rate     
**Sediment Capacity** -  How much debris can be carry by sediments down (pojemność osadów)  

**Riverbank:** (brzeg)


||||||
|--|--|--|--|--|
**Bank Angle** | Threshold angle. (Low values will make erosion on flatter planes more erosion with longer slopes and expanded riverbed)  | 30 85 | <img src="/src/hou/heightfields/hydro/003.png">  | <img src="/src/hou/heightfields/hydro/004.png">  
**Spread Itterations** |(high: longer slopes and expanded riverbed)     |20 - 60  | <img src="/src/hou/heightfields/hydro/005.png">  | <img src="/src/hou/heightfields/hydro/006.png">  
#### Hydro Advanced  
**Removal Rate** | How much of debris to remove (-1 Accumulate a lot), (1 - Cuts but not debris)     |
**Max Depth** | Stop when debris reach level      |
**Grid Bias** | (-1 Sand on the Ground), (1- Leave sand on cliffs/slopes) Bias angles    |
##### Erodibility Adjustment
**Ramp-up Iterarions** | How many itters before full erosion (0 - Immediately)      |
**Initial factor** | Strength of erosion in initial movement      |
**Slope Factor** | (0 - Everything, will erode),  (0.8) Less erosion (stip lot of, shallow little)   |  
##### Riverbed  (koryto)
**Erosion Rate Factor** |  | 0.2 - 0.6  | <img src="/src/hou/heightfields/hydro/001.png">  | <img src="/src/hou/heightfields/hydro/002.png">  
**Deposition Rate** | Removal rate     |
**Sediment Capacity** |  How much debris can be carry by sediments down (pojemność osadów)  |
**Riverbank:** (brzeg)|








7 8
riverbank0.5
2


9 10
riverbet rate factor 0.5
2


11 12
deposition 0.001
0.1


13 14
???deposition 0.001
erodablilty: slope  0.4




## Thermal  

<img src="/src/hou/heightfields/021.png" width="350" align="center"  >  
<img src="/src/hou/heightfields/thermal/020.png" width="350" align="center"  >  
<img src="/src/hou/heightfields/thermal/019.png" width="350" align="center"  >  


Heat based. mostly about mountaintops    
**Cut Angle** -  Threshold angle. (Angle grater than value will be considered as erodible )(0 for more sand soft tops, 90 low erosion)   

#### Thermal Advanced
**Remove Rate** - (-1 - Add more debris , +1 Remove debris )  
**Max Debris Depth** -   
**Grid Bias** - change values per angle (- debris remain on ground + debris remain on slopes )  (lower : more on bottom)   

#### Precipitation (opad)
**Precipitation** - How much water.  High to erode quicker.  (AMOUNT)   
**Density** - how much   low: more lines hi: wide and rear lines - High to erode quicker  (AMOUNT)   
**Evaporation rate** - how much water to sink    

#### Water Flow


#### Debris Flow
**Spread Itter** - 4 low -fine lines , 15-20 - is middle ,   hi - large chunks of sand   (AMOUNT)   
**Max Height** - how height debris can build up - high value can create interesting cliff pattern (bolders?)  

lobes - płaty  



default thermal

-------------



1 2
erosion rate 0.2
0.6



4 3
bank angle 30
85




5 6
spreed 20
60



7 8
riverbank0.5
2


9 10
riverbet rate factor 0.5
2


11 12
deposition 0.001
0.1


13 14
???deposition 0.001
erodablilty: slope  0.4





BOTH DEFAULT
BOTH 3
hydro 3
hydro 1
thermal 3
thermal 1
00000000 21


---

# Unreal

.r16


#### Landscape Size

||||
|-|-|-|
SectionSize|7x7 LOD sections more aggressively at a higher CPU cost.|256x256 fewer components and is less costly on the CPU. (for large landscapes)  
Sections per component| 1x1 reduced CPU calculation time too many vertices at once | 2x2  possible that one component could be rendering four different LOD's |
num components| Tiles count  |  
Overal resolution|final size  1+(SectionSize * NumOfComp * Sectionspercomp)

#### Height

512 jednostek w unrealu. 256 up + 256 down

 -256 to 255.992 and stored with 16 bit precision. multiplied by the Z

  scale value of 1 results in a maximum height of roughlty 256 centimeters (cm) and a maximum depth of -256cm. Therefore, at the default Z scale value of 100 your height values with be between 256 meters (m) and -256m.
