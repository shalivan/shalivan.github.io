---
title: Houdini
categories:
  - DTA
tags:
  - CG
  - Houdini
  - Shortcuts
  - Configs
  - NodesGraph
  - Software
  - 3D
description: Configs
permalink: /houdiniconfigs/
---
> Pxlink: [TUT](/tutmain/) [Material data](/matdata/)   
> Obsidian: [[TUT]] [[16-02-01-Rendering]]  [[08-01-01-Material]] [[18-01-01-Color]]  [[14-01-01-Procedural]]  [[11-01-01-Math]] [[12-01-01-Gaea]] [[16-02-01-Substance_Designer]] [[17-01-01-Modeling]] [[17-01-01-Modeling_Foliage]] 


> [[02-01-01-LSystem]]  [[03-01-01-Karma]] [[04-01-01-Mantra]] [[05-01-01-Heightfields]]  [[06-01-01-CHOP]] [[07-01-01-PDG]]  [[08-01-01-CFX]]  [[10-01-01-LAB]] [[11-01-01-COP]] [[12-01-01-USD]]  [[13-01-01_VOP]] [[13-01-01-SOP]] [[13-01-01-SOP-curves]]

> [[01-01-01-Noise]] [[02-01-01-V_DrawCurves]] [[02-Vex_Volume]] [[03-01-01-V_Measure]] [[13-01-01_VOP]] [[05-01-01-V_Orientation]] [[07-01-01-V_Strings]]  [[08-01-01-V_Expressions]]  [[09-01-01-V_Attribs]] [[10-01-01-V_Syntax]]  [[12-01-01-Python-hou]]

> [[01-01-01-FLIP]] [[01-01-01-PYRO_Dense]] [[01-01-01-RBD_SOP]] [[01-01-01-RBD]] [[01-01-01-Vellum]] [[01-01-01-Vellum_SOP]]


|Operation type|houdini shorts|Tools|
|-|-|-|
|Enter Mode|`ENTER`|Enter modeling mode
|Camera|`Alt` + `RMB`|Rot as cam
| | `RMB`|Rot around
| |`Alt` + `MMB` / `LMB` + `RMB`|Pan
| |`LMB`|Zoom
| |`MMB`|Move tool


--------------



# CUSTOM
`Shift` + `W` - In all windows wireframe mode   
~~`Alt` + `W`~~ - close window  
~~`Ctrl` + `1`,`2`~~ ... - change   
~~`C` is visualize~~ should be: comment
`9` selection group        
`\` - manual update   `|` - auto update      
` ' ` - RESELECT FOR CURENT TOOL     
` ~ ` - SECURE SELECTION  




# załozenie do modelowania 

szybki przeskok do porzednich nodów na dodatkowym scrollu ???


ROspisac shortcuty w zaleznosci od trybu w jakim jesteś 

shortcuty w nodach 
shortcuty globalne 




#### Match translate
> is icon on the right of transform params click, and select obj u want rotate to.




----



# Viewport Manipulation

| | | |
|-|-|-|
|`T` | Transform  | W
|`R` | Rotate   | E
|`E` | Scale  | R
|`Y` | Cycle  |  -
|`M` | World Coordinates    | !!
















---

### Pivot / Handle

For animation. Permanent pivot of object.

| | | |
|-|-|-|
| `'`+`Shift`/`Insert`| **Pivot** - pivot transform change parameter.
| `'` | **Handle** - leave pivot unaffected. Detached Viewport handle temporary. For modeling and placement.

| | | |
|-|-|-|
|`RMB>presistant` | For enable 2nd handles!   |
|`RMB>SnapTo..` | Pivot or centroid.  |
|`RMB>HandleParameters` | Options  |
|`RMB>Local/Global` | Local pivot points vs Global - centroid of all  |
|`RMB>TranslateGloballyInLocalControl` | Local transform of last selected|


### Align  
Hover over geometry .. Y is up.
Check if you have object or world aligned handles it change behaviour

| | |
|-|-|
|`:` /  `:` + `Shift` | Align (`RMB>OrientationPeaking`).       
|`selct placement` + `Shift` | only rotate    
|`selct placement` + `Ctrl` | move dont rotate   
|`selct placement` + `Ctrl` + `Shift` | lookat Y  (to change click handle with ctrl)   
|`select axis` + `drag` | secondaty axies direction  

### Snap

### Grid plane

| | |
|-|-|
|`/` | Align Grid   
|`?`  |


