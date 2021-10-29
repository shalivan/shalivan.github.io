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


# Cache H19 Workflow
- time dependent - add `$F` to name.
- Version add `v1`
- Wedge add `w0`
- is simulated - off can multiple process


-----
- Frame
- Wedges

Using file cache with rop geo TOP. with sequences choose automatic.


# Paths

- All Assets are folders named after Object Container
- Modeling in _geo, then import to other Object

### Paths

|Exports, Cache||
|---|---|
| Export | ```$HIP/`opname("..")`/export/$OS.fbx``` |  
| Cache |```$HIP/`opname("..")`/cache/``` v1/w0/$OS.bgeo.sc  |     
|**Bake**|
| Maps Bake |```$HIP/`opname("..")`/export/bake/${OS}/${OS}_$(CHANNEL).tif``` |   
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
|Vellum cache | ```$HIP/cache/...```
|**COP**|
|COP image | ```$HIP/`opname("..")`_cop/${OS}.exr```
|Embeded assets| opdef:/Sop/...



|||
|---|---|
|Name from attribute|$HIP/`details("../filecache1","attribute1")`.fbx
|offset 0010-0260  |$HIP/name.`padzero(4,$F-10)`.png  
|range loop 0000-0250 |$HIP/name.`padzero(4,$F%251)`.png    
|range loop 0050-0300 |$HIP/name.`padzero(4,($F-50)%251+50)`.png    
|hold first |$HIP/name.`padzero(4,min($F,250)`.png   
|hold last|$HIP/name.`padzero(4,max($F,1)`.png      
|clamp|$HIP/name.`padzero(4,clamp($F,1,250))`.png  



### Folders

- `$HIPNAME.hip`  
- `$HIP/raw/` - Sources     
- `$HIP/ref/` - References      
- `$HIP/ObjectA/`
  - `/export/v1/w0/`
    - `fileA.fbx` -     
    - `fileA_lod1.fbx`  
    - `fileA_lo.fbx`
    - `fileA_hi.fbx`
    - `fileA_locage.fbx`
    - `fileA_paint.fbx`
    - `/bake/fileA/fileA_channel.png`        
    - `/niagara/` -     
  - `/cache/`  
  - `/zbrush/fileA.ztl` - Tool (ctrl shift T)  
  - `/material/fileA.sbs` - Substance     Designer / Painter          
  - `/material/fileA.png` - Export    / in same folder as  spp/sbs   


### Files

##### Sufixes

- **Mesh Parts** - A B C D
- **Maps Channels**
  - `cd` - Color
  - `rg` - Roughness  
  - `ao` - Ambient
  - `cv` - Curvature
  - `th` - Thickness
  - `fb`
  - `h`
  - `a`
  - `p`
  - `nm`/`wn` - world normal  ,`bn` bent normal, `wp` - world position va

#### Attributes

Base
- `v@N` (vert) -  
- `@P`, `v@rest`, `v@Cd`, `i@id`, `@Alpha` (point)  
- `s@shop_materialpath` (prim) - to split mesh in partes / or do it by primitive Groups: Attr copy to `name`  

Manage
- `s@name` -  (prim) , joints names
- `i@class` -  (prim), reserved to connectivity   
- `i@id` -  particles, ctrl points for animation     
- `s@tag` - string in new scatter, tree
- `variation` - copy to point / new scatter

Uv
- `v@uv` - (vert)
- `v@uv1` ?.
- `i@udim=1001;` - (prims)
- `i@island=3;` - (prim)  



---
# Unreal Import

||SM (def)|VA3||SK|PP2|
|---|---|---|---|---|---|
Skeletal Mesh | | | |On| -
Generate Missing Collision | ||||-
Staticm MeshLODGroup | ||||-
Vert Color |  |Repleace|||Repleace|
Remove Degenerates || | x|| -
Building Adjacency Buffer | || x|| -
Building Reversed Index Buffer | | | x|| -
Generate Lightmap UVs | ||||-
One Convex Hull per UCX | || x||-
Combine Meshes | || x||-
Transform Vertex to Absolut | |On| x|| ?
Import Mesh LOD's || depending on Houdini |||-
Normal Import |  |Import Nm & Tang| Import Nm || ImportNm
Normal Generation | || Mikk TSpace||-
Compute Weighted Normal || | x || -
|.|
Transform|  |1| ||-
|.|
Convert Scene |  |On| x || On
Force Front XAxis  | || || x
Convert Scene to Unit | ||||-
Override Full Name | |On| x||-
|.|
Material | ||||-
Reorder mat to fbx |  | On|||-


---

# Collision

- `UCX_*` - from houdini need to be in separated containers  named UCX_nameOfGeoContainer. - object level  (make container !!! and ROPnet > fbx)  


# Digital Assets

#### Asset node
RMB on node >
- `Create digital Asset`...  
- `Digital Asset` >
  - create new:  
  - preferences:   

- `Digital Asset` >
  - save ass
  - increase major

- `Allow Editing`
- `Match Definition`
- ``

#### Library

# P4
- `Accept Source` GEt clean file from repo, discarding your changes.  
- `Accept Target` Accepts the file local, overwriting repo.  
