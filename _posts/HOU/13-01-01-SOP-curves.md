---
title: SOP

categories:
 - HOU
tags:
- Houdini
- SOP

description: Curves
permalink: /sopcurves/
---


To preserve curve direction u must preserve vertex order.


# SOP
cut on point
- `Convert Line`  |   redraw primitive (destructive for gr &atrr)  
- `Carve` | (will disconect points ! )
- `Poly Path` |   redraw primitive (destructive for gr &atrr)
- `Resample` | Redistribute point and attribs alobg the spine (blend attribs)
- `Poly Cut` | can cuts only on points (detroy point grups )
- `Fuse` |

inject edge where is no point  
- `Boolean`
- `Poly Split`
- `Clip`
- `Knife`
- `Intersection analysis`
- `Incrementersection stitch`

labs tool
-  `Poly Slice` make points on curve or prim > slice / preserve edge group & curve dir. snap.   
  Based on:
   - poly split  
   - boolean (faster)
- `Merge Splines` - with specific conditioons.
- `direction ???`
- `Poly Wire UV` !!!! - <<<

# NURBS & B splines

[Be More Moog: Tool Design That Empowers Users | Richard C Thomas | Games Workshop](https://youtu.be/6BAtzdMGnwA)    
[Advanced Road Generation | Erwin Heyms | Games Workshop](https://youtu.be/G5Iq-jxgZn0)  
