---
title: U Lighting Setups
description: Atmosphere, Fog, Sun, Sky, Lumen
categories:
 - PXL
tags:
- Unreal
- Rendering
- Real Time
- Light
- Art
- Game Dev

permalink: /ulight/

---

[Unreal Rendering Features](/ue_rendering_features/)

Sky is black and the sun is white


# Light



1 cd = 625 unitless
1 cd = 1 lm/sr

Candelas, it is unaffected by its cone angle.
Lumens, its luminous power only applies to the solid angle affected by the light, in Steradians (sr).



### Units

- Directional lights uses Direct Normal Illuminance, lux = (lm/m²)   
- Sky lights Luminance, cd/m²  `1 cd` = `1 lm/sr` = `625 unitless`     
- Emissive  Luminance, cd/m²

[Light Data](/light/)



---

## Directional Light
- `■` `Light Color` - **White**   Light Color     
- `Temperature` - **6500 K**  Spectrum similar to black body with a correlated color temperature   
- `x` `Intensity ` -   ??  


- `Source Angle` - **0.5357** Angular Diameter of circle drawn on skybox for Sun   
- [x] `Atmospheric / Fog Sunlight` - Fog on Hallo & sun location from sky

### Light Shafts & Bloom
- `Light Shafts` -  Max darkness / depth   
- `Light Bloom` -    Scale / threshold / max bright / color


---



## Sky Atmosphere

Work with SUN. Simulates **absorption** with **Mie** scattering and **Rayleigh** scattering. They themselves are made up of particles and molecules that have their own shape, size and density. When photons (or light energy) enters the atmosphere and collides with the particles and molecules there, it is either reflected (**scattered**)  or consumed (**absorbed**).  Different colors during day because angle to ground change the **distance light go through** Atmospheric density.

- `■` `Ground Albedo` - Horizon color (can be modified by rayleigh)  
- `z` `Atmosphere Height` - **60 km** up - default
- [x] `Multiple scattering` - Use  

### Rayleigh
Scatter Uniform-ish on the molecules smallest size than 1/10 of photon wave length. Longer wavelength less scattering, therefore **sky is Blue** (400 nm) is 5.8 more scattered than red (700 nm) 1.0  


- `■` `Color` - Effect color   
- `x` `Rayleigh Scattering Scale` - **0,0331** for Earth. - 0.0 Black sky (no scattering), white Sun - 1.0 more like opposite to selected  color
- `F` `Exponential Distribution` - **8 km** Z falloff - 1 black  - 20 (more intense, caused by thicker layer)


### Mie
More directional Interaction of light with larger particles  **Height fog** simulation. (Aerosols Scattering; dust, pollen, or air pollution) **absorbs light** causing the clarity of the sky to appear hazy by occluding light.  

- `■` `Scattering Color` - Halo color + Inverted Horizon color   
- `x` `Scattering Scale` **0.003996** -  Amount of Lightness - 0 - 5  more fog and scatter > shadows less contrast   
- `■` `Absorption Color` -  Color to remove
- `x` `Absorption Scale` **0.000444**  - Amount of particles (darkens) 0 - 5 dark
- `F` `Anisotropy` - **0.8**   - Halo Distribution.  0 - Uniformly, 1 - More Hallo     
- `F` `Exponential Distribution` - **1.2**  Z falloff -   0 - on ground, 1 - whole sky.

### Absorption
Ozon molecules:
10 -25km density increase 25-40km decrease.  
- `■` `Color` - Color to absorb   
- `x` `Absorption scale` - 0-1 Amount      
- `z` `Tip Altitude`, `Tip Value`, `Width` -  Distribution    

### Art
- `■` `Sky Luminanse Factor` - Multiply background color  
- `Aerial Perspedctive View Distance Scale` **1** - Fog Distance 0 less - 2500 more    
- `Aerial Perspective Start Depth` **0.1 km** - Start dist 0 near - 10 far (performance save )
- `Taransmittance Min Light Elevation Angle` **-90** - Help maintain sun and shadows when sun under horizon    


- `Height Fog Contribution`   - ~~Directional Inscattering fog Amount~~ ( **Added to Height fog** )  [allow contribution in project settings]   


```
r.SkyAtmosphere.Visualize 1
```


---

## Sky Light
Cubemap Capture.  Position is important !
Emit light from captured cube map  Require: **Recapture**
Real Time Capture mode enables 9-frames time slicing to distribute a single frame's capture over multiple frames.

- `■` `Light Color` -    
- `x` `Intensity` -  Amount (always 1)   
- `◻` `Low hemisphere Color` - Lower hemi color     

##### Capture Cube
- `Distance threshold` - Near meshes cutoff    
- `Capture emissive only` - Materials. Skips all lighting making the capture cheaper. (Capture Every Frame)    

##### DFAO


----


## Sky dome
Shape of sky dome mesh is important when using some of these expressions since they will drive evaluation of those values. For example, if you use the functions to evaluate lighting on clouds, you can assume the sky dome pixel world position represents the cloud world position in the atmosphere.  



### Sky dome - Traditional

**Material setup**  
- `Atmosphere Light Vector` - **Angle** - of sun dir.   
- `Atmosphere Light Color` - Cd light         
- `Atmosphere Fog Color` - Cd fog

### Sky HDR

HDR sky: If exposure is to high (dark) you must multiply a lot HDR. Sky intensity will not work. If HDR have lot of stops wun will have huge values. But you cannot check value of sky in area.  

