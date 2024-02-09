---
title: Substance Designer
description: Material authoring
categories:
  - PXL
tags:
  - Tech
  - Art
  - Materials
  - Shaders
  - CG
  - NodesGraph
permalink: /substancedesigner/
aliases:
  - substancedesigner
---
[[16-02-01-Rendering|rendering]]
[[08-01-01-Material|matdata]] / [Material data](/matdata/)

Dartk circle on node input mean this input is primary.

# Bit depth

L8 - 8 bit  > grayscale (256 colors) > base color default color, albedo, ambient occlusion  
L16 - 16 bit/channel (65000 colors/channle) >   normal export
L16F - 16 bit/channel > but floating point for heightmaps
L32 -  32 bit/channel > (ta sama co 16 tylko powyzej i poniżej 0 mozna matme)   , {not better but additional functionality} (assumed to be raw (linear space) by most rendering soft)


# Mixing
Mixing colors:

Inconsistant amount of value
- multiple - will darken image (not linear)
- screen - will brighten image (non linear)
- overlay - screen&multiple (non linear)
- Add/Sub - (linear !)
- max min - blending h maps - linear
- soft light - use with color blending

Inne:
- random to ABSOLUTE - nba kazdym nodzie nie bedzie niespodianek
- WEIGHTED AVARAGE = tak average of each input and divide by nr of input ... we should weigh of intensity of each input ()


# Nodes plugins

`BW Color variation`  
- value variation - jakie valu ma variacja  
- hue variation - base on original ccolor how much to offset original color
smaple count - 2 colors variation - more ++

# Nodes

`make tile photo` -  
`pixel processor`  !   


### Base:
`Blend` - basic node  
`Transform 2d` - limited to ^2  
`Height Blend` -  with height mask output !!!!  

### Channels:
`Gradient` - Gray to color   
`Curve` -  
`Split RGBA` / `Merge` - floats > vector > float   

### Filter
- `Histogram scan` - Select
- `Quantize`- Steps
- `Highpass` - (leave only detail)
- `Curve` - Broad range
- `Edge detect`
### Blurs
- `Blur hq`
- `Non uniform blur Grayscale` - just blur  with angle and tex amp
### Warp / Organic
- `Warp` - Move direction of gradient. From black to white.
- `Directional Warp`  -  In one direction  in: mask how much will transfrer in const direction (use when need to break noise for tiles, bend shapes)
- `Vector Warp` -   
- `Multi dir warp grayscale` - w kilku kierunkach sterowanie  tylko amp
  - wrapy zostawiaja za soba  trailsy
- `Non- uniform dir wrap` - adv mozna sterować kątem maską
- `Vector wrap` - flow
- `Slope Blur` / `Slope Blur Grayscale` - ('input', 'gradient with blur dir') like warp slide in direction of gradient descent.  Chained warps
  - min: cutoff
  - max: add
- Shadow ?
### Tilers:
- `Tile Sampler` - new  - more control - use with texture noise mask
- `Tile Generator` -    - less control    
- `Splatter` -  simpler in use than  Tile Generator
- `Tile Random` - random constraint to keep random on string.    

Flood fill system:
- `Fill flood`   
- `Flood Fill to grayscale` - Input noise to select random islands.    
-

Shape Splatter system:
- `Shape Mapper` /
- `Shape Splatter`   - system of advanced scattering . Is using bcg heigth.

### Noise
- `Voronoii`
- `Voronoii fractal` - 3d more detiaal vars
- trailangle grid

- `perlin noise zoom` -   
- `fract sum base` - dots   

### Scan processing


### Splines
Non destructive shape creation, scatter elements on.
Plieline steps: 1)Creation, 2) Assembly, 3) Modify , 4) Render

**Creation**
spline circle cubic and poly quadratic
- `Mask to path` > `path to spline` > `scatter on spline`
- `Spline Bridge` - skin

**Assembly**
You can 'chain' splines nodes one after another or use nodes:
- `Append` (group)
- `Connect`
- `Merge`
- `Select`

**Modify**
- Warp,
**Render**
You need to render spline to convert
- `Spline Render`

...

- `preview paths`
- `path select`


## Python
https://support.allegorithmic.com/documentation/sat/pysbs-python-api/getting-started

-----


https://sighack.com/post/getting-creative-with-perlin-noise-fields
https://flafla2.github.io/2014/08/09/perlinnoise.html

![GitHub Logo](/Sources/noise/SubstanceNoises.png)




https://youtu.be/WNwtc-OeGQ0  
https://youtu.be/YmTN8K5-7Oc  

https://youtu.be/YmTN8K5-7Oc
https://youtu.be/NzSkMVYzP18
