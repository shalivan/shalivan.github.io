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
> Pxlink: [TUT](/tutmain/) , [[DTA]]
>Obsidian: [[DTA]] , [[12-01-01-USD | USD]] ,[[20-01-01-Res | Res]] ,[[21-01-01-Pipes | Pipes]]

https://www.sidefx.com/docs/houdini/basics/hotkeys.html
https://miro.com/app/board/uXjVP06Hcz4=/ - skróty od ziomka
--------------


Modeling procedural vs Modeling destructive
objects in one geo node

![[Pasted image 20240716030315.png]]

 Hotkey Manager > Houdini  > Panes > Geometry Viewers



# GLOBAL
|       |                |
| ----- | -------------- |
| Shift | Selection      |
| Alt   | Modeling tools |
| Ctrl  | -              |

|                                          | Default        |                                           | NEW                            |
| ---------------------------------------- | -------------- | ----------------------------------------- | ------------------------------ |
| ![](/src/hou_icons/select_component.svg) | `S`            | SELECT                                    |                                |
| ![](/src/hou_icons/move.svg)             | `W`, `E`, `R`  | TRANSFORM                                 |                                |
| ![](/src/hou_icons/handles.svg)          | `Enter`        | INVOKE SOP                                | powinno byc tez pod  ``` ` ``` |
| ![](/src/hou_icons/view.svg)             | `Space`        | CAMERA                                    |                                |
|                                          | `X` , `C` ,`V` | Rings                                     | dodać `Z` ale jeszcze zajęte   |
|                                          | `Q`            | repeat tool                               | `Q`                            |
|                                          | `P`            | Params                                    | `P`                            |
|                                          | `D`            | Viewport Options                          | `O`                            |
|                                          |                | Edit / Draw/ Quick Shapes - node specific |                                |

---

# CAMERA
Use only with `Space` to free mode combos. View options & Editor UI shorts

|                                                             | Default                  |               | NEW                     |
| ----------------------------------------------------------- | ------------------------ | ------------- | ----------------------- |
|                                                             |                          | Pad           |                         |
|                                                             |                          | Pad           | `A` `D` `W` `S` `Q` `E` |
| ![](/src/hou_icons/tilt.svg) ![](/src/hou_icons/tumble.svg) | `Alt` / `Space`  + `LMB` | Rot           | `Space`  + `LMB`        |
| ![](/src/hou_icons/track.svg)                               | `Alt` / `Space`  + `MMB` | Move          | `Space`  + `MMB`        |
| ![](/src/hou_icons/dolly.svg)  ![](/src/hou_icons/zoom.svg) | `Alt` / `Space`  + `RMB` | Zoom          | `Space`  + `RMB`        |
|                                                             |                          | Pers          | `Space`  1              |
|                                                             |                          | Top           | `Space`  2              |
|                                                             |                          | Front         | `Space`  3              |
|                                                             |                          | Side          | `Space`  4              |
|                                                             |                          | Orto          | `Space`                 |
|                                                             |                          | Focus frame   | `Space`  F              |
|                                                             |                          | Focus home    | `Space` G               |
|                                                             |                          | Focus c-plane | `Space`  H              |

---

# SELECT
Press `S` to enter mode

|                                               | Default                                |                                              | NEW                                |
| --------------------------------------------- | -------------------------------------- | -------------------------------------------- | ---------------------------------- |
|                                               | `1`                                    | Multi select                                 |                                    |
| ![](/src/hou_icons/select_points.svg)         | `2`                                    | Points                                       | `1`                                |
| ![](/src/hou_icons/select_edges.svg)          | `3`                                    | Edges                                        | `2`                                |
| ![](/src/hou_icons/select_faces.svg)          | `4`                                    | Polys                                        | `3`                                |
| ![](/src/hou_icons/select_points.svg)         | `Shift` + `2`                          | Convert selection to Points                  | `Shift` + `1`                      |
| ![](/src/hou_icons/select_edges.svg)          | `Shift` + `3`                          | Convert selection to Edges                   | `Shift` + `2`                      |
| ![](/src/hou_icons/select_faces.svg)          | `Shift` + `4`                          | Convert selection to Polys                   | `Shift` + `3`                      |
|                                               |                                        |                                              |                                    |
|                                               | SELECTION TOOLS                        |                                              |                                    |
| ![](/src/hou_icons/select_mode_laser.svg)     | `F5`                                   | laser                                        | `F1`                               |
| ![](/src/hou_icons/select_mode_boxselect.svg) | `F2`                                   | box                                          | `F2`                               |
| ![](/src/hou_icons/select_mode_lasso.svg)     | `F3`                                   | lasso                                        | `F3`                               |
| ![](/src/hou_icons/select_mode_brush.svg)     | `F4`                                   | paint<br>                                    | `F4`                               |
|                                               |                                        |                                              |                                    |
|                                               | SELECTION MODES                        |                                              |                                    |
| ![](/src/hou_icons/select_visible.svg)        | `Shift`+`V`                            | backmasking                                  | `Shift`+`B`                        |
| ![](/src/hou_icons/select_contained.svg)      | `Shift`+`C`                            | contained                                    | `Shift`+`C`                        |
| ![](/src/hou_icons/select_by_normal.svg)      | -                                      | by normal                                    | `Shift`+`N`                        |
| ![](/src/hou_icons/show_group_colors.svg)     | `9`                                    | select by group (groups color)               | `Shift` +  `5`                     |
|                                               | -                                      | Toggle select types                          | `Shift` +  `6`                     |
|                                               | -                                      | Connected 3d                                 | `Shift` +  `7`                     |
|                                               | -                                      | Uv                                           | `Shift` +  `8`                     |
|                                               | -                                      | Name                                         | `Shift` +  `9`                     |
|                                               |                                        |                                              |                                    |
|                                               | SELECTION  MODIFY                      |                                              |                                    |
|                                               | `LMB` x 2                              | Semi loop                                    | `LMB` x 2                          |
|                                               | `MMB` x 2                              | Semi loop                                    | `MMB` x 2                          |
|                                               | `Shift`+`A`                            | Semi loop                                    | `Shift`+`Z`                        |
|                                               | `Shift`+`G`                            | Growth selection                             | `Shift`+`G`                        |
|                                               | `Shift`+`S`                            | Shrink selection                             | `Shift`+`F`                        |
|                                               | `Shift`+`B`                            | Selection bounds                             | `Shift`+`Y`                        |
|                                               | `Shift`+`I`                            | Invert                                       | `Shift`+`I`                        |
|                                               | `Shift`+`Ctrl`+`E` (on edges)          | Selection bounds edge                        | `Shift`+`U`                        |
|                                               |                                        |                                              |                                    |
|                                               | `Shift` + `P`                          | Set sellection pattern                       | `Shift` +  `T`                     |
|                                               | `Shift` + `🡰` `🡲` `🡱` `🡳`          | Growth pattern                               | `Shift` + `A` `D` `W` `S`          |
|                                               | `Shift` + `Ctrl` + `🡰` `🡲` `🡱` `🡳` | Growt pattern till the end                   | `Shift` + `Ctrl` + `A` `D` `W` `S` |
|                                               | `K`                                    | Growth till paint under mouse                | ?                                  |
|                                               |                                        |                                              |                                    |
|                                               |                                        | Revert                                       | `Shift` +  `R`                     |
|                                               | `Shift` +  `F`                         | Fill to all contained in type                | ?                                  |
|                                               | `Shift`  + `D`                         | Normal / Fill selections to borders of group | ?                                  |
|                                               | `Shift`+`N`                            | select none                                  | -                                  |
|                                               | `N`                                    | select all                                   | -                                  |

---

# TRANSFORM

|                                | Default |                   | NEW |
| ------------------------------ | ------- | ----------------- | --- |
| ![](/src/hou_icons/move.svg)   | `T`     | Transform         | `W` |
| ![](/src/hou_icons/rotate.svg) | `R`     | Rotate            | `E` |
| ![](/src/hou_icons/scale.svg)  | `E`     | Scale             | `R` |
|                                | `Y`     | Cycle             | `T` |
|                                | `M`     | World Coordinates | `A` |
|                                | `MMB`   | move selection    |     |

https://youtu.be/Zh6Q6r9LQlA

### Pivot / Handle

For animation. Permanent pivot of object.

| Default              |                                                                                                      | NEW |
| -------------------- | ---------------------------------------------------------------------------------------------------- | --- |
| `'`+`Shift`/`Insert` | **Pivot** - pivot transform change parameter.                                                        |     |
| `'`                  | **Handle** - leave pivot unaffected. Detached Viewport handle temporary. For modeling and placement. |     |