----



# Viewport Main

|               |                                       |     |
| ------------- | ------------------------------------- | --- |
| `Alt`+`Space` | wieport                               |     |
| `B`           | show uv layout !!!!!                  |     |
| `9`           | select by group                       |     |
| `H`           | hide `H`+`ctrl`/`shift`   ??          |     |
|               |                                       |     |
| `F2`-`F5`     | Selection types box/lasso/paint/laser |     |
![[select_mode_lasso.svg]]
![[select_mode_boxselect.svg]]
![[select_mode_brush.svg]]
![[select_mode_laser.svg]]

![[select_visible.svg]]
![[select_contained.svg]]
### Hide


----


# Viewport Selection

### Selection modes:  


![[select_vertices.svg]]
![[select_points.svg]]
![[select_edges.svg]]
![[select_faces.svg]]

| | | |
|-|-|-|
|`Shift`+`V` | backmasking    
|`Shift`+`C` | contained  

### Selection modify:  

|                                        |                                    |     |
| -------------------------------------- | ---------------------------------- | --- |
| `N`                                    | select all                         |     |
| `Shift`+`N`                            | select none                        |     |
| `Shift`+`B`                            | bounds                             |     |
| `Shift`+`Ctrl`+`E` (on edges)          | pgrowth oli age boundary           |     |
| `Shift`+`G`                            | Growth selection                   |     |
| `Shift`+`S`                            | Shrink selection                   |     |
|                                        |                                    |     |
| `A`+`ctrl`/`shift`+`[MMB]`/`[RMB]`     | full selection / partial selection |     |
| `Shift` + `P`                          | Set sellection pattern             |     |
| `Shift` + `🡰` `🡲` `🡱` `🡳`          | Growth pattern                     |     |
| `Shift` + `Ctrl` + `🡰` `🡲` `🡱` `🡳` | Growt pattern till the end         |     |
| `K`                                    | Growth till paint under mouse      |     |




## [Edit] ![[edit.svg]] SOP 

|             |                            |     |
| ----------- | -------------------------- | --- |
| `L`         | Slide on Surface           |     |
| `H`         | Peak                       |     |
| `B`         | Sculpt                     |     |
|             |                            |     |
| `Y`         | Edit                       |     |
| `Shift`+`T` | Tweek mode   (no handles ) |     |

----

![[polyextrude.svg]]

edge / poly 

![[edgecollapse.svg]]  , ![[fuse.svg]] , ![[pointweld.svg]] ,![[dissolve.svg]] , ![[blast.svg]] , ![[delete_circle.svg]]
edge / points / poly 


![[bridge.svg]]
edges  / NOT WORKING ON POLYS 


![[polybevel.svg]]


![[polyfill.svg]]


![[clip.svg]]
F + LMB  - Draw plane 
G - display wire in
H - diaplay plane



![[polysplit.svg]]

![[mirror.svg]]


![](/src/hou/cfg/wheel1.png)

---


|                        | Operation type    | houdini shorts       | Tools                                            |     |
| ---------------------- | ----------------- | -------------------- | ------------------------------------------------ | --- |
|                        | Snap              | on wheel menu        |                                                  |     |
|                        | ConstructionPlane | on wheel menu        |                                                  |     |
|                        | Comon             | `Shift` + `M`        | Mirror selection in place                        |     |
|                        |                   | `Ctrl` + `+`         | Subdivide                                        |     |
|                        |                   | `D`                  | Display                                          |     |
|                        |                   | `F`                  | Focus                                            |     |
|                        |                   | `G`                  |                                                  |     |
|                        |                   | `Space`              | Context wheel                                    |     |
|                        |                   | `Q`                  | Repeat                                           |     |
|                        |                   | `Ctrl` +  `Q`        | Collapse stack                                   |     |
|                        |                   | Scroll               | Smooth selection                                 |     |
|                        | Hide              | `H`                  | Hide                                             |     |
|                        |                   | `Ctrl` + `H`         | Invert                                           |     |
|                        |                   | `Shift` + `H`        | Unhoide                                          |     |
|                        | Selection Context | `1`                  | Multi select                                     |     |
| ![[select_points.svg]] |                   | `2`                  | Points                                           |     |
| ![[select_edges.svg]]  |                   | `3`                  | Edges                                            |     |
| ![[select_faces.svg]]  |                   | `4`                  | Polys                                            |     |
|                        |                   | `ctrl` + `1-4`       | Convert selection to other type                  |     |
|                        | Pivot             | on wheel menu        |                                                  |     |
|                        | Coordinates       | `Shift` + `Q`        | Coords loop  (obj, world, viewport,plane, tweek) |     |
|                        | Move Constraints  |                      |                                                  |     |
|                        | Selection         | `S` / `Shift`  + `S` | Select                                           |     |
|                        | Selection         | `A` / `Shift`  + `A` | Semi loop                                        |     |
|                        |                   | `Shift` +  `F`       | Fill to all contained in type                    |     |
|                        |                   | `Shift` +  `S`       | Shrink                                           |     |
|                        |                   | `Shift` +  `G`       | Grow                                             |     |
|                        |                   | `Shift` +  `J`       | Pattern                                          |     |
|                        |                   | `Shift`  + `D`       | Normal / Fill selections to borders of group     |     |
|                        | Select Groups     | `Shift` +  `1`       | Toggle select types                              |     |
|                        |                   | `Shift` +  `2`       | Connected 3d                                     |     |
|                        |                   | `Shift` +  `3`       | Uv                                               |     |
|                        |                   | `Shift` +  `4`       | Name                                             |     |
|                        |                   |                      | Groups                                           |     |
|                        |                   |                      | Normal                                           |     |
![[hide.svg]]
![[transform.svg]]
![[scale.svg]]
![[move.svg]]
![[snap.svg]]
![[snap_curve.svg]]
![[snap_point.svg]]
![[snap_grid.svg]]

