---
title: Material Data
description: PBR
categories:
  - DTA
tags:
  - Unreal
  - Rendering
  - Shaders
  - RealTime
  - GameDev
permalink: /matdata/
aliases:
  - matdata
---

Corelated pages:

[Camera](/camera/)    
[Algebra](/algebra/)
[Rendering](/rendering/)
[Substance Designer](/substancedesigner/) / [[16-02-01-Substance_Designer|substancedesigner]]

[[11-01-01-Math|math]]


----
- albedo > refract
- sharpness of reflection > reflect
	- reflection on angle is more sharp and visible (fresnel)
- metal pure reflection > only refraction (or absorbed [heat]) > only mat that tint reflection  (but saturate with Fresnel)
- variance in reflection >

https://substance3d.adobe.com/tutorials/courses/the-pbr-guide-part-2
https://seblagarde.wordpress.com/2014/04/14/dontnod-physically-based-rendering-chart-for-unreal-engine-4/

# PBR 
Energy conservation 
Eyes are less sensitive in dark. 


**sRGB** - mid gray in middle (perceptual display of blacks)
**Linear RGB** - image is brighter (black are crushed into small range)
- Linear space value (0.5) converted to a gamma space rgb value: `0.5`^(1 / 2.2) = ~0.73 * 255 = `186`

sRGB to Liner
```
If (0 ≤ S ≤ 0.04045):  
    L = S/12.92  
Else (0.04045 < S ≤ 1):  
    L = ((S+0.055)/1.055)^2.4
```
Linear to sRGB 
```
 If (0 ≤ L ≤ 0.0031308):  
     S = L * 12.92  
 Else (0.0031308 < L ≤ 1):  
     S = 1.055*L^(1/2.4) - 0.055
```

### Workflow
##### Metal / Roughness 
A byproduct of using the metal/roughness workflow is that it can produce a white edge artifact,
- white artefacts on blend

##### Specular/glossiness
- dark artefacts on blend

# Render passes

## Albedo / Reflectance
Diffuse **reflected color** for dielectric and **reflectance** value for metals 
Flat lower contrast and brighter than normal photo. 

##### Dielectrics
`50` - `245` (sRGB)
`0.02` - `0.9` (Linear RGB)

##### Metal 
`180` / `186` - `255` (sRGB) 
`70` - `100%` specular

| Mat | Linear | Linear byte | sRGB | (R^2.2+G^2.2+B^2.2)/3 |
| ---- | ---- | ---- | ---- | ---- |
| Max WHITE | `0.893` | (229,229,229) | `0.95` | `240` - `249` |
| Neutral Gray (bright) | `0.5` | (128,128,128) | `0.72` | `186` |
| Middle Gray | `0.18` | (46,46,46) | `0.5` | `128` |
| Black Paint | `0.02` | (5,5,5) | `0.169` | `43` |
| Max BLACK | `0.01` - `0.027` | (7,7,7) | `0.117` - 0`.195` | `30` - `50` |
|  |  | 243,243,243 |  |  |
| White paint / Fresh snow | `0.81` (`0.80` - `0.90`) |  |  | 230 |
| Coal / Carbon / Fresh asphalt | `0.02` - `0.04` |  |  |  |
|  |  |  |  |  |
| Worn asphalt | `0.08`- `0.12` |  |  |  |
| Fresh concrete | `0.51` - `0.55` | 192,191,187 |  |  |
| Old Concrete |  | 135,136,131 |  |  |
| Ocean Ice | `0.56` ( `0.5` - `0.7`) |  |  |  |
|  |  |  |  |  |
| Rock | `0.3` - `0.4` |  |  | `148` - `168` |
| Limestone | `0.3` - `0.45` |  |  | `148` - `177` |
| Sandy Soil Dry | `0.25` - `0.45` |  |  | `136` - `177` |
| Silt loam soil. Dry | `0.23` - `0.28` |  |  | `131` -`143` |
| Clayy soil, dry | `0.23` - `0.4` | 137,120,100 |  | `131` - `168` |
| Bare soil | `0.13` - `0.17` |  |  | `114` |
| Yello Clay | `0.16` |  |  | `111` |
| Grey soil.  (wet-dry) | `0.1` - `0.3` |  |  | `90` - `148` |
| Black soil, (wet-dry) | `0.08` - `0.15` |  |  | `81` - `108` |
| Desert sand | `0.36`  -` 0.40` | 177,167,132 |  |  |
|  |  |  |  |  |
| Green grass | `0.2` -  `0.25` |  |  | `123` - `136` |
| Tundra | `0.2` |  |  | `123` |
| Tall wild grass | `0.16` - `0.18` |  |  | `111` - `117` |
| Tea bushes | `0.16` - `0.18` |  |  | `111` - `117` |
| Corn field | `0.16` - `0.17` |  |  | `111` - `114` |
| Deciduous trees | `0.15` - `0.18` |  |  | `108` - `117` |
| Autumn foliage | `0.15` - `0.3` |  |  | `109` -`148` |
| Grain crops | `0.1` - `0.25` |  |  | `90` - `136` |
| Moss | `0.1` |  |  | `90` |
| Fummer Foliage | `0.09` - `0.12` |  |  | `85` |
| Conifer Forest | `0.08` - `0.12` |  |  | `81` |
| Leaves (wet-dry) | `0.07` - `0.2` |  |  | `75` - `123` |
|  |  |  |  |  |
| Batten planks (fresh wood) | `0.35` - `0.42` |  |  | `158` - `172` |
| Batten planks (old weathered) | `0.12` - `0.16` |  |  | `97` - `111` |
| Varnished wood | `0.13` |  |  | `101` |
| Bark, oak | `0.1` |  |  | `90` |
|  |  |  |  |  |
| Water sun near horizon | `0.5` - `0.8` |  |  |  |
| Water sun near zenith | `0.05` |  |  |  |
|  |  |  |  |  |
| Skin European | 0.35 - 0.6 |  |  | 158 - 202 |
| Skin Indian | 0.15 - 0.3 |  |  | 108 - 148 |
| Skin African  | 0.05 - 0.15 |  |  | 65 - 108 |
|  |  |  |  |  |


