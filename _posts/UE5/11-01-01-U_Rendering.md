---
title: U Features Rendering
description: Shadows, Reflections,  Post Process, Nanite
categories:
  - PXL
tags:
  - Unreal
  - Rendering
  - Tech
  - Art
  - RealTime
  - GameDev
permalink: /urendering/
aliases:
  - urendering
---
> Obsidian: [[09-01-01-U_Optimisation]] [[05-01-01-U_BP]] [[05-01-01-U_Code]]


# Project Settings
- `Suport Sky Atmosphere` &   
- `Suppport Atmosphere Affecting Height Fog` - to work with new atmosphere Additional shader permutations     
- `Extend default range` in settings for Exposure   
- `Apply Pre-Exposure before writing to scene color` = true, can creates problems with sub-surface scattering materials   ( UNREL: If reflective surfaces have artifacts like black patches, the Scene Color buffer might be overflowing. To fix it, either enable Apply Pre-Exposure before writing to the scene color in the Project Settings, or reduce the brightness of lights in the scene.)

# Render buffer passes

|  |  |
| ---- | ---- |
| albedo |  |
| separate translucency  |  |
|  |  |

# Sky light
#### DFAO

# Post Process

Cube map.  Newer use.-  Same as sky but not shadowed !

#### DOF   
#### Bloom  
#### Flares
#### Color grading + tone mapping   
#### PP materials
#### Motion Blur   


#### Exposure   
DFAO ?? mUltiplaye  


#### SSGI

```
`r.SSGI.Enable`  
`r.SSGI.Quality 1-4`  

```

####  SSAO (Screen Space Ambient Occlusion)
implementation and is currently based on the depth buffer only. ur method makes use of the depth buffer and the normal from the GBuffer (see Deferred Shading). You can look at the AO value directly by using the "Visualize GBuffer" view mode (see View Modes) or by using the show flag "Visualize Ambient Occlusion". As the AO is part of the GBuffer, it also can be output by the material. The SSAO and material AO become combined and can result in even darker AO.

#### Bloom
Classic - Gausian filters
Convoluted - (weighted distribution) by filtering freq. with Fast Fourier Transform. (Each pixel render shape with weight).
Kernel: (duper center must be turbo bright. Percentage of bright will affect sharpnes of bloom from EXR texture). `HDR compression` no `mip maps` and `never stream`. (Kernel is remaped to size and transf to freq space and cached)  
`Convolution Center` - It can move image if wrongly set becase it giev out back an image with efect composed  
`Convolution Boost` - Promote bright pixels    
`Convolution Buffer` - Help to not blead bloom to other side of screen. (should be as small as possible cause it add black borders)      


Raytraceing: GI + Reflections + Translucency   
Path Traceing   

---

# Reflection
Capturing the level into cube maps is a slow process which must be done outside of the game session. - Planar (can mask assets)

##### SSR   
SSGI becomes apparent when it's being used as the sole indirect lighting illumination for the scene. For example, using baked lighting reduces screen space artifacts when transitioning behind a large occlude where a bright object may be located. SSGI is recommended as a means to improve indirect lighting illumination in your scene but not as a sole indirect lighting method  

Project Settings > Engine > Rendering under the Lighting category


---

DFAO, HFGI, Raytraced Soft
Distance Field Soft Shadows
Distance Field Ambient Occlusion


---

## Linear Space Workflow

(pix.ink Linear data:)[/res/]

- Render in linear > Apply gamma > apply s-curve corections.
- GammaCorrection-to-LinearRGB Linear RGB `( Gamma Correction Value ^ (1 / 2.2))`  (1/22 = 0.4545)    
- LinearRGB-to-GammaCorrection Gamma Correction `(Linear RGB Value ^ 2.2)`        

 Unreal render in linear hdr and tonmap (filmic: ACES) to LDR.  

The HDR input in the **Pixel Inspector** measures everything in luminance or cd/m² or nits, which is why you want to use a pure white material since luminance is based on color. Taking that HDR value and multiplying it by pi will give you the Lux value.
 `pixel Brightness = Exposure * Luminance` ( before the tonemapper and exposure compensation) - scene surface luminance (L in cd/m²)


```
`r.tonemapperfilmic 0`- disable filmic and change to default
```

## HDR
texture compress: vector displacement   

https://www.unrealengine.com/en-US/tech-blog/how-epic-games-is-handling-auto-exposure-in-4-25

```
`r.HDR.Display.OutputDevice`	Device format of the output display:
- `0`: sRGB (LDR),
`1`: Rec709 (LDR),
`2`: Explicit gamma mapping (LDR),
`3`: ACES 1000 nit ST-2084 (Dolby PQ) (HDR),
`4`: ACES 2000 nit ST-2084 (Dolby PQ) (HDR) ,
`5`: ACES 1000 nit ScRGB (HDR),
`6`: ACES 2000 nit ScRGB (HDR),
`7`: Linear EXR (HDR)   
`r.HDR.EnableHDROutput`    
`r.HDR.Display.ColorGamut`   
```

## ACES

```
UE4 ships with ACES as the default tonemapper but they did tweak it to make it a less shockingly different result to what people were used to before... which I think helps with the "8-bit ACEScg textures not a great idea" problem
[10:17 PM]
someone on ACEScentral figured out what the exact change was - I think broadly it's brighter and flatter than what you'd expect if you just took a scene authored for sRGB and interpreted it as ACEScg
[10:22 PM]
they did adopt the standard ODTs though which is very sensible - you can work in SDR then switch the output for an HDR TV without having a Huge Nightmare
```


-----
Gi
ddgi -dynamic direct gi -  proby
https://www.youtube.com/watch?v=ZefvmV1pdP8&t=121s




"Tech:
Fixed v-sync being unavailable when only DLSS SR is on but not FG. Now only FG disables v-sync community request "

Can you actually revert this. Unless you are setting a frame rate limiit in the Nvidia control panel, (with gsync , or freesync premium or vrr monitors).  You still need to use V-sync enabled to cap the fps above the monitors refresh rate.  Typically most people will cap there fps 1-5 fps below the monitors max refresh rate ( that is how gsync and freesync works .) If you don't want to use a framerate  limiter, you still need v-sync to use Gsync even if you are using frame generation.
TLDR: if using Gsync or Gsync with Frame Geneation , you need to either cap fps 1-5 below max refresh rate, and or have V-sync enabled .