| MENU                                  |                                                |
| ------------------------------------- | ---------------------------------------------- |
| `RMB>presistant`                      | For enable 2nd handles!                        |
| `RMB>SnapTo..`                        | Pivot or centroid.                             |
| `RMB>HandleParameters`                | Options                                        |
| `RMB>Local/Global`                    | Local pivot points vs Global - centroid of all |
| `RMB>TranslateGloballyInLocalControl` | Local transform of last selected               |

### Align  
Align by Orientation picking. Select points/edges, enable tool and hover over geometry to snap or RMB on the handle and choose Align handle ▸ Start orientation picking 3) Hover over geometry .. Y is up. 4) klick
Dependencies
- if you have object or world aligned handles it change behavior

| Default                         |                                               |     |
| ------------------------------- | --------------------------------------------- | --- |
| `:` / `;`                       | Orientation picking toggle                    |     |
| `:` + `Shift` Hold              | Orientation picking (need to hold)            |     |
| `:` + `Shift` + `LMB`           | only Rotate                                   |     |
| `:` + `Shift` + `LMB`  + `Ctrl` | Look at Y  (to change click handle with ctrl) |     |
| `:` + `Ctrl` + `LMB`            | only Move                                     |     |
| `:` + `select axis` + Drag      | secondaty axies direction                     |     |

