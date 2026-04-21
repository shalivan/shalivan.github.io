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
rock ref: https://www.alexstrekeisen.it/english/meta/maficgranulite.php
rock sudety: https://zywaplaneta.pl/granulity-sudety/

Related notes: [Color](/color/), [Rendering](/rendering/) 

{% comment %} [[DTA]] [[11-01-01-Math]]  / [[15-01-01-Shading]] {% endcomment %}


[Color theory bible](https://chrisbrejon.com/cg-cinematography/chapter-2-color-theory/)
[Convert colors calculator](https://davengrace.com/dave/cspace/)



# Substrate (Strata)
more expresive workflows, can combine 2 shaderws toghether No cost if input is not used ! 
Layer system - layering is expensive  if possible make with onslab 
Slab << is a material **matter responce to light**. = **interface** + **medium**
#### **G buffer** 
Gbuffer Format (projection)
`Adaptive` - packed data noi blend like decal ??? - play 5 & xboix series SM6 - pit packed uav to encod per pixel << full 
`Blendable` - not fully  but safe and low compatibility, ok for transition. 

https://youtu.be/KYmd_LNlw2c?t=2125



[YT unreal fest](https://youtu.be/G0h-5dQivI8) - Everything You Wanted to Know About Substrate(But Are Too Afraid to Ask)| Unreal Fest Stockholm 2025
[YT Render Bucket - UE5.7 Substrate – Next-Gen Shading Workflow Explained](https://youtu.be/Ghn-FvdaBBc) - 
[YT  Beyond Extent and Hugh Chew](https://youtu.be/Pbbu-wxCqnE)
https://youtu.be/4X-nZ7qflcw - base to advanced substrate 

![[Pasted image 20251127035117.png]]
## Slab BSDF 


`BSDF` - Bidirectional scattering distribution functions  -


## Monolithic
complex stand alone phenomena  non composible 
Volumetric 
Hair 
Eye 
Unlit, Single layer water.



Wyjątki: 
Monolithic / Domain Materials 
Still benefit from substrate 

post pro , Light fn, decal

decal > convert to decal 



| Material Strata        | BaseColor (sRGB) range (R,G,B) | Example sanity color (sRGB) |    Roughness range | Metallic | Specular / IOR                 |                                            |
| ---------------------- | ------------------------------ | --------------------------: | -----------------: | -------: | ------------------------------ | ------------------------------------------ |
| Wood (unfinished)      | R 100–170, G 70–140, B 40–110  |                (140,110,75) |          0.55–0.80 |      0.0 | Specular ~0.5 / IOR ~1.5       |                                            |
| Wood (oiled/varnished) | R 100–180, G 70–150, B 40–120  |                (155,120,80) |          0.15–0.55 |      0.0 | Specular ~0.5 / IOR ~1.5       |                                            |
| Grass (dry/healthy)    | R 50–120, G 90–170, B 40–110   |                 (90,125,55) |          0.70–0.95 |      0.0 | Specular ~0.5 / IOR ~1.38–1.45 |                                            |
| Bark / Trunk           | R 60–130, G 50–110, B 40–95    |                  (95,75,55) |          0.75–0.95 |      0.0 | Specular ~0.5 / IOR ~1.5       |                                            |
| Rock (dry)             | 90–170                         |               (125,125,125) |          0.70–1.00 |      0.0 | Specular ~0.5 / IOR ~1.5–1.6   | (channels usually close; low saturation)   |
| Rock (wet patches)     | 90–170                         |               (120,120,120) | 0.15–0.45 (masked) |      0.0 | Specular ~0.5 / IOR ~1.5–1.6   | (keep similar to dry; don’t brighten much) |
| Moss (dry to damp)     | R 35–110, G 70–150, B 30–110   |                 (65,105,55) |          0.75–0.98 |      0.0 | Specular ~0.5 / IOR ~1.38–1.45 |                                            |


| Material         | Linear (0–1) | sRGB (0–255) | Notes                      |
| ---------------- | ------------ | ------------ | -------------------------- |
| **Middle Gray**  | **0.18**     | **117**      | Standard calibration point |
| **Fresh Snow**   | 0.81         | 232          | Brightest safe dielectric  |
| **Rock (Grey)**  | 0.35         | 165          | Standard dry cliff/stone   |
| **Wood (Fresh)** | 0.30         | 152          | Unweathered light wood     |
| **Grass**        | 0.21         | 128          | Medium green field         |
| **Wood (Bark)**  | 0.14         | 103          | Weathered tree trunk       |
| **Soil (Dry)**   | 0.13         | 99           | Standard bare earth        |
| **Moss**         | 0.08         | 78           | Deep, absorbent green      |
| **Soil (Wet)**   | 0.05         | 60           | Saturated dark earth       |
| **Charcoal**     | 0.02         | 40           | Darkest safe dielectric    |

| PBR                            | default value                                                |              |                                     | Order of dops during simpli fication |                                                                                                                           |           |
| ------------------------------ | ------------------------------------------------------------ | ------------ | ----------------------------------- | ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------- | --------- |
| Albedo                         | -                                                            |              |                                     |                                      |                                                                                                                           | medium    |
| `F0` v3 (metlic / specularity) | (0.04, 0.04, 0.04)                                           | Reflectivity | Reflection at facing angle          |                                      | if f0 increase diffuse response lower                                                                                     | interface |
| `F90` (metlic / specularity)   | 1                                                            | Reflectivity | Reflection at shilluete.            | 5 Simple                             | adobe use F82 (specular edge)  - Hue and saturation shift relative to F0 value                                            | interface |
| Roughness                      |                                                              | Roughness    |                                     |                                      | spread of the highlight                                                                                                   | interface |
| `Anisotropy`                   |                                                              | Roughness    | Stretching highlights               | 2 Complex                            |                                                                                                                           | interface |
| Normal                         | (0.5, 0.5, 1)                                                |              |                                     |                                      |                                                                                                                           | interface |
| Tangent                        |                                                              |              |                                     |                                      |                                                                                                                           | interface |
| `SSS MFP`                      | 0 cm                                                         |              | Subsurface mean free path - Opacity | 5 Simple                             | density of material and effect of absorption how RGB answer to depth<br>Large values can be noisy !, best on translucency | medium    |
| `SSS MFP Scale`                | Negative values negative scattering, 0 - scatter in both dir |              |                                     | 5 Simple                             |                                                                                                                           | medium    |
| `SSS Phase Anisotropy `        |                                                              |              |                                     | 5 Simple                             |                                                                                                                           | medium    |
| Emissive                       |                                                              |              |                                     |                                      |                                                                                                                           |           |
| Second Roughness               |                                                              | Roughness    |                                     | 3 Complex                            |                                                                                                                           | interface |
| Second Roughness Weight        | 0 is using only first and 1 will use only second.            | Roughness    |                                     | 3 Complex                            |                                                                                                                           | interface |
| `Fuzz Roughness`               |                                                              | Fuzz         | Emulate fuzz                        | 4                                    |                                                                                                                           | interface |
| Fuzz Amount                    |                                                              | Fuzz         |                                     | 4                                    |                                                                                                                           | interface |
| Fuzz Color                     |                                                              | Fuzz         |                                     | 4                                    |                                                                                                                           | interface |
| Glint Dens                     |                                                              |              |                                     | 1 Most complex                       |                                                                                                                           |           |
|                                |                                                              |              |                                     |                                      |                                                                                                                           |           |

- f0 is a color - any material can exibit chromatic specular (oxide, oil films)
- energy conserving by design. if F0 increse then diffuse responce decrese 
- medium > sss, translucent, semi transparent , skin glass soft plastic 

Clasic domains (Domain matrial) will not blend:  Decal, Light fn, Post-pro, Volume, Hair / Eye, Unlit, Single Layer

##### SSS 
E-num on slab node:
- wrap < simpler 
- two-sided wrap < two sided foliage simpler 
- diffusion 
- simple volume 


IRO


##### Metal 
SMF Metal  - node help to convert metallic workflow  but can be achieved by Diffuse Albedo and F0 
- Diffuse - diffuse is separated so 0,0,0
- F0 - should be color of metal 

##### Silk fabric 

##### Thin-film  
- f0 & f90 
- dif - 0 

### Blend Materials 

`Add`  - not physically correct braking energy conservation by suming contribnution postevaluated.  Use for emissives! 
`Horizontal layers` blend materials  - if blend factor is 0/1 is only 1  else < eveluate both (only on blends)
- background / foreground 
`Vertical layers` - one on top of other and define what thick first layer is.  Expensive
- top / bottom  with thickness   (Non 0 MFP if 0 ius considered opaque and not evalueated)
`Coverage weight` (how strong material is)
`Select` - Condition  (can be smooth with TAA) ONLY WAY To blend mat with different SSS !!!! 

![[Pasted image 20251227032045.png]]
### Example glass
Material details: 
- set refraction model  (and then IRO in material)
- mode 
	- tintied glas - transl col transm 
- Ligth mode 
	- surface forroward sjhading (expensive)


# Slab BTDF 
Transmision


# Slab BSDF  
Bi-Directional Scattering distribution Fn. 
Outer and inner surface toghether 





---

# PBR
Guideling how to author textures 
Energy conservation. Light reflected or absorbed 
Metal in PBR - base color is reflection tint - metal reflect much more in facing angles as specular. (non metal 4-7%) and all materials reflect 100% at shilluete edge angle 
Roughness - how smooth on fine level (microfacet like).


# Metallic Workflow

## Albedo / Reflectance
Diffuse **reflected color** for dielectric  - flat lower contrast and brighter than normal photography
**Reflectance** value for metals 
Brightness should be between: `50` - `245` (sRGB) / `0.02` - `0.9` (Linear RGB)

Dielectrics Median luminosity:

| Mat                               | Linear                  | Linear byte | sRGB              | sRGB byte                    |
| --------------------------------- | ----------------------- | ----------- | ----------------- | ---------------------------- |
| Black                             | `0.013`                 | `5`         | `0.117`           | `30`                         |
| Gray (Zone V)                     | `0.18`                  | `46`        | `0.5`             | `128`                        |
| White                             | `0.893`                 | `229`       | `0.95`            | `249`                        |
|                                   |                         |             |                   |                              |
| Black Paint                       | `0.02` - `0.027`        | `5` - `7`   | `0.169`- `0.195`  | `43` - `50`                  |
| Coal<br>Carbon<br>Asphalt (Fresh) | `0.02` - `0.04`         |             |                   |                              |
| Brright Gray                      | `0.5`                   | 128         | `0.72`            | `186`                        |
| White acrylic paint               | `0.81`                  | 243         |                   | `230`                        |
| Fresh snow                        | `0.90`                  |             | `0.95`            | `240`                        |
|                                   |                         |             |                   |                              |
| **CONCRETE**                      |                         |             |                   |                              |
| Fresh concrete                    | `0.51` - `0.55`         | 192,191,187 | 0.67              |                              |
| Worn asphalt                      | `0.08`- `0.15`          |             | `0.42`            |                              |
| Old Concrete                      | 0.3                     | 135,136,131 | `0.57`            |                              |
| White cement                      | 0.7                     |             | `0.85`            |                              |
|                                   |                         |             |                   |                              |
| **ROCK**                          |                         |             |                   |                              |
| Limestone                         | `0.3` - `0.45`          |             |                   | `148` - `177`                |
|                                   |                         |             |                   |                              |
| Rock                              | `0.3` - `0.4`           |             |                   | `148` - `168`                |
|                                   |                         |             |                   |                              |
| **SOIL**                          |                         |             |                   |                              |
| Sand                              | 0.440,0.386,0.231       |             | 0.694,0.655,0.518 | 177,167,132                  |
| Desert sand                       | `0.36`  -` 0.40` Dry    | 177,167,132 | `0.65`            |                              |
| Sandy Soil                        | `0.25` - `0.45` Dry     |             |                   | `136` - `177`                |
| Clay Soil                         | `0.23` - `0.4` Dry      | 137,120,100 |                   | `131` - `168`                |
| Grey soil                         | `0.1`  Wet  `0.3` Dry   |             |                   | `90` - `148`                 |
| Silt loam Soil                    | `0.23` - `0.28` Dry     |             |                   | `131` -`143`                 |
| Bare soil <br>Dark earth          | `0.13` - `0.17` Dry     |             |                   | `114`                        |
| Yellow Clay                       | `0.16`                  |             |                   | `111`                        |
| Black soil                        | `0.08` Wet  `0.15` Dry  |             |                   | `81` - `108`                 |
|                                   |                         |             |                   |                              |
| **FOLIAGE**                       |                         |             |                   |                              |
| Green grass                       | `0.2` -  `0.25`         |             | `0.53`            | `123` - `136`                |
| Tundra                            | `0.2`                   |             |                   | `123`                        |
| Tall wild grass                   | `0.16` - `0.18`         |             |                   | `111` - `117`                |
| Tea bushes                        | `0.16` - `0.18`         |             |                   | `111` - `117`                |
| Corn field                        | `0.16` - `0.17`         |             |                   | `111` - `114`                |
| Deciduous tree                    | `0.15` - `0.18`         |             |                   | `108` - `117`                |
| Grain crops                       | `0.1` - `0.25`          |             |                   | `90` - `136`                 |
| Moss                              | `0.1`                   |             |                   | `90`                         |
| Summer Foliage                    | `0.09` - `0.12`         |             |                   | `85`                         |
| Autumn Foliage                    | `0.15` - `0.3`          |             |                   | `109` -`148`                 |
| Conifer Forest                    | `0.08` - `0.12`         |             |                   | `81`                         |
| Leafs                             | `0.07` Wet  `0.2` Dry   |             |                   | `75` - `123`                 |
|                                   |                         |             |                   |                              |
| **WOOD**                          |                         |             |                   |                              |
| Batten planks <br>(fresh wood)    | `0.35` - `0.42`         |             |                   | `158` - `172`                |
| Batten planks <br>(old weathered) | `0.12` - `0.16`         |             |                   | `97` - `111`                 |
| Varnished wood                    | `0.13`                  |             |                   | `101`                        |
| Bark, oak                         | `0.1`                   |             |                   | `90`                         |
|                                   |                         |             |                   |                              |
| **WATER**                         |                         |             |                   |                              |
| Ocean Ice                         | `0.56` ( `0.5` - `0.7`) |             |                   |                              |
| Water sun horizon                 | `0.5` - `0.8`           |             |                   |                              |
| Water sun zenith                  | `0.05`                  |             |                   |                              |
|                                   |                         |             |                   |                              |
| **SKIN**                          |                         |             |                   |                              |
| Skin European                     | `0.35` - `0.6`          |             |                   | `158` - `202`                |
| Skin Indian                       | `0.15` - `0.3`          |             |                   | `108` - `148`                |
| Skin African                      | `0.05` - `0.15`         |             |                   | `65` - `108`                 |
|                                   |                         |             |                   |                              |
| Metal                             | <br>                    |             |                   | `180` / `186` - `255` (sRGB) |

Joey Lenz

| Material    | Description | Color Swatch | Hexadecimal Values | RGB Channel Values | Normalized Values |
|-------------|-------------|---------------|--------------------|--------------------|-------------------|
| Charcoal | Dielectric albedo values control reflected color and most exist in the midtone range. Charcoal is the darkest dielectric albedo value that should be used. Insulators don't typically have colored specular reflectivity, but lights affect reflected color. | Dark gray | sRGB = 2b2b2b<br>Linear RGB = 060606 | sRGB = 43<br>Linear RGB = 5 | sRGB = 0.17<br>Linear RGB = 0.02 |
| Fresh Snow | Dielectric albedo values control reflected color and most exist in the midtone range. Fresh snow is the brightest dielectric albedo value that should be used. Insulators don't typically have colored specular reflectivity, but lights affect reflected color. | White | sRGB = e8e8e8<br>Linear RGB = cecece | sRGB = 232<br>Linear RGB = 207 | sRGB = 0.91<br>Linear RGB = 0.81 |
| Metallic | Unlike dielectric base colors, metallic albedo brightness controls specular intensity, which can contain color. Conductive albedo values fall within this row's range. | Light gray to white | sRGB = d9d9d9 - ffffff<br>Linear RGB = b1b1b1 - ffffff | sRGB = 217 - 255<br>Linear RGB = 179 - 255 | sRGB = 0.85 - 1<br>Linear RGB = 0.7 - 1 |
**Saturation Formula**

`(((Max(RGB Channel Value) - Min(RGB Channel Value)) / Max(RGB Channel Value)) * 100) = Saturation %`

| Material         | Color Swatch | Saturation Percent             |
| ---------------- | ------------ | ------------------------------ |
| Varnished Wood   | Light gray   | sRGB = 56%<br>Linear RGB = 82% |
| Dark Soil        | Gray         | sRGB = 42%<br>Linear RGB = 70% |
| Green Vegetation | Gray         | sRGB = 40%<br>Linear RGB = 67% |
| Gold             | Gray         | sRGB = 39%<br>Linear RGB = 67% |
| Sand             | Dark gray    | sRGB = 25%<br>Linear RGB = 47% |
| Rough Wood       | Dark gray    | sRGB = 25%<br>Linear RGB = 47% |

[A database of physically based values for CG artists](https://physicallybased.info/)


## Specular
**Dielectric F0 Reflectance** Unreal values 0-8%. Thus default value is .05 (which is 4% reflective)  
`Value = ( (1 - IOR) / (1 + IOR) )²` 
Fresnel reflection coefficient mount of light that reflects off a surface when the viewing angle is perpendicular (i.e., the angle of incidence is 0 degrees).

Let the material value in unreal be default 0.5 and multiply by a cavity map to darken cavities.

specular reflectance values (denoted as "F0") specular reflectance refers to the amount of light reflected at a particular angle from a surface.

Wood  - 0.02 to 0.05 
natural stones like granite or marble, the F0 value can range from 0.02 to 0.05.


Depending on factors like moisture content and leaf type, F0 values can vary, but they may range from 0.03 to 0.08.
F0 values for healthy green leaves typically range from around 0.03 to 0.08.
Dry or Wilted Leaves: Leaves that are dry or wilted may have slightly lower F0 values, possibly ranging from 0.02 to 0.06.

| Mat | sRGB |
| ---- | ---- |
| Plastic | 55-64 |
| Rusted metal | 52 |
| Water | 43 |
| Ice | 41 |
| Glass | 57 |
| Gold | 255 226 155 |
| Silver | 252 250 245 |
| Aluminium | 245 246 246 |
| Iron | 196 199 199 |
| Copper | 250 506 192 |
metal  `0.7` - `1` specular


## Roughness
**Microfacets models** how rough (in microscale)  mat is (amp & freq of bumps in material ) tiny imperfections in mat  & angle of incoming lightEverything has Fresnel and reflections ! [YT link](http://filmicworlds.com/blog/everything-has-fresnel/)
The specular part of Disney “principled” BRDF is a GGX BRDF. It use a roughness parameter.
Nm is crucial! 
more direct reflection and depends heavily on the viewing angle relative to the light source and the surface normal.
- reflection on angle is more sharp and visible

|             |                |
| ----------- | -------------- |
| 0 -0.2 <br> | polished / wet |
| 0.2-0.5     | smooth <br>    |
| 0.5-0.8     | rough <br>     |
| 0.8-1       | matte          |

| Mat | UE |
| ---- | ---- |
| Air |  |
| Ice | `0.224` |
| Water | `0.255` |
| Milk | `0.277` |
| Skin | `0.35` |
| COMON | `0.5` |
| Glass | `0.5` |
| Plastic | `0.5` |
| Quartz | `0.57` |
| Diamond |  |
| Rubbet | .8 ?  |


argiles - ziemia like 
craie
sable (kamienie zółtawe)
calcaire = limestone  (kamienie szare jane z białymi przetarciami)
 schistes = łupki 
granite


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



# Specular Workflow 

## Strata 



|         | F0                                    | f90 |
| ------- | ------------------------------------- | --- |
| Plastic | 0.04 most materials default in unreal |     |





- metal pure reflection > only refraction (or absorbed [heat]) > only mat that tint reflection  (but saturate with Fresnel)