---
title: UE Materials
description: PBR
categories:
 - RT
tags:
- Unreal
- Rendering
- Real Time
- Shaders
- Game Dev

permalink: /ue_mat/
---



## Shading modes


|Lighting Mode | PS VS | Cost |  Usage|
|-- | -- | -- | -- |
|.


###### Motion Vectors

https://www.sidefx.com/tutorials/create-motion-vectors-for-time-warping-image-sequences/


###### 6D Lightmaps.

###### Biplanar projection:    

https://www.shadertoy.com/view/ws3Bzf     
https://iquilezles.org/www/articles/biplanar/biplanar.htm   


IOR: most dielectrics 1.5.

Unreal simplified disney model


# Material

Material models:

Metallic / Specular setups


## Albedo

Mat | Albedo int U4 | Lagarde tut (linear space)| Control Game |
-- | -- | -- |-- |
Neutral Gray | .5 | (128, 128, 128)
Middle Gray |  .18 | (46, 46, 46) | 186,186,186
Black Paint  ||| 56,56,56
Metallic  |  0.7 - 1 |
| ||
Bare soil | 0.13  | 0.17
Dry Clay Soil  |||  137,120,100
Green grass | 0.21 |  0.25
Desert sand | 0.36  | 0.40 | 177,167,132
Fresh snow | 0.81 |  0.80–0.90 | 243,243,243
|||
Fresh concrete | 0.51 |   0.55 | 192,191,187
Charcoal / Fresh asphalt | 0.02 | 0.04
Worn asphalt | 0.08 | 0.12
Old Concrete  |||  135,136,131
Ocean Ice | 0.56 | 0.5–0.7




## Spec / Refraction

- Dielectric F0 Reflectance `Value = ( (1 - IOR) / (1 + IOR) )²` (0.08 = UE4 Specular Reflectivity Value)


Mat | specular U4 | Index of Refraction (IOR) |  
-- | -- | -- |
COMON | 0.5 | 1.5
Air | | 1
Ice | 0.224 | 1.31
Water  |  0.255 | 1.33
Milk | 0.277 | 1.350
Skin | 0.35 |  
Glass | 0.5 | 1.52
Plastic | 0.5 | 1.460
Quartz | 0.57 | 1.544 - 1.644
Diamond | | 2.42



## Roughness


>(Roughness here is coupled with the BRDF used by the Unreal engine 4, it may not be compatible with other engines)

https://seblagarde.wordpress.com/2011/08/17/feeding-a-physical-based-lighting-mode/

## SSS
To use this feature, enable Burley in the Subsurface Profile and set the Editor Preview Level to Cinematic. If you're already using Separable SSS profile, minimal changes are required to switch to this method. Note that Burley SSS requires Temporal Anti-Aliasing to work properly.


## Translucency



Lighting Mode | Ps/Vs | Cost |  Usage|
-- | -- | -- | -- |
Volume Non Directional| pixel | cheapest pixel|
Volume Directional | pixel ||
Volume Per-Vertex Non Directional| vert | cheapest vert|
Volume Per-Vertex Directional| vert||
Surface Translucency Volume ||low per pixel but blurry | glass, water
Surface forward Shading| forward |most expensive. Each light per pixel| glass, water


**Thin Transparent** shading model and material expression, you are able to accurately represent tinted and colored transparent material



## paralax / wpo

https://youtu.be/kxsQ5m2IAXs



https://marmoset.co/posts/physically-based-rendering-and-you-can-too/