### Snap

|                                    |     |       | NEW            |
| ---------------------------------- | --- | ----- | -------------- |
| ![](/src/hou_icons/snap_grid.svg)  |     | Grid  | `Shift` + `F1` |
| ![](/src/hou_icons/snap_point.svg) |     | Point | `Shift` + `F2` |
| ![](/src/hou_icons/snap_curve.svg) |     | Prim  | `Shift` + `F3` |
| ![](/src/hou_icons/snap.svg)       |     | Multi | `Shift` + `F4` |

- for edge if you select near center it will snap center to point, if selected near end will snap end point of edge

### Construction plane

|                                                    | DEFAULT   |                                                                                       |     |
| -------------------------------------------------- | --------- | ------------------------------------------------------------------------------------- | --- |
| ![](/src/hou_icons/display_construction_plane.svg) | `/` / `?` | Construction plane                                                                    |     |
|                                                    |           | You can choose pivot handle to choose primary axis for align it will appear as yellow |     |



---


---




---

# RMB Menus

On pivot - Edit manipulator
On empty - Move
With Space/Alt - View


000



## Viewport
| ![](/src/hou_icons/select_visible.svg) | Hide | `H`           | Hide    | X   |
| -------------------------------------- | ---- | ------------- | ------- | --- |
|                                        |      | `Ctrl` + `H`  | Invert  | X   |
|                                        |      | `Shift` + `H` | Unhoide | X   |

|     |                                |                            |
| --- | ------------------------------ | -------------------------- |
|     |                                |                            |
|     | show uv layout !!!!!           |                            |
| `H` | hide `H`+`ctrl`/`shift`   ??   |                            |

| `H`           | Hide    |
| ------------- | ------- |
| `Ctrl` + `H`  | Invert  |
| `Shift` + `H` | Unhoide |


#### Hide


|                                      | Viewport other nodes |     |
| ------------------------------------ | -------------------- | --- |
| ![](/src/hou_icons/show_all.svg)     |                      |     |
| ![](/src/hou_icons/show_ghosted.svg) |                      |     |
|                                      |                      |     |





![[Pasted image 20240724041253.png]]


----

# HANDLE TOOL

## [Edit] ![](/src/hou_icons/edit.svg) SOP


Shift + T - Tweek mode
Shift C make circle

|             |                            |                |
| ----------- | -------------------------- | -------------- |
| `L`         | Slide on Surface           |                |
| `H`         | Peak                       |                |
| `B`         | Sculpt                     |                |
| `Y`         | Edit                       |                |
| `Shift`+`T` | Tweek mode   (no handles ) | ![[tweak.svg]] |

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

## Draw ![](/src/hou_icons/polydraw.svg)


#### `Shift`+`1` Build

