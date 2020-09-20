---
title: Vex Orient
description: VEX Transform, orientation and rotation.
categories:
 - VEX
tags:
- VEX
- Code
---


<!-- more -->



##  Nomenclature
`revolution` rev 0-1 - 1 full circle = 1 rev = 1 turn = 1 rot = 360°   
`degrees` 0-360°  - measure angles by how far we tilted our heads- observer viewpoint   
`radians` 2πr ~6.283.. - measure angles by distance traveled - movers viewpoint   
`euler angle` direction 3Vector     
`dihedral angle` - is the upward angle from horizontal of the wings or tail plane of a fixed-wing air craft.  

`matrix3 m = ident();` - no rotation form of @orient    matrix 3 is rot matrix, matrix 4 is full transform.  


## Transform hierarchy
Order of rotation determine output:  
Use one transform at a time by priority:     
- `v@pivot` exists, use it as the local transformation of the copy/inst. If not:     
- `4@transform` attribute exists: Use it as **Transformmatrix**, overriding everything except P/pivot/trans    
- `p@orient` Use it to orient  **(Copy to point SOP)**  result of your rotation matrix as a **quaternion**  
- `v@N` + `v@up` as the +Z axis and up as +Y axis.     
- `v@v` Velocity of the copy (motion blur, and used as +Z axis of the copy if no orient or N)      
- `p@rot` (quaternion) - Additional Q rotation, (applied after the orientation attributes above)      
- `f@pscale` - Uniform (multiplied by @scale if it exists).      
- `v@scale`  Non-uniform `scale(3@transform, vector(@pscale));` (transform:1!)       
- `v@trans` exists, use it and P to move the copy/instance.  - Translation of the copy, in addition to P     
- `v@P` - Translation of the copy - Instance Position      




---



# Rotations
(Houdini operate in radians)   

Rot types:  
- Matrices (v3= rot, v4= full transform)
- Vector (N and up, Euler)
- Quaternions (V4)   


`f@angleInDeg = degrees(@angleInRad)` - Convert 0-1 > 0-360 radians to degrees       
`f@angleInRad = radians(@angleInDeg) ` - Convert 0-360 > 0-1 degree to radians  
`v@eulerAngle = set(@angleInRad,0,0)` - Direction by vector      
`p@quat = eulertoquaternion(@eulerAngle, 0)` - Convert Euler to Quat  
`3@rot_m = qconvert(@quat)` - Rotate `matrix3` by Quat   
`4@m = set(@rot_m)` - Convert to full transform `matrix`   
`v@P *= m` - Apply rotation matrix  
`p@orient = quaternion(maketransform(@N,@up));` - make orient from N & up    
`p@orient = quaternion(f@angle,v@axies);` - Angle and Vector to Quat    

`slerp()` - easy blend 2 quats    
`cracktransform()` -  returns value of rotation scale or translate from a matrix  

### Copy To Points  (oreint Quaternion)

