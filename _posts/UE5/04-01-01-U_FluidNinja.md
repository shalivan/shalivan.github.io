---
title: Niagara
description: Paradigm
categories:
  - PXL
tags:
  - Unreal
  - VFX
  - Rendering
  - HLSL
  - Niagara
  - RealTime
  - GameDev
  - Node
permalink: /niagara/
aliases:
  - niagara
---
> Obsidian: [[16-01-01-VFX|VFX]] [[04-01-01-U_Niagara|Niagara]]

# Fluid Ninja Live 
Input  
- Field (distance field, static mesh only, landscape, splines),  - object interacting with surface / base collision for sim (landscape) - only with world facing setpus 
- Points (bones, particles, chaos chunk)  
Sim
- motion trajectory painter > 2d Ninja fluid sim
Output 
- Render Targets External Materials


Ninja Live Core is wrap with helpers for **Ninja Live Component** 

##### Transform rules
Rotation: Ninja ignore rots as intended `IgnoreSystemRotation = TRUE`
Scale: Do not scale actor.  Use parameters 
- LiveActivation / ActivationVolumeSize 
- LiveInteraction / InteractionVolumeSize
- LiveCore / ExtentsXYZ


## Modes

Modes:  
- **Simple paint** - No sim (simple), 
- **Fluid sim** - Advect density (complex)
Space: 
- **Cam facing**, 
- **World facing** 
Influence: 
- **Standalone** - internal renderers (simple),  
- **Drive other systems** - use external (complex)
Water: 
- **Sparse** (n < 1) density fades. -  rivers, lakes, FX = visual detail only but more detailed due to additional dense channel usage. 
- **Dense** (n > 1) density accumulates - creeks, terrain water = real water behavior that fills valleys



## Buffer 

Typically ninja handle Buffers internally with linked materials

| Buffers                      |      |                                                     |                                                                                              |
| ---------------------------- | ---- | --------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| **PaintBuffer**              | RGBA | Paint Velocity (RG) + Density (B) + HeightField (A) | accelerate particles             <br>bend foliage                         <br>drive flowmaps |
| **VelocityDensityBuffer**    | RGBA | Sim Velocity (RG) + Density (B) + WetMap (A)        | heightmap for Volumes        <br>alpha mask for translucency                                 |
| **PressureDivergenceBuffer** | RG   | Sim Pressure (R) + Divergence (G)                   | height-displacement              <br>refraction                                              |

We can write buffers directly to RT: 
- `LiveOutputRenderTargets`

A material is provided with the buffers if: 
- contains Texture Objects using the above naming convention and
- the material is added to a ninja "OutputMaterials" array

Niagara for Sampling, using User.Parameters:
 - NinjaPaintBuffer
 - NinjaVelocityDensityBuffer
 - NinjaPressureDivergenceBuffer

More: NinjaLiveComponent Blueprint / MODULE023



# Ninja Live Component 


##### LiveCore
Main controls
Pressets / Resolution 
SimplePainter / CameraFacing
Sim Speed 
- Performance
- Debug
- ZLock <<
- WorldSpaceOffset
- DrawLinesBetweenPoints

##### LiveEditorTools
"Editor Mode ON".


##### LiveInputFields
- Bitmaps
	/VelocityDensityFieldFromTexture
	/VelocityFieldFromTexture
- MeshFields
 /LandscapeFields
	/FluidStabilityOnLandscape
	/ExternalHeightData
- SplineFields
 /Destructibles
 /Cache

##### LiveInputPoints
 /BrushKillers
 /BrushNoise
 /BrushVelocity
 /InteractionWithOwner
 /InteractionWithDestructibles
 /InteractionWithParticles

##### LiveSimulation
 /Bounds
 /Noise
 /Pressure

##### LiveOutputRenderTargets ----------
 /PaintVelocityDensityAndElevation
 /SimVelocityDensityAndWetmap
 /SimPressureDivergence
 /LegacyExporter

##### LiveOutputNiagaraNative-----------
 /Mesh
 /Volumetric
 /Particles

##### LiveOutputMaterials --------------

##### LiveOutputParams------------------

##### LiveLegacy -----------------------
 /Unused
 /RayMarching
 



#  NinjaDrivingExternalSystemsUtility




#  NinjaLandscapeUtility


-----

# External displays / Direct Drivers



#### External driving

Instead of rendering inside Niagara:

- write buffers → RenderTargets
- feed materials externally
- apply to:
    - landscapes
    - meshes
    - Niagara systems




# Water

Requires:

EnableHeightField = TRUE

Effects:

- fluid follows terrain
- velocity follows slope
- mesh deforms to surface

##  Surface aligment 

##  Sparse 
### Splines (rivers)


- provide **directional flow**
- NOT terrain-aware by default
- used for:
    - rivers
    - controlled flow paths

EnableSplineReader = TRUE


NinjaLiveComponent /LiveInputFields /SplineFields /EnableSplineReader = TRUE
NinjaLiveComponent /LiveInputFields /SplineFields /GetSplineComponentsFromTaggedActors



## Dense




