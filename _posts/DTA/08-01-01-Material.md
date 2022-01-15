---
title: Material Data
description: PBR
categories:
 - DTA
tags:
- Unreal
- Rendering
- Real Time
- Shaders
- Game Dev
permalink: /matdata/
---
[Camera](/camera/)    
[Algebra](/algebra/)
[Rendering](/rendering/)

----






## Albedo
sRGB

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

Everything has fresnel and reflections !
http://filmicworlds.com/blog/everything-has-fresnel/


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

- **Microfacets models** how rough (in microscale)  mat is (amp & freq of bumps in material ) tiny imperfections in mat  & angle of incoming light
- Dielectric F0 Reflectance `Value = ( (1 - IOR) / (1 + IOR) )²` (0.08 = UE4 Specular Reflectivity Value)

Water:
Total internal refl - speed of light in mat to speed of light oudisde.....   IRO
- from top only go inside
- low light reflect
AIR speed of light > 1.0 iro
speed of light in water slower
so AIR to water 1.33


## Metal
Mat |  |
-- | -- |
Conductors | 1  
Dielectrics | 0

- **Conductors** Spec and glossy refl, in conductors typicaly metlas. dep on wave len (yellow gold) (reflect most light and turn non reflected into heat)
- **Dielectrics** - (BTDF shader ie) reflected and refracted (IOR,bend ing rays on medium change) sometimes scatter (as subsurf) and flat ss is difuse
`Conductors` - (tyupicly reflect depend on wave leng. give color)  
`Dielectrics` - (refl + refract + scatter refracted (subsurf but rather difuse ))   
Refl + refr >> have fresnel.
