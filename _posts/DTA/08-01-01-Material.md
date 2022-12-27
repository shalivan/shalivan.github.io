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

https://substance3d.adobe.com/tutorials/courses/the-pbr-guide-part-2

https://seblagarde.wordpress.com/2014/04/14/dontnod-physically-based-rendering-chart-for-unreal-engine-4/

Dielectrics


Metal / Roughness Workflow - A byproduct of using the metal/roughness workflow is that it can produce a white edge artifact,
 specular/glossiness workflow -


## Albedo

0.5^(1 / 2.2) = ~0.73 * 255 = 186

This is the equation for getting a linear space value (0.5) converted to a gamma space rgb value (186)





Albedo in linear spce (0.02-.9 ) as unreal editor expect.
Albedo range
30-240 sRGB
50-249 sRGB (strict Range)
50-243 !!!!!


Mat | Linear  | in byte ranges | gamma / sRGB (darker)||
-- | -- | -- |-- |-- |
Max WHITE |0.893| (229,229,229) | 0.95 |(243,243,243) 240-249
Neutral Gray (bright) |0.5| (128,128,128)| 0.72 |(186,186,186)
Middle Gray |  0.18  | (46,46,46)  | 0.5 |(128,128,128)
Black Paint  | 0.02  | (5,5,5) | 0.169 |(43,43,43)
Max BLACK | 0.01 - 0.027 | (7,7,7) | 0.117 - 0.195 | (50,50,50) 30-50
| ||
Bare soil | 0.13 - 0.17  |
Dry Clay Soil  ||  137,120,100
Green grass | 0.21 -  0.25
Desert sand | 0.36  - 0.40 | 177,167,132
Fresh snow | 0.81 -  0.80–0.90 | 243,243,243
|||
Fresh concrete | 0.51 - 0.55 | 192,191,187
Charcoal / Fresh asphalt | 0.02 - 0.04
Worn asphalt | 0.08- 0.12
Old Concrete  ||  135,136,131
Ocean Ice | 0.56 - 0.5–0.7

The reflectance part (the one use by metallic) must be in the range 186-255  

## Spec / Reflectance
There is no chart for the reflectance value of the Unreal engine 4, just let the value by default and apply a cavity map on it.

## Roughness
Roughness
The specular part of Disney “principled” BRDF is a GGX BRDF. It use a roughness parameter.


## Spec / Refraction
Specularity refers to the amount of specular light reflected by a surface. This value is inherent to the Material type, and usually the default value of 0.5 is accurate.

Unreal Engine uses a default Specular of 0.5, which represents approximately 4% specular reflection.


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
