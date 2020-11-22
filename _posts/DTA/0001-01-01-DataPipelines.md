---
title: Data Pipelines

categories:
 - DTA
 - HOU
tags:
- CG
- Configs
description: .
permalink: /datapipelines/
---





# Paths


```$HIP/`opname("..")`/export/$OS.fbx``` - Mesh  Export   
```$HIP/`opname("..")`/cache/$OS.bgeo```  -  Mesh  Cache    
```$HIP/`opname("..")`/cache/${OS}/$OS.$F3.bgeo``` -  Simulation   Cache   

```$HIP/`opname("..")`/bake/${OS}/${OS}_$(CHANNEL).tif``` -  Maps Bake    
```$HIP/`opname("..")`/export/vat_$OS/$OS_$(CHANNEL).exr``` -  Vertex Anims    
```$HIP/`opname("..")`/bake/${OS}_sequence``` - TextureSheet/MorionVector seqence      
```$HIP/`opname("..")`/bake``` - TextureSheet/MorionVector   




#### Substance

```$HIP/`opname("..")`/material/fileA.sbs``` - Substance     Designer / Painter          
```$HIP/`opname("..")`/material/fileA.png``` - Export    / in same folder as  spp/sbs   



#### Zbrush
```$HIP/geo_`opname("..")`/zbrush/fileA.ztl``` - Tool (ctrl shift T)


### PDG
```$HIP/geo_`opname("../..")`/top/`opname("../..")`_part`@wedgeindex`.bgeo.sc``` - ROP Geometry




### Folders

`$HIPNAME.hip`
fileA.fbx - export    
fileA_LOD1.fbx - lod    
fileA_paint.fbx - export for painting    
fileA_lo.fbx - low to bake    
fileA_locage.fbx - cage to bake      
fileA_hi.fbx - high for bake     
` $HIP/raw/ ` - Sources    
` $HIP/ref/ ` - References    


---

# Rules

- niezmienna nazwa noda-contenera
- modelowaną geometrie trzymaj w innym nodzie !!!  

#### Attributes

- `s@name` -  prim  
- `i@class` -   reserved to connectivity   
- `i@id` -  particles ?   
- `s@tag` - string in  new scatter

#### Sufixes

**Mesh Parts** - oznaczenia czesci A B C D jak jest policzalna ilosc, jak nie to liczby  
**Maps Channels** - `cd`,  `ao`, `cv` ,`th` ,`fb` ,`h` ,`a` ,`p` `nm`, `wn` ,`bn`

---

# Configs

#### Substance


(*.spexp - E:\Documents\Allegorithmic\Substance Painter\shelf\export-presets)  

#### Zbrush


Documents>SaveAs ZBrush Document.ZBR   
Preferences>Enable customisation   and Ctrl+Alt drag
*.cfg - custom UI  Preference>StoreConfig  
*.zep - Brushes C:\Program Files\Pixologic\ZBrush 2020\ZStartup\BrushPresets  
*.zmt - Matcaps C:\Program Files\Pixologic\ZBrush 2020\ZStartup\Materials  


---





# Res

### res:
`2048`  
`4096^2` pix = `16 777 216` pix   =  (mb ?)  
`4096^2` pix = `33 550` points - `500` frames (~`16` sek)      
`8192`    

`3440 x 1440` personal   
`2560 x 1440`   
`3840 x 2160` 4K (4K UHD) (2160p)        
`4096 × 2160` 4K (DCI) movie ind   
`1920 x 1080` full HD 1080p  

`(16:9) 1.7778` HDTV format    
`(1.85:1)` WideScreen format       
`(2.35:1.00)` CinemaScope    

## Formats

`linear space` - RGB    
`gamma space` - sRGB - 2.2 Gamma  (1/2.2=0.4545)      
`bpc` -- bit per channel  
`pbi` - bits per image  
`LDR` - 8F  bits per channel    
`HDR` - 16F low precission     
`HDR` - 32F high precision   

WHAT FORMAT AND COMPRESSION TO UNREAL  

`*.tif` - loseless Adobe Tagged Image File Format, 8 or 16 bpc (to 48bit  transp can constain metadata like GeoTiff for Print    
`*.tga` - loseless Truevision Advanced (deep color 32 bpi = 8 bpc) only for UE  16/24/32 bits per pixel (24?) for video (No windows prev!)  
`*.png` - Portable Grap Network Graphic (48 bpi = 16 bit per channel bpc)   
`*.exr` - OpenEXR is Light & Magic  high dynamic range raster file    
`*.sbs` - Substance Designer Document     
`*.sbsar` - Substance Archive    
`*.iff`- maya “z-depth”    



---





# P4
`Accept Source` GEt clean file from repo, discarding your changes.  
`Accept Target` Accepts the file local, overwriting repo.  


---
# Tools

C:\Program Files\Side Effects Software\Houdini 18.0.432\bin\Gplay - przegladarka 3d  



```

### .env



PDG_IMAGEMAGICK = "..magic.exe"  
PDG_FFMPEG = ".. ffmpeg.exe"   
CURVES IN EDITOR: python2.7libs fcurves.py 3 files / HSITE = ""  

python:?
```
