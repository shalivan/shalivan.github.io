---
title:  UE Rendering Features
description: RAW
categories:
 - RT
tags:
- Unreal
- Rendering
- Real Time
- Game Dev
- Tech Art
permalink: /ue_rendering_features/
---


[Unreal Light & Atmosphere](/uelight/)



#### Project and Light Settings
- `Suport Sky Atmosphere` &   
- `Suppport Atmosphere Affecting Height Fog` - to work with new atmosphere Additional shader permutations     
- `Extend default range` in settings for Exposure   
- `Apply Pre-Exposure before writing to scene color` = true, can creates problems with sub-surface scattering materials   ( UNREL: If reflective surfaces have artifacts like black patches, the Scene Color buffer might be overflowing. To fix it, either enable Apply Pre-Exposure before writing to the scene color in the Project Settings, or reduce the brightness of lights in the scene.)

----




# Shadows
Point Light - Point light have 6x shadows .Max draw distance


 - Cascade shadows:   split cam frustrum to pieces
 - Ray traced distance dield shadows: for far 30 50% more eficient than cascade (5000 units) save on GPU little
 - Capsule shadows
 - Close shadow (contact)   
 - Volume shadows

`Cast Shadows`    
`deep shadow` - Advanced hair strands (GPU time)  
`Ray Trace`  
`Cast Volumetric Shadows` - (GPU time)  
`Affect translucency` (GPU time)    
`transmision` (for sss)    

  Cache shadows lights: movable prim: staic/stationary


##### Distance field Shadows    
`Distance`     
`Trace dist`   
`Ray start Depth off`  

##### Cascade Shadow Maps   
`Dyn Shadow Distance Movable Light`     
`Casc numb`   
`Distribution Exp`  
`Tranmsition Fraction`   
`Distance Fade Out fraction`   
`Far Shadow Cascarde Count`   
`Far Shadow Distance`   

---

# Reflection
>Capturing the level into cubemaps is a slow process which must be done outside of the game session. - Planar (can mask assets)

##### SSR  
>SSGI becomes apparent when it's being used as the sole indirect lighting illumination for the scene. For example, using baked lighting reduces screen space artifacts when transitioning behind a large occluder where a bright object may be located. SSGI is recommended as a means to improve indirect lighting illumination in your scene but not as a sole indirect lighting method  

Project Settings > Engine > Rendering under the Lighting category

---

# Exposure
>Algorithm uses the average of the log luminance of the scene
Using phisycal values help with nor overexposure for emissives
Extend default range and **Apply Pre-Exposure before writing to scene color** Calculation of the average scene luminance is used for the Grey Point exposure values are interpreted as EV100 in Unreal Engine    
 By default, Unreal Engine’s lens attenuation is set to 0.78. At a value of 0.78, the math cancels out and you can interpret the lighting as unitless. bnecause game camera dont loose light and not required 1.2(q=0.65)    


##### `Basic`
Simple for whole pixels

- `Exposure Compensation` - Low Brighter, High Darker. (Add scale of 2^ExpComp on top of existing exposure)     
- `Min/Max EV100` - to set Min set view in dark place and adjust. to set Max adjust in max brightness  

##### `Histogram`
Discards the pixels above and below treshold

- `Low/high Percentage` - is 10% A and  95% B Therefore current luminance is the The average between A and B    
- `Histo Min/Max`  

- `Apply Physical Camera Exposure`. It enables you to control whether physical camera parameters affect auto exposure or not. This means that a manual camera with an exposure compensation of 0.0 will exactly match an auto exposure scene that is set to zero when this property is disabled.   


 ##### Pre-Exposure
>If reflective surfaces have artifacts like black patches, the SceneColor buffer might be overflowing. To fix it, either enable `Apply Pre-Exposure` before writing to the scene color in the Project Settings, or reduce the brightness of lights in the scene. Apply Pre-exposure before writing to the scene color is only supported on Windows. and can have problems with SSS

```
`r.UsePreExposure` - 0-1  
`r.EyeAdaptation.PreExposureOverride` - 0-1    
```

##### Exposure Measurement
>To check how many light incom from skylight by: You can `pixel inspector` and have luminnance in candela and pixel brightness.. and check how much candelas. (HDR luminance value).



- Window > DeveloperTools > PixelInspector  
- Show > Visualize > HDR (Eye Adaptation)

```
ShowFlag.VisualizeHDR 1
```


 - blue line is the target EV100 exposure value for the view.
 - purple line is the actual EV100 exposure
 - white line is the final EV100 exposure value after adjusting the exposure compensation



below the target histogram range will be shown in red, anything above the range will be in blue. It ensures that the high and low percentile ranges that we’ve set are removing the unwanted pixels
```
r.EyeAdaptation.VisualizeDebugType 0 (scene color after tone mapping)   
r.EyeAdaptation.VisualizeDebugType 1 (histogram debug mode)   
```

---


# Sky light
#### DFAO

---

# Post Process

Cubemap.  Newer use. Old One !!!! same as sky but not shadowed !