points:    
- `LMB` - create / select  
-  `Shift`+`[LMB]` select  
- `Ctrl` - angels  
-  `Alt` - viewport  

- `F` FILL  
- `Shift`+`K`/`K` -  dziwnby bridge / BRIDGE  
- `Shift`+`del` - remove unused points  

- `Shift`+`C` - Circle  
- `Shift`+`S` - Straighten  
- `Shift`+`E` - Evenly space    

prims:  
- `Shift`+`C` - Circle  
- `Shift`+`X` - Collapse

#### `Shift`+`2` Slice  
#### `Shift`+`3` Split   
#### `Shift`+`4` Brush
#### `Shift`+`5` Smooth  

----
![](/src/hou_icons/transform.svg)


## Delete / Blast / Fuse ![](/src/hou_icons/edgecollapse.svg)   ![](/src/hou_icons/fuse.svg) ![](/src/hou_icons/dissolve.svg)  ![](/src/hou_icons/blast.svg)  ![](/src/hou_icons/delete_circle.svg)
edge / points / poly




Weld  ![](/src/hou_icons/pointweld.svg)
 - `A` - collapse to midpoint
 - `B` -restart
 - `G` - cancel

## Bridge ![](/src/hou_icons/bridge.svg)
edges  / NOT WORKING ON POLYS

## Extrude ![](/src/hou_icons/polyextrude.svg)
edge / poly

## Fill ![](/src/hou_icons/polyfill.svg)

edges

## Bevel ![](/src/hou_icons/polybevel.svg)
Operation
- Drag `LMB`
- `Ctrl` + `LMB` - Subtract from selection
- `Shift` + `LMB` - Add to selection
- `Shift` + `A` `LMB` - Add loop to selection
- `Scroll` - change divisions

## Clip ![](/src/hou_icons/clip.svg) / Mirror ![](/src/hou_icons/mirror.svg)
Operation
- `F` + Drag `LMB`  - Draw plane
Displace
- `G` - display wire in
- `H` - diaplay plane

## Split ![](/src/hou_icons/polysplit.svg) / Edge loop

Split loop !
- `Scroll` - split magnet



---

## Path deform  ![](/src/hou_icons/sweep.svg)

Operation
- `B` -  change align
View
- `F` , `G` , `H` - change preview

----

## Curve ![](/src/hou_icons/curve.svg | 70)



# Radial
All Adam settings in one

default circle menu shoudld be on C because it change automaticly for some tools

![[SRC/hou_icons/Untitled.png]]

Better options:
- make one ring for create geo
- one for snap
- one for change viewport + selection
- uv
- edit

****
![[Pasted image 20240716030927.png]]



----

```
#### Managing multiple object
- name prim by class
- rest pos
- pack geo
- what node for material ?


# CUSTOM


`Shift` + `W` - In all windows wireframe mode   
~~`Alt` + `W`~~ - close window  
~~`Ctrl` + `1`,`5`~~ ... - change   

`9` selection group        
`\` - manual update   `|` - auto update      - Stop / Start logic sim!
` ' ` - RESELECT FOR CURENT TOOL     
` ~ ` - SECURE SELECTION  
~~`U`/`I`  ~~<< DELETE - go up in hierarchy

- ? szybki przeskok do porzednich nodów na dodatkowym scrollu ???



#### Model  / move / manipulate

- coordinates
- shading
- snap
- pivot
- construction plane
- align
- repeate  << Q is ok
- hide << na selekcji tylko  i edit modzie

### Rings
- model
- snap
- view
-