Default Auto cam:  Shutter 60 ISO 100 f-stop:4.   30000 -125000 lux sun light. sky luminance: 5000 cd/m2  



### Sky dome - SkyAtmosphere
**Material properties**  
- Settings: `Sky Atmosphere Compatible Material` - Enable     
- Material: `Is Sky`, `Opaque`, `Unlit`    
- Mesh: `No Cast Shadow`, `No Distance Field`  

**Material setup:** - Sky + Sun + (Cloud*mask):     
- `Sky Atmosphere View Luminance` - **Sky color** - (final sky gradient with cutoff below horizon)   
- `Sky Atmosphere Light Disc Luminance` [0] -  **Sun circle** - (draw circle on skybox)
- `Sky Atmosphere Distant Light Scattered Luminance` * `mask` - **Cloud color** - (like atmoshere ambient tint [ raylight scatter & foga colors]) Ambient light / tint




### Clouds & Smoke - SkyAtmosphere

**For smoke particle** (M_SkyTimeOfDay) (Translucent & without isSky property):
- `Sky Atmosphere Aerial Perspective` - **Fog ..** - How wide/glow/tint sun    (color but ) Sun white glow and tint - wider glow of sun come from sky.
- `Sky Atmosphere Light Luminance` [0] - **Sun color /intensity** - light hitting atmosphere  [NOT ALWAYS VISIBLE] LIGHTER (color = color of light at 1 lumen )
- `Sky Atmosphere Light Direction` - **Angle** - of sun dir. Check if day - ( * 5 > clamp > lerp sun low/high)  

new:
- Atmosphere sun light luminance on ground < SUN COLOR 1:1 DARKER (same as light at 10 lumens)




---


## Height Fog
Height fog is additive so to get it to work with SkyAtmosphere
- support sky atmosphere affecting height fog
- both colors to black

### Inscattering
- `■` `Color`  - Inscattering   
- `x` `Density`,  - Density  
- `x` `Density 2` - Density 2-nd      
- `z` `Fog Height Falloff` - Falloff  
- `z` `Fog Height Falloff 2` - Falloff 2-nd
- `z` `Offset 2` - Offset 2-nd fog Z   
- `Start Distance` -  Start  
- `Fog Cutoff Distance` -  End (excluding skybox which already have fog baked into them)  

### Directional Inscattering  
- `■ Color` - Directional Inscattering   
- `x` `Exponent` - 2-64  2 - huge Halo -  64 - Small Halo
- `Start Distance` - Start   
- `Max Opacity` - clamp   


## Volume Fog


- `□` `Albedo` -  The height fog particle reflectiveness used by Volumetric Fog. Water particles in the air have an albedo near white, while dust have slightly darker value  
- `■` `Emissive`  - 	Light emitted by Exponential Height Fog. (Like Sky color but volum. better to set in sky)   
- `x` `Extinction scale` -  0-10, larger than 1 cause fog particles everywhere absorb more light (Better use skylight!)  
- `Scatter Distrib` - (-1-1) 0 equally all directions / 1 Halo ( + for shafts visible)   
- `View Dist` - End Distance (0 + ext=0 to have no changes)  


`Override light color with fog` - match volume color to Height fog. (can mismatch surf light) Disable Emissive color below 1, (and partially disable albedo !!!!!!!)
  - (Directional Light has Atmosphere Sun Light enabled)
  - Fog `Inscattering Color` > Sky Light: `Volumetric Scattering Color`
  - Fog `Directional Inscattering Color` > Directional Light: `Scattering Color`




[pxl.ink Unreal Volumes](/uvolume/)




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

---


# Setups

## Capture Atmosphere from Photos

##### Photo references

Automatic Exposure Bracketing examples:  
13EV's of scene light for interiors (7 shots with 2EV)  
26EVs for Outdoors - Sun visible sometimes even on -20EV  

##### Shoot
- Shoot RAW - 16 bit if possible. HDR: (if not PBR will be affected)   
- Orient set to recognize front direction  
- Shoot in central point of scene: Cannot change EV during shot.    

`Color checker` - white ballans. from differences between shoot and CG create transform matrix to neutralize colour cast (shoot fulll exposure)   
`Gray card` - to set base EV (correctly expoing for 18% grey calibration card (fill frame) which is oriented twoward main light (without shadow))  
`Gray ball` -  lighting intensity and direction 18% grey (like lambert shading)   
`Chroma ball` -  help to correct Lightprobe rotation and light locations- shoot front and side   
`Lightprobe` shot for HDRI shoot with 8mm lens 3 shoots 0 120 240  
`RAW` > `TIFF` (PTGUI software) > merge to  `EXR` panorama  > color correction

##### Unreal Light
- For unreal HDRI mask out light sources to get ambient light   
- Gray Ball 18% Sepecular 0.7 Roughtnss 0.85 - paint on physical grayball    
- Position ball in exact location, find front orientation   
- Turn off PP    
- Set lights in proper location  
- Set lights intensity: Go to HDR view and match chroma ball with reference image by seting   



Old setup
 - `Sky box` > `Exp fog` > `Sky Light` > `Directional Light` > `Secondary lights` > `Cam Post` > `Color Grading`



 -------------
 # Baked light

 ## Static Bake
 Fog:  
 `Static Light Scatter Intensity`  - intensity of scattered static lighting in the Volumetric Fog.
 Sun:   
 `Source Soft Angle` -
 `Indirect light intensity` -  Increase bounce   
