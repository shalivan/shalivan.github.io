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

> Pxlink: [Camera](/camera/)  / [Algebra](/algebra/) /[Rendering](/rendering/) / [Substance Designer](/substancedesigner/) / [[16-02-01-Substance_Designer|substancedesigner]]
> Obsidian: [[DTA]] [[11-01-01-Math|Math]]  / [[15-01-01-Shading|Shading]]


# Render passes

## Albedo / Reflectance
Diffuse **reflected color** for dielectric and **reflectance** value for metals 
Flat lower contrast and brighter than normal photo. 

##### Dielectrics
`50` - `245` (sRGB)
`0.02` - `0.9` (Linear RGB)

##### Metal 
`180` / `186` - `255` (sRGB) 
`0.7` - `1` specular

| Mat | Linear | Linear byte | sRGB |
| ---- | ---- | ---- | ---- |
| White | `0.893` | 229,229,229 | `240` - `249` (`0.95`) |
| Gray (Zone V) | `0.18` | 46,46,46 | `128` (`0.5`) |
| Black | `0.01` - `0.027` | 7,7,7 | `30` - `50` (`0.117` - `0.195`) |
|  |  |  |  |
| White paint / Fresh snow | `0.81` (`0.80` - `0.90`) | 243,243,243 | `230` |
| Brright Gray | `0.5` | 128,128,128 | `186` (`0.72`) |
| Black Paint | `0.02` | 5,5,5 | `43` (`0.169`) |
| Coal / Carbon / Fresh asphalt | `0.02` - `0.04` |  |  |
| **CONCRETE** |  |  |  |
| Fresh concrete | `0.51` - `0.55` | 192,191,187 |  |
| Worn asphalt | `0.08`- `0.12` |  |  |
| Old Concrete |  | 135,136,131 |  |
| **ROCK** |  |  |  |
| Limestone | `0.3` - `0.45` |  | `148` - `177` |
| Rock | `0.3` - `0.4` |  | `148` - `168` |
| **SOIL** |  |  |  |
| Sandy Soil | `0.25` - `0.45` Dry |  | `136` - `177` |
| Desert sand | `0.36`  -` 0.40` | 177,167,132 |  |
| Clay Soil | `0.23` - `0.4` Dry | 137,120,100 | `131` - `168` |
| Grey soil | `0.1`  Wet  `0.3` Dry |  | `90` - `148` |
| Silt loam Soil | `0.23` - `0.28` Dry |  | `131` -`143` |
| Bare soil | `0.13` - `0.17` |  | `114` |
| Yellow Clay | `0.16` |  | `111` |
| Black soil | `0.08` Wet  `0.15` Dry |  | `81` - `108` |
| **FOLIAGE** |  |  |  |
| Green grass | `0.2` -  `0.25` |  | `123` - `136` |
| Tundra | `0.2` |  | `123` |
| Tall wild grass | `0.16` - `0.18` |  | `111` - `117` |
| Tea bushes | `0.16` - `0.18` |  | `111` - `117` |
| Corn field | `0.16` - `0.17` |  | `111` - `114` |
| Deciduous trees | `0.15` - `0.18` |  | `108` - `117` |
| Grain crops | `0.1` - `0.25` |  | `90` - `136` |
| Moss | `0.1` |  | `90` |
| Summer Foliage | `0.09` - `0.12` |  | `85` |
| Autumn foliage | `0.15` - `0.3` |  | `109` -`148` |
| Conifer Forest | `0.08` - `0.12` |  | `81` |
| Leafs | `0.07` Wet  `0.2` Dry |  | `75` - `123` |
| **WOOD** |  |  |  |
| Batten planks (fresh wood) | `0.35` - `0.42` |  | `158` - `172` |
| Batten planks (old weathered) | `0.12` - `0.16` |  | `97` - `111` |
| Varnished wood | `0.13` |  | `101` |
| Bark, oak | `0.1` |  | `90` |
| **WATER** |  |  |  |
| Ocean Ice | `0.56` ( `0.5` - `0.7`) |  |  |
| Water sun near horizon | `0.5` - `0.8` |  |  |
| Water sun near zenith | `0.05` |  |  |
| **SKIN** |  |  |  |
| Skin European | `0.35` - `0.6` |  | `158` - `202` |
| Skin Indian | `0.15` - `0.3` |  | `108` - `148` |
| Skin African | `0.05` - `0.15` |  | `65` - `108` |



## Specular
**Dielectric F0 Reflectance** Unreal values 0-8%. Default value is .05 (which is 4% reflective)  `Value = ( (1 - IOR) / (1 + IOR) )²` 
Fresnel reflection coefficient mount of light that reflects off a surface when the viewing angle is perpendicular (i.e., the angle of incidence is 0 degrees).

Let the material value in unreal be default 0.5 and multiply by a cavity map to darken cavities.


## Roughness
**Microfacets models** how rough (in microscale)  mat is (amp & freq of bumps in material ) tiny imperfections in mat  & angle of incoming lightEverything has Fresnel and reflections ! [YT link](http://filmicworlds.com/blog/everything-has-fresnel/)
The specular part of Disney “principled” BRDF is a GGX BRDF. It use a roughness parameter.
Nm is crucial! 
more direct reflection and depends heavily on the viewing angle relative to the light source and the surface normal.
- reflection on angle is more sharp and visible

| Mat |  UE |
| ---- | ---- |
| COMON | `0.5` |
| Air |  |
| Ice | `0.224` |
| Water | `0.255` |
| Milk | `0.277` |
| Skin | `0.35` |
| Glass | `0.5` |
| Plastic | `0.5` |
| Quartz | `0.57` |
| Diamond |  |

## Metal
| Mat |  |
| ---- | ---- |
| Conductors | `1` |
| Dielectrics | `0` |
| Diamond |  |

- **Conductors** Spec and glossy reflection, in conductors typically metals. dep on wave len (yellow gold) (reflect most light and turn non reflected into heat)
- **Dielectrics** - (BTDF shader ie) reflected and refracted (IOR,bend ing rays on medium change) sometimes scatter (as subsurf) and flat ss is difuse
`Conductors` - (typicly reflect depend on wave leng. give color)  
`Dielectrics` - (reflect + refract + scatter refracted (subsurf but rather difuse ))   
Refl + refr >> have fresnel.


# Advanced Render passes

## Refraction 
-  physical model of **Index of Refraction** - but you will have an offset that reads from off screen, shift material glitches can occure.   
- **Pixel Normal Offset** enables refraction for these large flat surfaces, like water,

| Mat |  | IOR |
| ---- | ---- | ---- |
| COMON |  | `1.5` |
| Air |  | `1` |
| Ice |  | `1.31` |
| Water |  | `1.33` |
| Milk |  | `1.35` |
| Skin |  |  |
| Glass |  | `1.52` |
| Plastic |  | `1.46` |
| Quartz |  | `1.544` - `1.644` |
| Diamond |  | `2.42` |


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

To use this feature, enable Burley in the Subsurface Profile and set the Editor Preview Level to Cinematic. If you're already using Separable SSS profile, minimal changes are required to switch to this method. Note that Burley SSS requires Temporal Anti-Aliasing to work properly.

### Anisotropy 

---

- metal pure reflection > only refraction (or absorbed [heat]) > only mat that tint reflection  (but saturate with Fresnel)