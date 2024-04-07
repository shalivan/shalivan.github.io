---
title: Insta Mat
categories:
  - DTA
tags:
  - NodesGraph
  - 3D
  - Software
description: .
permalink: /instamat/
---
> Pxlink: [TUT](/tutmain/) [Material data](/matdata/)   
> Obsidian: [[TUT]] [[16-02-01-Rendering]]  [[08-01-01-Material]] [[18-01-01-Color]]  [[14-01-01-Procedural]]  [[11-01-01-Math]]


# New project 
- **Layering** - paint on mesh with fx 
- **Mat Layering**  - artist friendly blend materials from finish ones 2d
- **Materialize** - Create from photo 
- **Element Graph** - 
- **nPass Graph** - loop (like scatter)
- **Atom** - create nodes with other nodes 
- **fn graph** - smaller than atom


# Mat Layering



# Element Graph
can browse materials 
quick search witth nodes

#### Nodes

- Material Blend 


#### Export 

- **Output** - per channel for export
- **Material Make** - export set    > `RMB` > `Export Output parameters`  
Output category is important - if Material you can use in other graphs (spawn as node)


# Atom Graphs 

Expose param as graph input - user can adjust 
Expose param as local variable - inside atom 

### Control Flow Graph - loop/branch atoms 



# nPass Element Graphs 
Loop function on GPU 

Buffer saves the lasts iterations output and passes it over to the next pass 


2 fn: 
- `On Execute Assignment` 
- `Did Execute Assignment`  - loop after execution 
input parameters are public. 
npass variables have logo 