### Shortcuts for tools
- extr / extract / dupl / mittot  / disol
- fill bridge bevel  clip mirror
- group  fuse split loop  
- draw edge collapse bool combine  normal  wels smooth
```

# czego brakuje
- MERGE UVS
- ![[Pasted image 20240714231130.png]]

- move with shift should duplicete
- : ![[Pasted image 20240723031033.png]]
-

# Network View Graph
~~`C` is visualize~~ should be: comment

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
In properties

|                         |                         |
| ----------------------- | ----------------------- |
| `Alt` + `LLM`           | Create key              |
| `Ctrl` + `LLM`          | Delete key              |
| `Ctrl`+ `Shift` + `LLM` | Delete key whertever is |
| `Ctrl` + `MMB`          | Zero                    |
| `Shift` + `LLM`         | OPEN CURVE EDITR        |

| .                                   | .                                                  | .                                                                                              |
| ----------------------------------- | -------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| ![ \|100](/src/hou/cfg/parm_0.png)  | Default value                                      | `Ctrl` + `MMB` - reverte to default                                                            |
| ![ \|100](/src/hou/cfg/parm_1.png)  | Modified value                                     | `Shift` + `RMB` - switch to previous value                                                     |
| ![ \|100](/src/hou/cfg/parm_14.png) | Parameter being manipulated in wievport            |                                                                                                |
| ![ \|100](/src/hou/cfg/parm_4.png)  | Value changed waiting for kayframe                 |                                                                                                |
| ![ \|100](/src/hou/cfg/parm_2.png)  | **Keyframe** / **fn** on current frame             | `Alt` + `LMB` - add / `Ctrl` + `LMB` - remove key /  `Ctrl` + `Shift` + `LMB` - remove channel |
| ![ \|100](/src/hou/cfg/parm_3.png)  | **Keyframe** / **fn** on other frame               |                                                                                                |
| ![ \|100](/src/hou/cfg/parm_6.png)  | **Channel reference** on current frame             |                                                                                                |
| ![ \|100](/src/hou/cfg/parm_7.png)  | **Channel reference** on other frame               |                                                                                                |
| ![ \|100](/src/hou/cfg/parm_5.png)  | **CHOP**                                           |                                                                                                |
| ![ \|100](/src/hou/cfg/parm_11.png) | Non default language **fn**                        |                                                                                                |
| ![ \|100](/src/hou/cfg/parm_12.png) | Non default language **fn with channel reference** |                                                                                                |
| ![ \|100](/src/hou/cfg/parm_8.png)  | Locked                                             |                                                                                                |
| ![ \|100](/src/hou/cfg/parm_9.png)  | **Take** - not changed                             |                                                                                                |
| ![ \|100](/src/hou/cfg/parm_10.png) | **Take** - not changed                             |                                                                                                |
| ![ \|100](/src/hou/cfg/parm_13.png) | Evaluated string (MMB on string param)             | `Ctrl` or `Alt` + `E` - edit expression                                                        |
| ![ \|100](/src/hou/cfg/parm_15.png) | Bound to viewport handler                          |                                                                                                |
| ![ \|100](/src/hou/cfg/parm_16.png) | Error                                              |                                                                                                |
| ![ \|100](/src/hou/cfg/parm_18.png) | Error                                              | wrong language used                                                                            |
| ![ \|100](/src/hou/cfg/parm_17.png) | After deleted all keys ?                           |                                                                                                |



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


![[attribdelete.svg]]
![](/src/hou/cfg/wheel1.png)
>  [[TUT]] [[16-02-01-Rendering]]  [[08-01-01-Material]] [[18-01-01-Color]]  [[14-01-01-Procedural]]  [[11-01-01-Math]] [[12-01-01-Gaea]] [[16-02-01-Substance_Designer]] [[17-01-01-Modeling]] [[17-01-01-Modeling_Foliage]]


> [[02-01-01-LSystem]]  [[03-01-01-Karma]] [[04-01-01-Mantra]] [[05-01-01-Heightfields]]  [[06-01-01-CHOP]] [[07-01-01-PDG]]  [[08-01-01-CFX]]  [[10-01-01-LAB]] [[11-01-01-COP]] [[12-01-01-USD]]  [[13-01-01_VOP]] [[13-01-01-SOP]] [[13-01-01-SOP-curves]]

> [[01-01-01-Noise]] [[02-01-01-V_DrawCurves]] [[02-Vex_Volume]] [[03-01-01-V_Measure]] [[13-01-01_VOP]] [[05-01-01-V_Orientation]] [[07-01-01-V_Strings]]  [[08-01-01-V_Expressions]]  [[09-01-01-V_Attribs]] [[10-01-01-V_Syntax]]  [[12-01-01-Python-hou]]

> [[01-01-01-FLIP]] [[01-01-01-PYRO_Dense]] [[01-01-01-RBD_SOP]] [[01-01-01-RBD]] [[01-01-01-Vellum]] [[01-01-01-Vellum_SOP]]


#### Match translate

> is icon on the right of transform params click, and select obj u want rotate to.
