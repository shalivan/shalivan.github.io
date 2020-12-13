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

- Add Subtract - masks, good transitions   TOP: gradient , bottom pattern
- Overlay -  Smoother than addsub. less useful for mask, for blend height car about 50%, bottom gradient
- Min, Max - boolean in heights  cz wspola/ Blend!!!

---

# Heightfields
#### Building
- `Noise`  
- `Project`  
- `Distort` : by noise or layer  
- `Terrace`
- `Flow Lines` :  - Simple version that create Water flow  - Wain Amount / density  Spread Smooth  (Adjust Height - Add to H.)


#### Layers

#### Change size
- `Remap` - change H (Y)  
- `Crop` - change X,Z  
- `Transform` - move / scale  
- `Resample` - dense  



### Export

- `Heightfield Output` > convert to image   
- `Convert`  


---

# Erosion
Erosion create Voxel grids:
- `mask`
- `sediment` (osady) - yellow
- `bedrock` (podłoże) - violet
- `debris` - orange
- `water`  - green

**Global Erosion**, **Erodability** & **Erosion rate** -   are multiplayers

||| ||
|---|---|---|---|
<img src="/src/hou/heightfields/0001.png" width="150"> | <img src="/src/hou/heightfields/0002.png" width="150"> | <img src="/src/hou/heightfields/0003_2k.png" width="150">   | <img src="/src/hou/heightfields/0003.png" width="150">  
|Resample  256 | 1024 | 2048 | 4096
<img src="/src/hou/heightfields/size_0001.png" width="150"> | <img src="/src/hou/heightfields/size_0002.png" width="150"> | <img src="/src/hou/heightfields/size_0003.png" width="150">   | <img src="/src/hou/heightfields/size_0004.png" width="150">  
|Rescale  100 (.1 of orginal) | 200 (.2) | 1000 (1) | 5000 (5)






## Hydro

|Hydro only default |Erodability x4| Riverbed x4 only|Riverbank x4 only|
|---|---|---|---|
|<img src="/src/hou/heightfields/hydro/0004.png" width="150" align="center"  >|<img src="/src/hou/heightfields/hydro/0006.png" width="150" align="center"  >|<img src="/src/hou/heightfields/hydro/0007.png" width="150" align="center"  >|<img src="/src/hou/heightfields/hydro/0009.png" width="150" align="center"  >


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

##### Riverbank (brzeg)
**Max Bank To Water Ratio** -  




## Thermal  



||no erosion| erosion 1|erosion 4|
|---|---|---|---|
||<img src="/src/hou/heightfields/0000.png" width="150" align="center"  > |<img src="/src/hou/heightfields/thermal/0011.png" width="150" align="center"  >| <img src="/src/hou/heightfields/thermal/0012.png" width="150" align="center"  >  


Heat based. mostly about mountaintops    
**Cut Angle** -  Threshold angle. (Angle grater than value will be considered as erodible )(0 for more sand soft tops, 90 low erosion)   

#### Thermal Advanced
**Remove Rate** - (-1 - Add more debris , +1 Remove debris )  
**Max Debris Depth** -   
**Grid Bias** -   change values per angle

|.| -1 debris remain on ground |debris remain on slopes +1 ||
|---|---|---|---|
| **Grid Bias** |<img src="/src/hou/heightfields/thermal/0014.png" width="150" align="center"  >| <img src="/src/hou/heightfields/thermal/0015.png" width="150" align="center" >  

|**Remove Rate**|<img src="/src/hou/heightfields/thermal/0016.png" width="150" align="center"  >| <img src="/src/hou/heightfields/thermal/0017.png" width="150" align="center" >  | <img src="/src/hou/heightfields/thermal/0018.png" width="150" align="center" >  
|0.7 / -1/ 0|

## Precipitation (opad)
**Precipitation** - How much water.  High to erode quicker.  (AMOUNT)   
**Density** - how much   low: more lines hi: wide and rear lines - High to erode quicker  (AMOUNT)   
**Evaporation rate** - how much water to sink    


||Amount 0.3 |Amount 0.6|Rate 0.5 |
|---|---|---|---|
**Density** 0.05|<img src="/src/hou/heightfields/precipitation/0021.png" width="150" align="center"  >|<img src="/src/hou/heightfields/precipitation/0022.png" width="150" align="center"  >|<img src="/src/hou/heightfields/precipitation/0024.png" width="150" align="center"  >
**Density** 0.6  |<img src="/src/hou/heightfields/precipitation/0019.png" width="150" align="center"  >|<img src="/src/hou/heightfields/precipitation/0020.png" width="150" align="center"  >|<img src="/src/hou/heightfields/precipitation/0023.png" width="150" align="center"  >



## Water Flow


## Debris Flow
**Spread Itter** - 4 low -fine lines , 15-20 - is middle ,   hi - large chunks of sand   (AMOUNT)   
**Max Height** - how height debris can build up - high value can create interesting cliff pattern (bolders?)  

lobes - płaty  

default thermal


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




  ```
  ||||||
  |--|--|--|--|--|
  |**Bank Angle** 30 85| Threshold angle. (Low values will make erosion on flatter planes more erosion with longer slopes and expanded riverbed)    | <img src="/src/hou/heightfields/hydro/003.png">  | <img src="/src/hou/heightfields/hydro/004.png">  
  |**Spread Itterations** 20 - 60  |(high: longer slopes and expanded riverbed)     | <img src="/src/hou/heightfields/hydro/005.png">  | <img src="/src/hou/heightfields/hydro/006.png">  
  Erosion rate main | | <img src="/src/hou/heightfields/hydro/001.png">  | <img src="/src/hou/heightfields/hydro/002.png">  
  ||**Hydro Advanced**
  |**Removal Rate** | How much of debris to remove (-1 Accumulate a lot), (1 - Cuts but not debris)     |
  |**Max Depth** | Stop when debris reach level      |
  |**Grid Bias** | (-1 Sand on the Ground), (1- Leave sand on cliffs/slopes) Bias angles    |
  ||Erodibility Adjustment
  |**Ramp-up Iterarions** | How many itters before full erosion (0 - Immediately)      |
  |**Initial factor** | Strength of erosion in initial movement      |
  |**Slope Factor** | (0 - Everything, will erode),  (0.8) Less erosion (stip lot of, shallow little)   |  
  ||Riverbed  (koryto)
  |**Erosion Rate Factor** 0.2 - 0.6  |
  |**Deposition Rate** | Removal rate     |
  |**Sediment Capacity** |  How much debris can be carry by sediments down (pojemność osadów)  |
  |**Riverbank:** (brzeg)|
  ```



  ```


  0
  1 2 3 - resolutions
  4 - hydro 1
  5 - ------tes off riversite and rivebet x0
  6 - hydro/erodability 4                vvvvvvvvvv
  7 - hydro advanced/ riverbed 4        vvvvvvvvvvvvv
  8 ------------------------------------- same rest others
  9 - hydro advanced / riverbank 4        vvvvvvvvvvv
  10 -------------------------------- same rest others



  - termal 1
  - ----------------------      global 4
  -  termal / erodability  4
  - grid bias - 14
  - grid + 15

  16
  17
  18

  on multi 4 opad:

  19 - am 0.3, dens 0.05 . rate 0.04
20 - am 0.6, dens 0.05 . rate 0.04
  21 - am 0.3, dens 0.6 . rate 0.04
  22- am 0.6, dens 0.6 . rate 0.04
  23- am 0.6, dens 0.05 . rate 0.5
  24- am 0.3, dens 0.6 . rate 0.5

  ```
