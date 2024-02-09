---
title: Shaders
description: PBR, MaterialX, Unreal
categories:
  - PXL
tags:
  - Unreal
  - Rendering
  - Shaders
  - RealTime
  - GameDev
permalink: /mat/
aliases:
  - mat
---
> Pxlink: [Camera](/camera/) / [Algebra](/algebra/) / [Rendering](/rendering/) / [Mat Data](/matdata/)  
>Obsidian:  [[16-02-01-Rendering|Rendering]] / [[08-01-01-Material|matdata]] / [[16-02-01-Substance_Designer|substancedesigner]] / [[09-01-01-U_Optimisation|uoptimization]]

> External links: 
>[Cg encyclopedia](https://chrisbrejon.com/articles/albedo-and-pointers-gamut/)
>[SeblaGarde blog PBR](https://seblagarde.wordpress.com/2014/04/14/dontnod-physically-based-rendering-chart-for-unreal-engine-4/)
>[Iri Shinsoj](https://shinsoj.artstation.com/projects/klJb8d)
>[Substance PBR guide](https://substance3d.adobe.com/tutorials/courses/the-pbr-guide-part-2)
>[PBR wiki 2018](https://www.pbr-book.org/3ed-2018/contents )   

# Shaders 

##### Fragment shader
Shader Language has a single main function that returns a color at the end.
Each thread is not just blind but also memoryless.


### VS Vertex shader    
.

### PS Pixel shader (old fragment)    

grid of pixels that work paralel

### Compute shader   
in paralel on gpu
subdivisions workgroups and in each group divisions

### Mesh shader    
Mesh Shaders    
- for new tessalation

### Task shader
 call based of cam frustrum   



# PBR
Energy conservation 
Eyes are less sensitive in dark. 

### Workflow

##### Metal / Roughness 
A byproduct of using the metal/roughness workflow is that it can produce a white edge artifact, (Unreal)
- white artefacts on blend
##### Specular/glossiness
- dark artefacts on blend





----

# MaterialX

Layers Horizontal and vertical:

|  |  |
| ---- | ---- |
| Transparency | Specular reflection (coating) |
| Emission Additive | Specular reflection |
| Specular reflection (metal) | Specular reflection |
| Specular transmision | Specular retro-reflection (sheen) |



## Workflow

### Material Standard

![My image Name](/src/hou/mat/matx2.png)

###### Mat Nodes
Base nodes
- `mtlx Material Standard Surface` - use like default material
- `collect node` - pipe at the end and check orange flag as output
for color input to base_color

### Surface packed

![My image Name](/src/hou/mat/matx1.png)


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


##### Features

Displacement:
- `Collect` node - can plug in mtlx in  mtlx`Image` > mtlx`Remap` Color FA > mtlx`Displacement`


---

##### Basic
- `Usd Prim Var Reader` - bind attribs / get attrib

##### Math
- mtlx`Constant` - value
- mtlx`Multiply`
- mtlx`Remap` -
- mtlx`Mix` - lerp
- mtlx`Ramp` - Slower mix in vex

##### Noise
- mtlx`Fractal 3d` - noise
- mtlx`cellnoise 3d `
- mtlx`noise 3d`
- mtlx`worley noise 3d`

##### Texture
- mtlx `Image` / mtlx `Tiled Image` - Load texture basic
- mtlx`UsdUVTexture` - Load texture - channel options

How to Add normal map:
- mtlx `Image` > `Normal Map`- Load nm texture

###### UV
- mtlx`Texture coordinates` -
- mtlx`Triplanar Projection`
...

##### Volume:
- mtlx`Volume`
    - `vdf` - volume > mtlx `anisotropic vdf` set absorption&scattering > mtlx `Geompropvalue` geomprop: density > set value  
    - `edf` emmition


##### non mtlx Nodes
- Curvature
- Range
- Color correct
- Ambient occlusion
- State vector 

----


# Unrela



## Options

| Blend models |  | Usage |
| ---- | ---- | ---- |
|  |  |  |

| Translucency Mode | Ps/Vs | Cost | Usage |
| ---- | ---- | ---- | ---- |
| **Sss** |  |  |  |
| **Preintegrated Skin** | cheaper to render than the Sss method |  |  |
| **Subsurface Profile** | higher-end skin rendering |  |  |
| **2 Sided Foliage** |  | simulate transmision, for cloths (non solid materials) |  |
| **Hair** |  | multiple specular highlights: 1) color of light, 2) mix of hair and light color. |  |
| **Cloth** |  | "fuzz" layer |  |
| **Single Layer Water** |  | translucent in opaque mode |  |
| **Thin Translucent** |  | colored glass (background) white specular highlight and the tinted background are needed |  |


|Translucency Mode | Ps/Vs | Cost |  Usage|
|-- | -- | -- | -- |
|Volume Non Directional| pixel | cheapest pixel|
|Volume Directional | pixel ||
|Volume Per-Vertex Non Directional| vert | cheapest vert|
|Volume Per-Vertex Directional| vert||
|Surface Translucency Volume ||low per pixel but blurry | glass, water
|Surface forward Shading| forward |most expensive. Each light per pixel| glass, water


**Thin Transparent** shading model and material expression, you are able to accurately represent tinted and colored transparent material


----


## Decals

There are 11 blend modes that decals can use:

The DBuffer decals can be used with lighting. These are not on by default and must be enabled in the Project Settings > Rendering section.

|  |  |
| ---- | ---- |
| Translucent | Can use Diffuse, Metallic, Specular, Roughness, Emissive, Opacity, and Normal |
| Stain | Is a modulate type blend with Diffuse and Opacity. |
| Normal | Uses the Opacity and Normal channels and only affects the Normal map layer it is projecting on. |
| Emissive | Uses Emissive and Opacity only. |
| Volumetric Distance Function | Use the output of signed distance in Opacity depending on Light Vector. |
|  |  |
| DBuffer Translucent Color, Normal, Roughness | This is non-metallic and will use the Color, Opacity, Roughness, and Normal to work with baked lighting. |
| DBuffer Translucent Color | This is non-metallic and will use only the Color and Opacity to work with baked lighting. |
| DBuffer Translucent Color, Normal | This is non-metallic and will use the Color and Normal to work with baked lighting. |
| DBuffer Translucent Color, Roughness | This is non-metallic and will use the Color and Roughness to work with baked lighting. |
| DBuffer Translucent Normal | This will only use the Opacity and Normal channels to work with baked lighting. |
| DBuffer Translucent Normal, Roughness | This will only use the Roughness, Opacity, and Normal to work with baked lighting. |
| DBuffer Translucent Roughness | This will only use the Roughness and Opacity to work with baked lighting. |



## Unreal material nodes
`Camera vector` is a vector, that points from pixel to camera position. (observatiion vector)
`CameraDirectionVector`, is a vector, that corresponds to direction, where camera is pointing in worldspace.


----

## Triplanar

[Basic](https://bgolus.medium.com/normal-mapping-for-a-triplanar-shader-10bf39dca05a#d715)
[Biplanar](https://iquilezles.org/articles/biplanar/)
[dithered and optimized](https://ryandowlingsoka.com/Triplanar-Dithered-Triplanar-and-Biplanar-Mapping-in-Unreal-7844313e458e4316aca1e40e6394109e)


## Features
##### Motion Vectors

https://www.sidefx.com/tutorials/create-motion-vectors-for-time-warping-image-sequences/


##### 6D Lightmaps.

##### Biplanar projection:    

https://www.shadertoy.com/view/ws3Bzf     
https://iquilezles.org/www/articles/biplanar/biplanar.htm   


IOR: most dielectrics 1.5.

Unreal simplified disney model


## Dense details Landscape

- Paralax / wpo /
- Tessal / vs
- Virtual texture - runtime Vertual Texture
https://youtu.be/kxsQ5m2IAXs

## POM vs Tessalation:

