---
title: Unreal Rendering Atmosphere
description: RAW NOTE.
categories:
 - RT
tags:
- Unreal
- Rendering
- Real Time
- Art
- Game Dev
---

# Atmosphere
Lowering contrast and saturation over distance, make color more like sky  
Skylight intensity is relative to the HDR  
Light - Radious and intensity keep both toghether. Mini roiughness light without reflections

 Direct lighted vs shaded intensity ratio   | |
  ---| -- |
~4:1 |sun/sky
~3:1 |sunrise/sunset  
~2:1 |overcast

>You can measure that by looking at a white surface with sun on it, and adding a shadow casting object then comparing the brightness of the lit to the shadowed areas. Modify skylight until its around 25% the value of the sun. Convert to linear space if comparing in screens photoshop. (adjustment->levels and set the midpoint to 0.4545)

## Light

1 cd = 625 unitless
1 cd = 1 lm/sr

Candelas, it is unaffected by its cone angle.
Lumens, its luminous power only applies to the solid angle affected by the light, in Steradians (sr).

#### Units

- Directional lights uses Direct Normal Illuminance, lux = (lm/m²)   
- Sky lights Luminance, cd/m²  `1 cd` = `1 lm/sr` = `625 unitless`     
- Emissive  Luminance, cd/m²




---

# Directional Light
`■` `Light Color` - **White**   Light Color     
`Temperature` - **6500 K**  Spectrum similar to black body with a correlated color temperature   
`x` `Intensity ` -   ??  


`Source Angle` - **0.5357** Angular Diameter of circle drawn on skybox for Sun   
[x] `Atmospheric / Fog Sunlight` - Fog on Hallo & sun location from sky

#### Light Shafts & Bloom
`Light Shafts` -  Max darkness / depth   
`Light Bloom` -    Scale / threshold / max bright / color


---



# Sky Atmosphere

>Work with SUN. Simulates **absorption** with **Mie** scattering and **Rayleigh** scattering. They themselves are made up of particles and molecules that have their own shape, size and density. When photons (or light energy) enters the atmosphere and collides with the particles and molecules there, it is either reflected (**scattered**)  or consumed (**absorbed**).  Different colors during day because angle to ground change the **distance light go through** Atmospheric density.

`■` `Ground Albedo` - Horizon color (can be modified by rayl...)  
`z` `Atmosphere Height` - 60 km up - default
[x] `Multiple scattering` - use  

#### Rayleigh
> Scatter Uniform-ish on the molecules smallest size than 1/10 of photon wave length. Longer wavelength less scattering, therefore **sky is Blue** (400 nm) is 5.8 more scattered than red (700 nm) 1.0  


`■` `Color` - Effect color   
`x` `Rayleigh Scattering Scale` - **0,0331** for Earth. - 0.0 more like selected color - 1.0 more like opposite to selected  color (shift original toward sun)      
`F` `Exponential Distribution` - Z - Distance Falloff. - 1 black  - 20 nicer falloff to  see horizon color (8 default)     

#### Mie
> More directional Interaction of light with larger particles  **Height fog** simulation. (dust, pollen, or air pollution) **absorbs light** causing the clarity of the sky to appear hazy by occluding light.  Aerosols Scattering.

`■` `Scattering Color` - Halo color + Inverted Horizon color   
`x` `Scattering Scale` - 0 - 5 Amount of Lightness    

`■` `Absorption Color` -  Color to delete ???????????????????      
`x` `Absorption Scale` 0 - 5  - Amount of Horizon darkens     

`F` `Anisotropy` - 0-1  - Halo Distribution.  0 - Uniformly, 1 - More Hallo     
`F` `Exponential Distribution` - Z - Distance Falloff.  0- on ground, 1 - whole sky.

#### Absorption
`■` `Color` - Color to absorb   
`x` `Absorption scale` - 0-1 Amount      
`z` `Tip Altitude`, `Tip Value`, `Width` -  Distribution    

#### Art
`■` `Sky Luminanse Factor` - Background Color  
`Aerial Perspedctive Distance Scale `  - Fog Distance    
`Taransmittance Min Light Elevation Angle` - Help maintain sun and shadows when sun under horizon    


`Height Fog Contribution`   - ~~Directional Inscattering fog Amount~~ ( **Added to Height fog** )  [allow contribution in project settings]   


```
r.SkyAtmosphere.Visualize 1
```


---

# Sky Light
> Emit light from captured cubemap  Require: **Recapture**


`■` `Light Color` -    
`x` `Intensity` -  Amount (always 1)   
`◻` `Low hemisphere Color` - Lower hemi color     

#### Capture Cube
`Distance threshold` - Near meshes cutoff    
`Capture emissive only` - Materials. Skips all lighting making the capture cheaper. (Capture Every Frame)    


#### DFAO


----


# Skydome
>Shape of skydome mesh is important when using some of theseexpressions since they will drive evaluation of those values. For example, if you use the functions to evaluate lighting on clouds, you can assume the skydome pixel world position represents the cloud world position in the atmosphere.  

### Using HDR

HDR sky: If exposure is to high (dark) you must multiply a lot HDR. Sky intensity will not work. If HDR have lot of stops wun will have huge values. But you cannot check value of sky in area.  

Default Auto cam:  Shutter 60 ISO 100 f-stop:4.   30000 -125000 lux sun light. sky luminance: 5000 cd/m2  

### Using Atmosphere
Settings: `Sky Atmosphere Compatible Material` - Enable     
Material: `Is Sky`, `Opaque`, `Unlit`    
Skybox: `No Cast Shadow`, `No Distance Field`  


##### Atmospheric

`Sky Atmosphere Light Disc Luminance` [0] -  sun ( rendered effect as u see it)     
`Sky Atmosphere View Luminance` - sky gragient ( rendered effect as u see it)   
basic setup: [SkyAtmosphere Light Disc Luminance + SkyAtmosphere View Luminance]    

`Sky Atmosphere Distant Light Scattered Luminance` - Cloud sky color ~~ambient tint~~  
setup: add clouds to sky [multi mask and add to basic setup]    
setup: add clouds to plane/particles (M_SkyTimeOfDay) (Translucent)
add smoke  

`Sky Atmosphere Light Direction` - Sun Angle of dir. Check if day - ( * 5 > clamp > lerp sun low/high)  

??: `Sky Atmosphere Aerial Perspective` - wide glow tint  
??: `Sky Atmosphere Light Luminance` - intensity/color of sunlight hitting atmosphere  

##### H Fog & Lihght

`Atmospherer Light Vector` - Sun Angle of dir.   
`Atmosphere Light Color` -     Old    
`Atmosphere Light Vector` - Old  
`Atmosphere Fog Color` - Old   



---


# Height Fog
>With Atmosphere are ADDITIVE So basic setup black

#### Inscattering
`■` `Color`  - Inscattering   
`x` `Density`,  - Density  
`x` `Density 2` - Density 2-nd      
`z` `Fog Height Falloff` - Falloff  
`z` `Fog Height Falloff 2` - Falloff 2-nd
`z` `Offset 2` - Offset 2-nd fog Z   
`Start Distance` -  Start  
`Fog Cutoff Distance` -  End (excluding skybox which already have fog baked into them)  

#### Directional Inscattering  
`■ Color` - Directional Inscattering   
`x` `Exponent` - 2-64  2 - huge Halo -  64 - Small Halo
`Start Distance` - Start   
`Max Opacity` - clamp   

#### Volume Fog


`□` `Albedo` -  The height fog particle reflectiveness used by Volumetric Fog. Water particles in the air have an albedo near white, while dust have slightly darker value  
`■` `Emissive`  - 	Light emitted by Exponential Height Fog. (Like Sky color but volum. better to set in sky)   
`x` `Extinction scale` -  0-10, larger than 1 cause fog particles everywhere absorb more light (Better use skylight!)  
`Scatter Distrib` - (-1-1) 0 equally all directions / 1 Halo ( + for shafts visible)   
`View Dist` - End Distance (0 + ext=0 to have no changes)  


`Override light color with fog` - match volume color to Height fog. (can mismatch surf light) Disable Emissive color below 1, (and partially disable albedo !!!!!!!)
  - (Directional Light has Atmosphere Sun Light enabled)
  - Fog `Inscattering Color` > Sky Light: `Volumetric Scattering Color`
  - Fog `Directional Inscattering Color` > Directional Light: `Scattering Color`


https://shaderbits.com/blog/ue4-volumetric-fog-techniques  







# Light Units

Lights | solid angle | 1 lm ≈ | 1 cd ≈ |
-- | -- | -- | -- |
Point | 4π sr | 49.7 *  (1 unitless) | 4 x 3.14 = 12.566 lm
Spot | 2π * (1 - cos(θ)) | 99.5 / (1 - cos(θ)) * (1 unitless)
Spot 44°|1.76 sr | 354 *  (1 unitless) | 1.76 *  (1 lm)
Rect  | 2π sr | 1.31  | 199 *  (1 unitless) | 3.14 *(1 lm)
