---
title: Substance Designer
description: Material authoring
categories:
- PXL
tags:
- Tech Art
- Materials
- Shaders
- CG
permalink: /substancedesigner/
---

[Material data](/matdata/)

# Bit depth 

L8 - grayscale (256)
L16 - default color (65000)
L16F - 16 but floating point for heightmaps
L32 - (ta sama co 16 tylko powyzej i poniżej 0 mozna matme)   , {not better but additional functionality}

L32 we can use 
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
- `Histogram` select
- `Quantize`- steps
- `Highpass` to remove gruba daty
- `Curve` - broad range
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
- `non- uniform dir wrap` - adv mozna sterować kątem maską
- `vector wrap` - flow
- `Slope Blur` -   
- `Slope Blur Grayscale` - ('input', 'gradient with blur dir') like warp slide in direction of gradient descent.  Chained warps
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




-----



https://youtu.be/WNwtc-OeGQ0  
https://youtu.be/YmTN8K5-7Oc  

https://youtu.be/YmTN8K5-7Oc
https://youtu.be/NzSkMVYzP18