- Objects going into a copy SOP must be oriented to +Z. (Z-axis points towards N)    
- @orient - copy sop (or other things that are instance attribute rotation operate on matrices where orient is a quaternion   
- use quaternions for orientation. Note how the copies are much more stable.  

#### Rotate Individual Points (@orient)
```cpp
vector axis = @N;  
v@up = chv("up_vector"); // create a 3x3 orientation matrix using N and up as  
float eulerAngle = radians(ch("angle")); // or instead of angle: rand(@ptnum)*360  

matrix3 m = maketransform(@N, v@up); // instead of ident()  means our starting matrix is already pointing dir  
rotate(m, eulerAngle, axis);  
p@orient = quaternion(m); // make the quaternion  
```


#### Rotate Matrix about axis
(Run over points)
```cpp
vector axis = normalize(chv("axies")); //  Axies to rotate
float eulerAngle = radians(chf('rotateAmount')*360); // 0-1 amount *360 degree to radians
matrix3 m = ident();  // empty transform matrix

rotate(m, eulerAngle, axis);  // rotate matrix
@P *= m;  

// rotate back matrix
@P*=invert(m);
matrix translate_matrix = ident();
translate(translate_matrix, set(0,chf("transY"),0));
translate_matrix*=m;
@P*=translate_matrix;
```

##### Roatate Matrix Normal Along Tangent
(Run over points)
OpInput0: polyframe with `tangent`   
```cpp
float eulerAngle = radians(ch("angle"));
matrix rot = ident();

rotate(rot, eulerAngle, @tangent); // matrix to rotate, angle, vector to rotate about
@N= @N*rot;
```

#### Rotate Quaternion in local space
(Run over points)
```cpp
vector eulerAngle = radians(chv("rot"));  // angle  in degrees  converted to radians

vector4 quat = eulertoquaternion(eulerAngle, 0);
matrix3 m3 = qconvert(quat);
matrix m = set(m3);
@P *= m;
```
if xform is present set attrib before @P:

```cpp
if (hasdetailattrib(0, "xform")){
   matrix inputXform = detail(0,"xform");
   @P*=invert(inputXform);
   m*=inputXform;
   }
setdetailattrib(0,"xform",m); // store xform in detail
```

Store xform in Attribute to return it to the original position

```cpp
4@xform_matrix = xform;
@P *= invert(4@xform_matrix);
```


#### Packed Geometry  Rotate
(Run over Prims)  
OpInput0:  packed geo
```cpp
matrix3 x = primintrinsic(0, "transform", @primnum); // matrix3 x = ident();
vector axis = normalize(chv("axis"));
float euler_angle = radians(chf("angle"));

rotate(x, euler_angle, axis);
setprimintrinsic(0, "transform", @primnum, x, "set");
```



#### Orient piece of geometry by 4 points: {@vux}  
- src_pt - source point 1
- dst_pt - destination point 1
- src_opt - source point 2
- dst_opt - destination point 2

```cpp
int src_pt = 10 ;
int dst_pt = 2 ;
int src_opt = 11 ;
int dst_opt = 3 ;
vector4 q = dihedral( point(geoself(), “P”, src_pt)-point(geoself(), “P”, src_opt),
                     point(geoself(), “P”, dst_pt)-point(geoself(), “P”, dst_opt) );
@P = qrotate(q, @P)+point(geoself(), “P”, dst_pt)-qrotate(q, point(geoself(), “P”, src_pt));
```


perfect loop: `sin(2*PI*(@Time*frequency + offset))`


https://www.toadstorm.com/blog/?p=493    
http://www.tokeru.com/cgwiki/?title=Copy,_Stamps,_Rotation,_Hscript,_Vex,_a_ramble  
http://www.tokeru.com/cgwiki/index.php?title=JoyOfVex17#Combine_orients_with_qmultiply
http://yoong-cut-and.blogspot.com/2014/12/orienting-objects-to-curve-basic-of.html  
https://vimeo.com/307156961

---

# Angle
`f@angle =          degrees(acos(dot(normalize(a),normalize(b))));` - Angle Between Vectors   

---

# Look at

lookat()  
```cpp
vector current_axis = {0,0,0};
vector up_axis      = {0,1,0};
vector lookat_axis  = point(1, "P", 0);

matrix3 m = lookat(current_axis, lookat_axis, up_axis);
@P *= -m;
```
dihedral()  
```cpp
vector target = chv("target");
vector4 q = dihedral({0,1,0}, target);
@P = qrotate(q,@P);
```
---

# Direction
### Directional Bias
2D  
`u@P += sample_circle_uniform(rand(@ptnum));` -  pos in circle     
`u@P += sample_circle_edge_uniform(rand(@ptnum));` - pos in circumference    
`u@P += sample_circle_slice(chu("direction"),chf("cone"),rand(@ptnum));` -  pos in circle sector    
`u@P += sample_circle_arc(chu("direction"),chf("cone"),rand(@ptnum));` -  pos in circumference arc    
3D   
`v@P += sample_direction_uniform(rand(@ptnum));` -  pos in sphere surface (Uniform Distribution)        
`v@P += sample_sphere_uniform(rand(@ptnum));` -  pos in sphere volume (Normalized)     
`v@P += sample_direction_cone(chv("angle"),ch("cone"),rand(@ptnum));` - pos in spherical sector. (Control Range)          
`v@P += sample_sphere_cone(chv("angle"),ch("cone"),rand(@ptnum));` -   pos in spherical cap. (Control Range Normalized)        
4D  
`p@p = sample_hypersphere_uniform()` - pos in hypersphere surface  
`p@p = sample_orientatnion_uniform()` - pos in hypersphere volume (Normalized)    
`p@p = sample_orientation_cone()` -  pos in hypersphere sector. (Control Range)    
`@orient = sample_orientation_cone(quaternion(maketransform(@N,@up)),ch("cone"),rand(@ptnum));`     
`p@p = sample_hypersphere_cone()` -  pos in hypersphere sector. (Control Range Normalized)     

`v@v = sample_hemisphere({0,0,1},@bias,u);` -     

https://vimeo.com/226167508


---

#### Wave on plane (Points)
```cpp
float range = chf('Range');
float angle = chf('Angle');
float bias = chf('Bias');

matrix m = ident();
vector axis = {0, 0, 1};

vector pos = @P;
pos.z *= bias;
float amount = exp(length(pos) / range * -1 );
amount = radians(amount * angle);

rotate(m, amount, axis);
@P *= m;
```
