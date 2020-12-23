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
|Maps Bake PDG  - ```$HIP/`opname("..")`/pdg/bake/${OS}/${OS}_`@wedgeindex`_$(CHANNEL).tif```  
|**Game**|
|TextureSheet / MorionVector seqence - ```$HIP/`opname("..")`/export/bake/${OS}_sequence``` |      
|TextureSheet / MorionVector - ```$HIP/`opname("..")`/export/bake``` |  
|Heightfields - $HIP/`opname("..")`/export/heightfields/$OS|
|Vertex Anims  -```$HIP/`opname("..")`/export/vat_$OS/$OS_$(CHANNEL).exr``` |       
|Vertex Anims  -``` $HIP/export/`chs("_component")`_vat```   |
|Vertex Anims  -``` `chs("_project")`/`chs("_component")`_xxx.fbx```  |
|Niagara -``` $HIP/`opname("..")`/export/niagara/$OS.hbjson ``` |
|**KineFx**|
|FBX Character Export ```$HIP/.... .fbx```
|FBX Animation Output ```$HIP/.... .fbx```  
|**PDG**|
|PDG TopGeo - ```$HIP/`opname("../..")`/export/pdg/${OS}_`@wedgeindex`.fbx```
|PDG cache - ```$HIP/`opname("../..")`/cache/pdg/${OS}/${OS}_`@wedgeindex`.$F4.fbx```


$HIP/`opname("..")`/export/bake/`@top_name`/`opname("..")``@top_name``@lod_name``@bake_set`_$(CHANNEL).tif

### Folders

- `$HIPNAME.hip`  
- `fileA.fbx` - export   `fileA_lod1.fbx`
- `fileA_lo.fbx` `fileA_hi.fbx` `fileA_locage.fbx` - low to bake   `fileA_paint.fbx` - export for painting     
- `/raw/` - Sources     
- `/ref/` - References      
- `/AssetName/`
  - `/export/`
    - `NodeName.fbx` -       
    - `/bake/NodeName/NodeName_channel` -       
    - `/niagara/` -     
  - `/top/NodeName/NodeName.bgeo`  
  - `/zbrush/fileA.ztl` - Tool (ctrl shift T)  
  - `/material/fileA.sbs` - Substance     Designer / Painter          
  - `/material/fileA.png` - Export    / in same folder as  spp/sbs   


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
- `s@tag` - string in new scatter, tree
- `variation` - copy to point / new scatter

Uv
- `v@uv` - (vert)
- `v@uv1` ?.
- `i@udim=1001;` - (prims)
- `i@island=3;` - (prim)  

#### Sufixes

- **Mesh Parts** - oznaczenia czesci A B C D jak jest policzalna ilosc, jak nie to liczby  
- **Maps Channels** - `cd` color, `rg` roughness,  `ao` ambient, `cv` curvature, `th` thickness,`fb` ,`h` ,`a` ,`p` `nm`, `wn`world normal  ,`bn` bent normal, `wp` - world position (WD - WPO VA )
e

---

# Modeling
Houdini 1 U = 1m Zbrush - scale * 100  obj rotation ?    

- `UCX_*` - from houdini need to be in separated containers  named UCX_nameOfGeoContainer. - object level  (make container !!! and ROPnet > fbx)  







# P4
- `Accept Source` GEt clean file from repo, discarding your changes.  
- `Accept Target` Accepts the file local, overwriting repo.  
