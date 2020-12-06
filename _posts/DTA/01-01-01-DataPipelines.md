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


### Paths

|Exports, Cache|
|---|
| Mesh  Export - ```$HIP/`opname("..")`/export/$OS.fbx``` |  
| Mesh  Cache -```$HIP/`opname("..")`/cache/$OS.bgeo```  |     
| Simulation   Cache - ```$HIP/`opname("..")`/cache/${OS}/$OS.$F3.bgeo``` |  
|**Bake**|
| Maps Bake -```$HIP/`opname("..")`/export/bake/${OS}/${OS}_$(CHANNEL).tif``` |      
||
|TextureSheet / MorionVector seqence - ```$HIP/`opname("..")`/export/bake/${OS}_sequence``` |      
|TextureSheet / MorionVector - ```$HIP/`opname("..")`/export/bake``` |  
||
|Vertex Anims  -```$HIP/`opname("..")`/export/vat_$OS/$OS_$(CHANNEL).exr``` |       
|``` $HIP/export/`chs("_component")`_vat```   |
|``` `chs("_project")`/`chs("_component")`_xxx.fbx```  |
||
|Niagara -``` $HIP/`opname("..")`/export/niagara/$OS.hbjson ``` |
||
|PDG ROP Geo -```$HIP/geo_`opname("../..")`/top/`opname("..")`/part`@top_name`.bgeo.sc```


```$HIP/.... .fbx``` -  FBX Character Export   KineFx  
```$HIP/.... .fbx``` - FBX Animation Output  KineFx  

### Folders

`$HIPNAME.hip`
fileA.fbx - export    
fileA_lod1.fbx - lod    
fileA_paint.fbx - export for painting    
fileA_lo.fbx - low to bake    
fileA_locage.fbx - cage to bake      
fileA_hi.fbx - high for bake     

`raw` - Sources     
`ref` - References      
`AssetName/export/NodeName.fbx` -       
`AssetName/export/bake/NodeName/NodeName_channel` -       
`AssetName/export/niagara/` -     
`AssetName/top/NodeName/NodeName.bgeo`  
`AssetName/zbrush/fileA.ztl` - Tool (ctrl shift T)  
`AssetName/material/fileA.sbs` - Substance     Designer / Painter          
`AssetName/material/fileA.png` - Export    / in same folder as  spp/sbs   


---

# Rules

- niezmienna nazwa noda-contenera
- modelowaną geometrie trzymaj w innym nodzie !!!  
- TOP net nie zmieni wedgeparamsa po zmianie nazwy noda

#### Attributes

Base
- `v@N` (vert) -  
- `@P`, `v@rest`, `v@Cd`, `i@id`, `@Alpha` (point)  
- `s@shop_materialpath` (prim) - to split mesh in partes / or do it by primitive Groups: Attr copy to `name`  

Manage
- `s@name` -  (prim) , joints names
- `i@class` -  (prim), reserved to connectivity   
- `i@id` -  particles    
- `s@tag` - string in new scatter
- `variation` - copy to point / new scatter


#### Sufixes

- **Mesh Parts** - oznaczenia czesci A B C D jak jest policzalna ilosc, jak nie to liczby  
- **Maps Channels** - `cd`,  `ao`, `cv` ,`th` ,`fb` ,`h` ,`a` ,`p` `nm`, `wn` ,`bn`

---

## Modeling
Houdini 1 U = 1m Zbrush - scale * 100  obj rotation ?    

- `UCX_*` - from houdini need to be in separated containers  named UCX_nameOfGeoContainer. - object level  (make container !!! and ROPnet > fbx)  







# P4
- `Accept Source` GEt clean file from repo, discarding your changes.  
- `Accept Target` Accepts the file local, overwriting repo.  