| Snap          | Point | Edges |
| ------------- | ----- | ----- |
| `Shift` + `E` |       |       |
| `Shift` + `R` |       |       |
| `Shift` + `T` |       |       |
| `Shift` + `Y` |       |       |


![[attribdelete.svg]]

| Edit geo tools        | Point         | Edges                 | Border        | Poly           |     |
| --------------------- | ------------- | --------------------- | ------------- | -------------- | --- |
| `Ctrl` + `A`          | -             | Make circle           | Make circle   | Circle         |     |
| `Ctrl` +  `D`         | Evenly spaced | Evenly spaced         | Evenly spaced | Square         |     |
| `Ctrl` +  `G`         | Straighten    | Straighten            | Straighten    | Flatten n-gone |     |
| `Ctrl` +  `X`         | Fuse          | Fuse                  | Fuse          | Fuse           |     |
| `Ctrl` +  `Shift` `X` | Delete        | Delete                | Delete        | Delete         |     |
| `Ctrl` +  `C`         | Relax         | Split Knife like tool | Bridge / Fill | Bridge / Fill  |     |
| `Ctrl` +  `V`         | -             | Flip                  | -             | Inset          |     |
| `Ctrl` +  `B`         | Bevel         | Bevel (bridgeborders) | -             | Extrude        |     |
|                       |               |                       |               | Bridge         |     |


```
JESZCZE DORZYUCIC IKONKI OD 
PRImitives 
MODIFIRES
- bend taper 
- path def ![[sweep.svg]]
pedzle 

remeshe 

splines curves 
```



Fuse / delete (disappear)/ remove

Delete  
Backspace
Delete
Delete and retain poly


![[polydraw.svg]]
```

## PolyDraw

#### `Shift`+`1` Build

points:    
`[LMB]` - create / selsct  
`Shift`+`[LMB]` select  
`Ctrl` - angels  
`Alt` - wiewport  

`F` FILL  
`Shift`+`K`/`K` -  dziwnby bridge / BRIDGE  
`Shift`+`del` - remove unused points  

`Shift`+`C` - Circle  
`Shift`+`S` - Straighten  
`Shift`+`E` - Evenly space    

prims:  
`Shift`+`C` - Circle  
`Shift`+`X` - Collapse

#### `Shift`+`2` Slice  
#### `Shift`+`3` Split   
#### `Shift`+`4` Brush
#### `Shift`+`5` Smooth  

```




# Radial
All Adam settings in one 
![](/src/hou/cfg/wheel1.png)

Better options: 
- make one ring for create geo 
- one for snap 
- one for change viewport + selection 
- uv 
- edit 
- 
----

# Network View Graph




### Navigation

| | |
|-|-|
|`U` | Up  
|`I` | Dive  
|`Shift` + `/` | Find node by path   
|`Ctrl` + `F` | Find node by name   
|`PageUp` or `PageDown` | move through nodes `Shift`    
|` ' ` | last view  
|`F` or `G` | zoom selected   
|`H` | zoom all

