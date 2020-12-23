---
title: L-system
description: Turtle commands for L system
categories:
- HOU
tags:
- Math
- Houdini
- Procedural
- .HIP
- SOP
permalink: /lsystem/
---



[SOP_L.hiplc](/src/hip/SOP_L.hiplc)

# Turtle commands

#### Move and Rot (d0L)

|||
|---|---|
`F`| Move forward a step, drawing a line connecting the previous position to the new position.  
`f`| Move forward without drawing.  
`+` `-` | Rotate right / left 90  degrees.  
`[]` |  Branch


#### Parameters
`F(l,w,s,d)` - `l` - distance / `w` - width / `s` - cross sections divisions (rows) / `d` - divisions (columns)   

#### Direction and branches  (bracketed systems)
`F+(45)F` - change direction   

`F[+F]F[+F][-F] ` - branching  

Rewriting
`A` - Init
`A=F+A`-  Rule
#### 3d

|||
|---|---|
`&`, `^` | pitch up , pitch down  
`\\`, `/`| roll clockwise, counter-clockwise  
`~` | Random   
`"` | Step size scale. command makes the F commands half length in each generation, which makes the branches shrink further out.  
`;` | Angle
`T` | Gravity
`J`,`K`| Leaf

stochastic systems (to add divergence using probabilities;
parametric systems (using conditions

context sensitive systems
two-rule system will take twice as many generations to produce the same result.


COPY TO POINTS : https://youtu.be/4krEG2rK5iA?t=1090

---

# Recursive fractals
recursively replacing an initial state

## Koch snowflake
- Angle = 60   
- Premise `F++F++F`    
- Rule 1 `F = F-F++F-F`  

## Sierpinski triangle
- Angle = 60  
- Premise `F--G--G`  
- Rule 1 `F = F--G++F++G--F`  
- Rule 2 `G = GG`  


https://qiita.com/procedural_design/items/a27b38e862bcfcb2f09e


https://www.sidefx.com/docs/houdini/nodes/sop/lsystem.html  
http://www.motionesque.com/beautyoffractals/  
https://www.toadstorm.com/blog/?p=214  
