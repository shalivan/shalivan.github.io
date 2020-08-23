
# Rendering

#### PBR      
>path tracer

realistic light with multip dif bounces. (use rayytrace) and phis light   
GI - diffuse limits  
(path traceing happening outside surface shader )  

#### MICRO POLIGON  

(divide to micro polis in buckets) (same as pbr but mp)  
Rendering DICEING: shader quality 1 >> 5  

#### RAY TRACRING:

>ray tracer

reflection & refraction. (cleaner resoult because not diceing) its going pixel by pixelon image.
(path traceing happening inside surface shader)

## Render Settings:
setting | lo | med | hi | production
--- | --- | --- | --- | ---
pixel sample | 4x4 | - | 7x7 | 10x10 (fur or huge motion)
Min/Max ray samples | - | 1/9 | - | 2/9
Noise Levels | - | 0.1 | - | 0.08
Sample Lock | - | ON | - | OFF
Stochastic sample (AA volume quality) | 1 | - | - | 4

**[light]** light: sample quality on lights more than 1 (on direct samples) now direct light is clean.

#### Indirect illumination:
[mantra] rendering > limits:  2 3 2 0 1
[mantra] rendering > sampling, Qualities. diffiuse, reflection  quality (1-4)
Reflect/Refract/Diffuse lim 4/4/1  
Color Space Gamma 2.2
Color Limit 4

#### PHOTON MAP
generaiotn (Final gather) for final gather

# Shadeing  


`material bnuilder`  - colapse selected to material > (like subnets)
 `layer mix` you can mix shader by layers outputs

Core versions are without texture and displacement inputs.
#### Classic shader
oldschool mantra  
More settings  
Workglow in metalic: color reflections and black diffuse (all in texture)  

#### Principle shader
Less parameters and ranged 0-1  
Workflow normal albedo and metallic channel like pbr     
IOR use with `nasted dielectrics` model. model 2 side surface and liquid should be inside betwreen then set priorities to surfaces [mantra] rendering >  shadeing:  ENABLE ABSORBTIONA AND NESTED DIELECTRICS ~!!!! turn on !

#### Volume shader


#### Pyro shader
`pyro shader` shader use 2 field: smoke field: density /// color form temperature // intensity from heat ///  
only flame simple    
```for shader flame simple change to density evetywhere```  
fog simple  
```for fog same setup but fire intendity to 0 and increse smoke desn and attenuation color to get shift // (fit range in smoke field)
smokefield shape > tagget range max 6
color maping na ramp```  


https://youtu.be/h5azbcLaMzY

www.sidefx.com/tutorials/mantra-pbr-sampling-render-settings-path-tracer-houdini-16-1/
