---
title: Shaders
description: PBR, MaterialX, Unreal
categories:
 - PXL
tags:
- Unreal
- Rendering
- Real Time
- Shaders
- Game Dev
permalink: /mat/
---
[Camera](/camera/)      
[Algebra](/algebra/)  
[Rendering](/rendering/)  
[Mat Data](/matdata/)  
Karmam   


# PBR

Material models:  
- Metallic  - unreal
- Specular setups

https://seblagarde.wordpress.com/2011/08/17/feeding-a-physical-based-lighting-mode/   
 https://www.pbr-book.org/3ed-2018/contents    
https://marmoset.co/posts/physically-based-rendering-and-you-can-too/  


----

# MaterialX

Layers Horizontal and vertical:

| | |
| -- | -- |
|Transparency | Specular reflection (coating)
|Emission Additive | Specular reflection
|Specular reflection (metal) | Specular reflection
|Specular transmision | Specular retro-reflection (sheen)
|Diffuse reflection / transmision / sss


## Workflow

### Material Standard


<img src="/src\hou\mat/matx2.png" width="600">  

###### Mat Nodes

- `mtlx Material Standard Surface` - use like default material
- `collect node` - pipe at the end and check orange flag as output

### Surface packed

<img src="/src\hou\mat/matx1.png" width="600">


surface/volume/light/displace

###### BRDF Nodes

- `Oren-Nayar` - _diffuse_brdf_
- `Disney Principled BRDF`  - _burley_diffuse_brdf_
- `Conductor BRDF` - artistic friendly Metalic fresnel (energy compensation for multiple microfacet bounces)
  - D = ddx/beckman
  - G = height corelated smith
  - F = conductor
- `Dielectric`
  - D = ddx/beckman
  - G = height corelated smith
  - F = dielectric / schlick  
- `Generalized Schlick`
- `Thin Film`
- `sheen` - cloths

---

###### Basic
- `mtlx Usd Prim Var Reader` - bind attribs / get attrib


###### Math
- `mtlx Const` - value
- `mtlx Multiply`
- `mtlx Remap` -

###### Noise
- `mtlx Fractal 3d` - noise
- `cellnoise 3d `
- `noise 3d`
- `worley noise 3d`

###### Texture
- `mtlx Image` - Load texture
- `mtlx Tiled Image` - Load texture
- `mtlx Image` > `mtlx Normal Map`- Load nm texture

###### UV
- `mtlx Triplanar Projection`
...

 - Displacement: - `Collect` node - can plug in mtlx in  `mtlx image` > `mtlx remap` Color FA > `mtlx displacement`
 - Volume: - `mtlx Volume`
    - `vdf` - volume > `mtlx anisotropic vdf` set absorption&scattering > `mtlx Geompropvalue` geomprop: density > set value  
    - `edf` emmition

----


# Unrela

## Options


|Blend models | |   Usage|
|-- | -- | -- |
|alpha composite
| alpha holdcut

|Shading models | |   Usage|
|-- | -- | -- |
|Lit / Unlit
**Sss** |
**Preintegrated Skin**|   cheaper to render than the Sss method |
**Subsurface Profile** | higher-end skin rendering |
**2 Sided Foliage** | |  simulate transmision, for cloths (non solid materials)
**Hair** | | multiple specular highlights: 1) color of light, 2) mix of hair and light color.
**Cloth** | | "fuzz" layer
**Single Layer Water** | | translucent in opaque mode
**Thin Translucent** | | colored glass (background) white specular highlight and the tinted background are needed


Translucency Mode | Ps/Vs | Cost |  Usage|
-- | -- | -- | -- |
Volume Non Directional| pixel | cheapest pixel|
Volume Directional | pixel ||
Volume Per-Vertex Non Directional| vert | cheapest vert|
Volume Per-Vertex Directional| vert||
Surface Translucency Volume ||low per pixel but blurry | glass, water
Surface forward Shading| forward |most expensive. Each light per pixel| glass, water


**Thin Transparent** shading model and material expression, you are able to accurately represent tinted and colored transparent material

## Passes

#### Roughness
(Roughness here is coupled with the BRDF used by the Unreal engine 4, it may not be compatible with other engines)

#### Refraction
-  physical model of **Index of Refraction** - but you will have an offset that reads from off screen, shift material glitches can occure.   
- **Pixel Normal Offset** enables refraction for these large flat surfaces, like water,

#### SSS
To use this feature, enable Burley in the Subsurface Profile and set the Editor Preview Level to Cinematic. If you're already using Separable SSS profile, minimal changes are required to switch to this method. Note that Burley SSS requires Temporal Anti-Aliasing to work properly.



----


## Decals

There are 11 blend modes that decals can use:

- Translucent - Can use Diffuse, Metallic, Specular, Roughness, Emissive, Opacity, and Normal.
- Stain - Is a modulate type blend with Diffuse and Opacity.
- Normal - Uses the Opacity and Normal channels and only affects the Normal map layer it is projecting on.
- Emissive - Uses Emissive and Opacity only.
- Volumetric Distance Function - Use the output of signed distance in Opacity depending on Light Vector.
- The DBuffer decals can be used with lighting. These are not on by default and must be enabled in the Project Settings > Rendering section.
- DBuffer Translucent Color, Normal, Roughness - This is non-metallic and will use the Color, Opacity, Roughness, and Normal to work with baked lighting.
- DBuffer Translucent Color - This is non-metallic and will use only the Color and Opacity to work with baked lighting.
- DBuffer Translucent Color, Normal - This is non-metallic and will use the Color and Normal to work with baked lighting.
- DBuffer Translucent Color, Roughness - This is non-metallic and will use the Color and Roughness to work with baked lighting.
- DBuffer Translucent Normal - This will only use the Opacity and Normal channels to work with baked lighting.
- DBuffer Translucent Normal, Roughness - This will only use the Roughness, Opacity, and Normal to work with baked lighting.
- DBuffer Translucent Roughness - This will only use the Roughness and Opacity to work with baked lighting.


## Nodes

- `camera vector` is to given vector (observatiion vector)
- `camera direction` is same dir

----


## Features
###### Motion Vectors

https://www.sidefx.com/tutorials/create-motion-vectors-for-time-warping-image-sequences/


###### 6D Lightmaps.

###### Biplanar projection:    

https://www.shadertoy.com/view/ws3Bzf     
https://iquilezles.org/www/articles/biplanar/biplanar.htm   


IOR: most dielectrics 1.5.

Unreal simplified disney model



## Dense details Landscape

- Paralax / wpo /
- Tessal / vs
- Virtual texture - runtime Vertual Texture
https://youtu.be/kxsQ5m2IAXs

#### Decals



.997 < brightest wall. never one !