### Node customize

|     |                 |
| --- | --------------- |
| `Z` | NODE shape      |
| `X` | NODE visualizer |
| `C` | NODE color      |

### Layaut


|                             |                                                                          |
| --------------------------- | ------------------------------------------------------------------------ |
| `L`                         | layaut                                                                   |
| `Shift`+`L`                 | layout Selected                                                          |
| `Shift` + `A` + `🡰` `🡲`   | (on selected nodes) - align horizontaly                                  |
| `Shift` + `A` +`🡱` `🡳`    | (on selected nodes) - align verticaly                                    |
| `Shift` + `S`               | Change link type                                                         |
| `Ctrl`+`Shift`+`Alt`+ `LMB` | on a node will duplicate the node and automatically reference everything |



To set/change key klick on shelf or menu item while holding `Ctrl` + `Alt` + `Shift`


----

# Parameter Fields

|                         |                         |
| ----------------------- | ----------------------- |
| `Alt` + `LLM`           | create key              |
|                         |                         |
| `Ctrl` + `LLM`          | delete key              |
| `Ctrl`+ `Shift` + `LLM` | delete key whertever is |
| `Ctrl` + `MMB`          | zero                    |
|                         |                         |
|`Shift` + `LLM` | OPEN CURVE EDITR   


| .                                           | .                                                  | .                                                                                              |
| ------------------------------------------- | -------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| <img src="/src/hou/parm_0.png" width="76">  | Default value                                      | `Ctrl` + `MMB` - reverte to default                                                            |
| <img src="/src/hou/parm_1.png" width="76">  | Modified value                                     | `Shift` + `RMB` - switch to previous value                                                     |
| <img src="/src/hou/parm_14.png" width="76"> | Parameter being manipulated in wievport            |                                                                                                |
| <img src="/src/hou/parm_4.png" width="76">  | Value changed waiting for kayframe                 |                                                                                                |
| <img src="/src/hou/parm_2.png" width="76">  | **Keyframe** / **fn** on current frame             | `Alt` + `LMB` - add / `Ctrl` + `LMB` - remove key /  `Ctrl` + `Shift` + `LMB` - remove channel |
| <img src="/src/hou/parm_3.png" width="76">  | **Keyframe** / **fn** on other frame               |                                                                                                |
| <img src="/src/hou/parm_6.png" width="76">  | **Channel reference** on current frame             |                                                                                                |
| <img src="/src/hou/parm_7.png" width="76">  | **Channel reference** on other frame               |                                                                                                |
| <img src="/src/hou/parm_5.png" width="76">  | **CHOP**                                           |                                                                                                |
| <img src="/src/hou/parm_11.png" width="76"> | Non default language **fn**                        |                                                                                                |
| <img src="/src/hou/parm_12.png" width="76"> | Non default language **fn with channel reference** |                                                                                                |
| <img src="/src/hou/parm_8.png" width="76">  | Locked                                             |                                                                                                |
| <img src="/src/hou/parm_9.png" width="76">  | **Take** - not changed                             |                                                                                                |
| <img src="/src/hou/parm_10.png" width="76"> | **Take** - not changed                             |                                                                                                |
| <img src="/src/hou/parm_13.png" width="76"> | Evaluated string (MMB on string param)             | `Ctrl` or `Alt` + `E` - edit expression                                                        |
| <img src="/src/hou/parm_15.png" width="76"> | Bound to viewport handler                          |                                                                                                |
| <img src="/src/hou/parm_16.png" width="76"> | Error                                              |                                                                                                |
| <img src="/src/hou/parm_18.png" width="76"> | Error                                              | wrong language used                                                                            |
| <img src="/src/hou/parm_17.png" width="76"> | After deleted all keys ?                           |                                                                                                |



--------------------------------------------

[Desktop](/src/configs/Hou/desktop/AB.desk)  
[Radial Menu](/src/configs/Hou/radialmenu/ABModeling.radialmenu)  
[qLibDarkFlatTheme](/src/configs/Hou/config/qLibDarkFlatTheme.hcs)  


--------------------------------------------



# TOPs
Generate nodes  
`Shift` + `G` - revert cooked to graph and cook uncooked    // do it before delete from disc  
`Shift` + `V` - Dirty node and cook all  




--------------------------------------------



---
# Tools

C:\Program Files\Side Effects Software\Houdini 18.0.432\bin\Gplay - przegladarka 3d  
