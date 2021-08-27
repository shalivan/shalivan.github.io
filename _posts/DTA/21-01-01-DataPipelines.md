---
title: Data Pipes

categories:
 - DTA
 - HOU
tags:
- CG
- Configs
- Pipelines
- Data
description: Pipelines
permalink: /pipes/
---


TOP cacahe
$HIP/`opname("../..")`/cache/`opname("../..")`/$OS.$F.bgeo

# Paths


### Paths

|Exports, Cache||
|---|---|
| Export | ```$HIP/`opname("..")`/export/$OS.fbx``` |  
| Cache Static |```$HIP/`opname("..")`/cache/$OS.bgeo```  |     
| Cache Simulation | ```$HIP/`opname("..")`/cache/${OS}/$OS.$F3.bgeo``` |  
|**Bake**|
| Maps Bake |```$HIP/`opname("..")`/export/bake/${OS}/${OS}_$(CHANNEL).tif``` |    
|Maps Bake PDG  | ```$HIP/`opname("..")`/pdg/bake/${OS}/${OS}_`@wedgeindex`_$(CHANNEL).tif```  
|**Game**|
|TextureSheet / MorionVector seqence | ```$HIP/`opname("..")`/export/bake/${OS}_sequence/``` |      
|TextureSheet / MorionVector | ```$HIP/`opname("..")`/export/bake/``` |  
|Heightfields | ```$HIP/`opname("..")`/export/heightfields/$OS/``` |
|Vertex Anims  |```$HIP/`opname("..")`/export/vat_$OS``` |       
|Niagara | ``` $HIP/`opname("..")`/export/niagara/$OS.hbjson ``` |
|Impostors| ```$HIP/`opname("..")`/export/${OS}_impostor/sequence/${OS}.$F4.exr``` |
|Impostors| ```$HIP/`opname("..")`/export/${OS}_impostor/${OS}_beauty.exr``` |
|**KineFx**|
|FBX Character Export | ```$HIP/.... .fbx```
|FBX Animation Output | ```$HIP/.... .fbx```  
|**Vellum** |
|Vellum cache | ```$HIP/cache/heightfield/$OS.bgeo.sc```
|**PDG**|
|PDG TopGeo | ```$HIP/`opname("../..")`/export/pdg/${OS}_`@wedgeindex`.fbx```
|PDG cache | ```$HIP/`opname("../..")`/cache/pdg/${OS}/${OS}_`@wedgeindex`.$F4.fbx```
|**COP**|
|COP image | ```$HIP/`opname("..")`_cop/${OS}.exr```

```
OLD
|Vertex Anims  |```$HIP/`opname("..")`/export/vat_$OS/$OS_$(CHANNEL).exr``` |  
|Vertex Anims  |``` $HIP/export/`chs("_component")`_vat```   |
|Vertex Anims  |``` `chs("_project")`/`chs("_component")`_xxx.fbx```  |
```


$HIP/`opname("..")`/export/bake/`@top_name`/`opname("..")``@top_name``@lod_name``@bake_set`_$(CHANNEL).tif   
$HIP/name.$F4.png   
$HIP/name.`padzero(4,$F-10)`.png - offset 0010-0260   
$HIP/name.`padzero(4,$F%251)`.png - range loop 0000-0250    
$HIP/name.`padzero(4,($F-50)%251+50)`.png - range loop 0050-0300    
$HIP/name.`padzero(4,min($F,250)`.png - hold first   
$HIP/name.`padzero(4,max($F,1)`.png - hold last     
$HIP/name.`padzero(4,clamp($F,1,250))`.png - clamp   


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
# Unreal Import

|||VA3|SM|SK|
|---|---|---|---|---|
Skeletal Mesh | | | |x
Generate Missing Collision | ||
Staticm MeshLODGroup | ||
Vert Color |  |Repleace|
Remove Degenerates || | x
Building Adjacency Buffer | || x
Building Reversed Index Buffer | | | x
Generate Lightmap UVs | ||
One Convex Hull per UCX | || x
Combine Meshes | || x
Transform Vertex to Absolut | |On| x
Import Mesh LOD's || depending on Houdini |
Normal Import |  |Import Nm & Tang| Import Nm
Normal Generation | || Mikk TSpace
Compute Weighted Normal || | x
|.|
Transform|  |1| |
|.|
Convert Scene |  |On| x
Force Front XAxis  | ||
Convert Scene to Unit | ||
Override Full Name | |On| x
|.|
Material | |
Reorder mat to fbx |  | On


---
# Modeling
Houdini 1 U = 1m Zbrush - scale * 100  obj rotation ?    

- `UCX_*` - from houdini need to be in separated containers  named UCX_nameOfGeoContainer. - object level  (make container !!! and ROPnet > fbx)  



# Digital assets

Adress to 'digital asset' embeded assets: opdef:/Sop/...



# P4
- `Accept Source` GEt clean file from repo, discarding your changes.  
- `Accept Target` Accepts the file local, overwriting repo.  
