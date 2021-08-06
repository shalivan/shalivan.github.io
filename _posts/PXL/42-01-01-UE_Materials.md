---
title: Unreal Materials
description: PBR
categories:
 - PXL
tags:
- Unreal
- Rendering
- Real Time
- Shaders
- Game Dev

permalink: /umat/
---


# Blend models


- alpha composite
- alpha holdcut

# Shading models


|Lighting Mode | PS VS | Cost |  Usage|
|-- | -- | -- | -- |
|lit

 Subsurface scattering model that works well for skin or thicker surfaces.  
**sss** -  You can think of this as the color of the matter just beneath the surface of the object, such that when light scatters through the surface, this color will be seen.   
**Preintegrated Skin** -   cheaper to render than the Subsurface method
**Subsurface Profile** - is geared towards higher-end skin rendering.
.
**2SidedFoliage+** - simulate transmision, for cloath(non solid materials) Materials
**Hair** - multiple specular highlights: one representing the color of light, and another representing a mix of hair and light color.


**cloth** - "fuzz" layer
**Single Layer Water** - translucent in opaque mode
**Thin Translucent** - colored glass (background) white specular highlight and the tinted background are needed
----

# PBR

Material models:  
- Metallic  
- Specular setups


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


## Refraction
-  physical model of **Index of Refraction** - but you will have an offset that reads from off screen, shift material glitches can occure.   
- **Pixel Normal Offset** enables refraction for these large flat surfaces, like water,

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




https://marmoset.co/posts/physically-based-rendering-and-you-can-too/

# Decals

There are 11 blend modes that decals can use:

Translucent - Can use Diffuse, Metallic, Specular, Roughness, Emissive, Opacity, and Normal.

Stain - Is a modulate type blend with Diffuse and Opacity.

Normal - Uses the Opacity and Normal channels and only affects the Normal map layer it is projecting on.

Emissive - Uses Emissive and Opacity only.

Volumetric Distance Function - Use the output of signed distance in Opacity depending on Light Vector.

The DBuffer decals can be used with lighting. These are not on by default and must be enabled in the Project Settings > Rendering section.

DBuffer Translucent Color, Normal, Roughness - This is non-metallic and will use the Color, Opacity, Roughness, and Normal to work with baked lighting.

DBuffer Translucent Color - This is non-metallic and will use only the Color and Opacity to work with baked lighting.

DBuffer Translucent Color, Normal - This is non-metallic and will use the Color and Normal to work with baked lighting.

DBuffer Translucent Color, Roughness - This is non-metallic and will use the Color and Roughness to work with baked lighting.

DBuffer Translucent Normal - This will only use the Opacity and Normal channels to work with baked lighting.

DBuffer Translucent Normal, Roughness - This will only use the Roughness, Opacity, and Normal to work with baked lighting.

DBuffer Translucent Roughness - This will only use the Roughness and Opacity to work with baked lighting.

# Features
###### Motion Vectors

https://www.sidefx.com/tutorials/create-motion-vectors-for-time-warping-image-sequences/


###### 6D Lightmaps.

###### Biplanar projection:    

https://www.shadertoy.com/view/ws3Bzf     
https://iquilezles.org/www/articles/biplanar/biplanar.htm   


IOR: most dielectrics 1.5.

Unreal simplified disney model



## paralax / wpo

https://youtu.be/kxsQ5m2IAXs

#### Decals



.997 < brightest wall. never one !
