---
title: Niagara Modules
description: Modules
categories:
 - PXL
tags:
- Unreal
- VFX
- Rendering
- Real Time
- HLSL
- Game Dev
- Niagara
permalink: /fluidninjalive/
---


`NinjaLive` (Red icon)  BP - Actor object
 - `NinjaLive Component` - more parameters (sim pressets / materials)
`NinjaLiveUtilities` (Green icon) - can add to actor
`NinjaLivePressetManager` (Black icon) -


setup:
1. project settings: new trace channel set to ignore withname: `FluidTrace`. Must be nr 1
2. Set up UV for hit collision
3. enable apex destruction

if we have a trace channel:
delete it
add fluid trace
and readd old trace channel
