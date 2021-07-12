---
title: Modeling

categories:
 - ART
tags:
- Art

description: RAW

permalink: /modeling/
---



### Mesh  
`*.obj` - no vertex color and 2-uvs standardised, no attribs  
`*.fbx` -  
`*.gltf`-    Create an unwanted catalog in UE4, no Vert Color?  
`*.bgeo.sc` - cache  
`*.sim` - more expensive H cache (eg in output node in dop)    



## Props
    - elements should be `grounded` in scene  
    - barnacling small things around,
    - footing - awareness of  intersecting,
    - greebling materialing



# Basics
- General meshes with equal triangles behave better: rendering performance (overdraw) / simulations (`Delanunay` max minimal angle (tend to 60) ! - smoothes interpolation but less approximation of surface when long trix better define edges)
- scale is important
- zastosowanie. games/subdivs.

   as much u can go be procedural to can fix


   Density of details
   3 poziomy density



# Asset workflow:

        Create library:
        - library files
        - asset files




# Common problems
- parts for bake and uvs overlaps
- symerites
/material ID bake
- pivots        
---        
# Hard surface

---


# Fabric
Best simulated

- Tailoring (amount of material)  
- Material properties >  (stretch, bend, weight)    
- Grain of fabric. (weakness of cross cuts)  

- **uv**
- uv for high. bake by uv
- make uvs straight for simulation and texturing (the direction of the fibers)






---


# Vegetation
rośliny - kawałki z których składamy całość i do tego dodajemy na całość atrybuty  
NIE OPISANE: z liści high składamy zbrushowa roslinke

- **ref** and different sizes and shapes  (grass, plants, bush , tree)
  - silhouette
  - characteristic: leaf band, beginning, grouping (higher leafs more vertical change shape) gravitation
  - growth to the sun, moss growth in shadows  because is not"vascular" plants (to not dry out (mostly 'N' in North hemisphere)
- **model low** poly (parts)
  - parts (leafs, stamp)
  - symmetry
  - direct leaf to create planes good for view
- **early uv** unvrap on low
  - 2 sided leaf  for detail u can apply different textures (2 sided nodes) ie U can move uv have (right and left part on uv). (or have 2 geometries)
  - test in engine with distance gradient alpha and check how big cutoff could be to get optimal visible part and leaf area
- **sculpt** think before sculpt if its what u need
  - make thickness and smooth to low poly
  - material id's for parts
  - sculpt
- **refine low** poly
  - minimize places with alfa to not have overdraw
  - triangulation sometimes needs to changed
- **bake**
  - by uv
- **compose** plants: arrange and deform  
  - use **simulation** to refine final shape
- set per object attributes
  - vertex color for movement  (main branch, leafs and thin edges ) / physical properties
  - normal. On bush:  `Custom Vertex normals` - transfer normal from vdb tree form.
- **painting**
  - spots with color variations (some blurry)
  - use also sharp lines
  - paint masks: sss,
  - veins and celular patterns
  - vines to subsurface mask!
- **material**
  - instances 2levels deep to global control
  - bend grass near player
- vertex anim **movement**  - wind and interaction
  - Tree bend, branches, leafs
  - wind for grass and branches pivoted  
  - wygiac przy playerze cardsy troche do kamery  
  - scale anim and size on distance to betere disappear LOD
  - scale grass down on last lod
  - how fast move depend on sale smooth ramp =x*(in+1))/(x-in)  
- engine **optimization**
  - cluster foliage, procedural placement system
  - early z pass   
