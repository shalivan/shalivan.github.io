


# UE

Gi
ddgi -dynamic direct gi -  proby

https://www.youtube.com/watch?v=ZefvmV1pdP8&t=121s




-----------------



# rendering
aproximation on physic lighting


## realtime on line



### Ray trace
- trace from camera
- if hit surface shoot ray to lightsource and evaluate shadow and reflections  and refractions
- indirect illumination (hard cost) we have to trace multiple rays depend of type of mat. Those patrhs not depend on eachother so we can calculate it independly (gpu).
- light decay :(shoot trace from geo to light) and
   - tradfitional: shoot ray to light
   - path trace: (full indir illum) multiple rays and recursyvly calculate for each additional hits .

#### Ray trace > Path trace

recently with RTX in realtime



### Rendering
*Defered* - more lights is ok    
*Forward Rendering* - bneter with translucency   



# Material (ray tr ?)

###
`Conductors` - (tyupicly reflect depend on wave leng. give color)  
`Dielectrics` - (refl + refract + scatter refracted (subsurf but rather difuse ))   
Refl + refr >> have fresnel.

http://filmicworlds.com/blog/everything-has-fresnel/


### Rendering
`BRDF` - bidirectional reflection distribution fn
hemisphere for mat / and directional spike for reflectivces. More blury reflection more direction samples > longer rendering
`BTDF` - transmision (reflectiw + (refracted + iro)) (so dielectric render slower )
`BSSRDF` -sub-scarttering surface
`BSDF` - bidiirectional scatering




### Rasterisation
3d viewport


### Camera simulation


### Light
`CRI` color rendering index  
if iluminated point id to 5x dist from light we can aprox as point light
directional aprox to (rownolegle)
dome light - `hdri light`





Each thread is not just blind but also memoryless.
Shader Language has a single main function that returns a color at the end.

### VS Vertex shader    
### PS Pixel shader (old fragment)    

grid of pixels that work paralel
### Compute shader   
in paralel on gpu
subdivisions workgroups and in each group divisions


### Mesh shader    
Mesh Shaders    
- for new tessalation


### Task shader
 call based of cam frustrum   