#### DOF   
#### Bloom  
#### Flares
#### Color grading + tonemaping   
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
>implementation and is currently based on the depth buffer only. ur method makes use of the depth buffer and the normal from the GBuffer (see Deferred Shading). You can look at the AO value directly by using the "Visualize GBuffer" view mode (see View Modes) or by using the show flag "Visualize Ambient Occlusion". As the AO is part of the GBuffer, it also can be output by the material. The SSAO and material AO become combined and can result in even darker AO.

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

# Mesh


Use High Precision Tangent Basis     
Use High Precision uv    


## Distance field
>0 inside. staic object and avoid v huge meshes


- DFAO Distance field   
- Soft Shadow rayytraced for far  

Acces in material slot  
Optimisation: 8 bit (halfmemory) / compress: les mem but hitches on sream decomp  



`Radious` `Distance` `Power` `Bias`

```
`r.AOListMeshDistanceFields` - check memory   
`ShowFlag.VisualizeGlobalDistanceField`    
`ShowFlag.VisualizeDistanceFieldAO`  
```

---


# Material

## POM vs Tessalation:


## Translucent in Deffered problems


## Motion Blur
Visualise > motion blur (in simulate) (colored in motion)    
Bufer visualitsation > Velocity     
`Accurate velo` in settings !

PP@cam can ovveride
- per object setting - will exclude from MB (not working if acucurate velo is enable in settings)

type of object
- sequence - (just work)
- BP set actor location - (just work)
- Verte offset material - (in project settings + material:  support accurate velo from vert deform)
- in particle system - material: Particle motion Blur Fade !!!!!(cascade override, and transulcent only on gpu)
- on spline - material: preview frame switch

https://youtu.be/r1BCJt22oHY



## Linear Space Workflow

- Render in linear > Apply gamma > apply s-curve corections.
- GammaCorrection-to-LinearRGB Linear RGB `( Gamma Correction Value ^ (1 / 2.2))`  (1/22 = 0.4545)    
- LinearRGB-to-GammaCorrection Gamma Correction `(Linear RGB Value ^ 2.2)`      
- Linear to sRGB (for sRGB dvices) - Mid grey 18% after gamma look like 50%    

https://www.vfxwizard.com/tutorials/gamma-correction-for-linear-workflow.html  

 Unreal render in linear hdr and tonmap (filmic: ACES) to LDR.  


 >The HDR input in the **Pixel Inspector** measures everything in luminance or cd/m² or nits, which is why you want to use a pure white material since luminance is based on color. Taking that HDR value and multiplying it by pi will give you the Lux value.
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


---

# Nanite
new format of representing datat. (less data) with custom rasterizer (multiview)
- no need of lod's    
- store everything as image so mipmap  automated   
- mesh stored in clusters   
- classic pipeline is skiped

ograniczenia
- only uv0
- no morphs and wpo no splines
- no custom depth , vertex paint (on instances only import)
- transform only general matrix
- no custom uvs
- only solid


---
# Virtual texturing  streaming
New aproach to mips.  Divided in to tiles
- memory optimisation where we pay a small amount in performance.  
- better granularity
- load smaller part of image

1. Project settings > Engine Rendering > Enable
2. Enable Virtual Texture Streaming in texture options (or convert to vertual texture)
3. Sample type in material to: Virtual Textura

cost of normal sample even more gpu instructions (2 tez samples: 1 per stack and 1 per each  )
Virtual texture stack: - using same uvs  (see in material stat)

there is bulk convert on texture in browser to convert many at once

---

# Virtual texture runtime
same tech in runerttime in gpu  (shading cash)
not change frame to freme
- performance optimisation not memory
- frame to frame read cache
- camera position independend ()
- decoding cost small
1. create virtual texture asset.
2. use node runtime virtual texture

```
r.VT.borders 1

```
- stack as much with same uv  (base color spec ... nm )
---





# Ray trace light
Path Tracer
In addition to the Ray Tracer, we've included an unbiased Path Tracer with a full global illumination path for indirect lighting that creates ground truth reference renders right inside of the engine. T  

- DXR
- run with DX12
- In project settings: Ray Tracing, Support Cmpute sskincache
- In light: casting ray trace shadow

soft shadow
reflections (bounces 1)

---

## Staic Bake
Fog:  
`Static Light Scatter Intensity`  - intensity of scattered static lighting in the Volumetric Fog.
Sun:   
`Source Soft Angle` -
`Indirect light intensity` -  Increase bounce   

---


## ACES

```
UE4 ships with ACES as the default tonemapper but they did tweak it to make it a less shockingly different result to what people were used to before... which I think helps with the "8-bit ACEScg textures not a great idea" problem
[10:17 PM]
someone on ACEScentral figured out what the exact change was - I think broadly it's brighter and flatter than what you'd expect if you just took a scene authored for sRGB and interpreted it as ACEScg
[10:22 PM]
they did adopt the standard ODTs though which is very sensible - you can work in SDR then switch the output for an HDR TV without having a Huge Nightmare
```