## Specular
**F0** values 0-8%. Default value is .05 (which is 4% reflective)
Let the value be default 0.5 and apply a cavity map to darken cavities.

- Dielectric F0 Reflectance `Value = ( (1 - IOR) / (1 + IOR) )²` (0.08 = UE4 Specular Reflectivity Value)
Fresnel reflection coefficient mount of light that reflects off a surface when the viewing angle is perpendicular (i.e., the angle of incidence is 0 degrees).



## Roughness
**Microfacets models** how rough (in microscale)  mat is (amp & freq of bumps in material ) tiny imperfections in mat  & angle of incoming lightEverything has Fresnel and reflections ! [YT link](http://filmicworlds.com/blog/everything-has-fresnel/)
The specular part of Disney “principled” BRDF is a GGX BRDF. It use a roughness parameter.
Nm is crucial! 
more direct reflection and depends heavily on the viewing angle relative to the light source and the surface normal.

| Mat |  UE |
| ---- | ---- |
| COMON | 0.5 |
| Air |  |
| Ice | 0.224 |
| Water | 0.255 |
| Milk | 0.277 |
| Skin | 0.35 |
| Glass | 0.5 |
| Plastic | 0.5 |
| Quartz | 0.57 |
| Diamond |  |


## Metal
|Mat |  |
|-- | -- |
|Conductors | 1  
|Dielectrics | 0

- **Conductors** Spec and glossy refl, in conductors typicaly metlas. dep on wave len (yellow gold) (reflect most light and turn non reflected into heat)
- **Dielectrics** - (BTDF shader ie) reflected and refracted (IOR,bend ing rays on medium change) sometimes scatter (as subsurf) and flat ss is difuse
`Conductors` - (tyupicly reflect depend on wave leng. give color)  
`Dielectrics` - (refl + refract + scatter refracted (subsurf but rather difuse ))   
Refl + refr >> have fresnel.


# Advanced Render passes

## Refraction 

| Mat |  | Index of Refraction (IOR) |
| ---- | ---- | ---- |
| COMON |  | 1.5 |
| Air |  | 1 |
| Ice |  | 1.31 |
| Water |  | 1.33 |
| Milk |  | 1.350 |
| Skin |  |  |
| Glass |  | 1.52 |
| Plastic |  | 1.460 |
| Quartz |  | 1.544 - 1.644 |
| Diamond |  | 2.42 |


```
Water:
Total internal refl - speed of light in mat to speed of light oudisde.....   IRO
- from top only go inside
- low light reflect
AIR speed of light > 1.0 iro
speed of light in water slower
so AIR to water 1.33
```


## SSS
### Anisotropy 
