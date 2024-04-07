---
title: U Lighting Setups
description: Atmosphere, Fog, Sun, Sky, Lumen
categories:
  - PXL
tags:
  - Unreal
  - Rendering
  - RealTime
  - GameDev
  - 3D
  - CG
permalink: /ugeo/
aliases:
  - ugeo
---
> Obsidian: 



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


hardwar / software rasterisation <<< check one for small another for big near trix

- instances for cpu - less actors
- hlod - racze dl dlow end hardware
not to much polys
- disk size can be big


- keep max (fix fn rasterisation) FFR  
 - WPO disable
 - opaque mat

overdraw
- overlaping geo
-closely stack togh geo
- paint mat ?

minimize bins
