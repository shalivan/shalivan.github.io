---
title: VEX Orient
description: Transform, Orientation, Rotation.
categories:
 - VEX
tags:
- VEX
- Code
permalink: /orient/
---


[Coords](/coords/)   


https://qiita.com/kit2cuz/items/55be3f432783fc979b16
<!-- more -->

https://vfxbrain.wordpress.com/2018/12/04/using-orient-attribute-with-instances/

##  Nomenclature
**Houdini operate in radians**    

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


Rotation types:  
- Matrices (`3@` = rot, `4@` = full transform)
- Vector (`v@N` and `v@up`, `v@EulerAngle`)
- Quaternions (`p@`)   


`@Degrees = degrees(@Radians)` - 0-1 to: 0-360 (radians to degrees) `f@`       
`@Radians = radians(@Degrees) ` - 0-360 to: 0-1 (degree to radians) `f@`     
`@Angle = set(@Radians,0,0)` - Euler angle (direction by vector `v@`)      
`@orient = eulertoquaternion(@EulerAngle, 0)` - (euler to quat)  
`@RotMartix = qconvert(@oreint)` - (rotation matrix3 by quat)   
`@m = set(@RotMatrix)` - (convert to full transform `matrix` )  `4@`     
`@P *= m` - (apply rotation matrix)     

.


`@orient = quaternion(maketransform(@N,@up));` - (make orient from **N** & **up** )      
`@orient = quaternion(f@angle, normalize(v@axies));` - ( make orient from **Angle** and **Vector** )     
`@orient = quaternion(normalize(axis)*@AmountOfTot);` - scale axis vec to get amount    
`@orient = quaternion(m);` - by matrix (matrix3 m = ident();)    
`@orient = slerp(a, b, ch('blend') );` - blend oreints   
`@orient = qmultiply(@orient, extrarot);` -

`cracktransform()` -  returns value of rotation scale or translate from a matrix  

### Copy To Points  
- Z-axis points towards N (Objects must be oriented to +Z)
- @orient (Quaternion)   


## Orient

**Rotate Individual Points**
```cpp
vector axis = @N;  
float angle = radians(ch("angle"));  
vector up = chv('up');

matrix3 m = maketransform(@N, v@up);
rotate(m, angle, axis);  
@orient = quaternion(m);
```

```cpp
// create an axis and an up vector.
// The axis will represent the Z direction of the final matrix
vector axis = {0,0,1};
vector up   = normalize(@P);

// build a vector for each axis, then build a matrix out of it.
// I may be normalizing a bit much here, but it cant hurt.
vector zaxis = axis;
vector xaxis = normalize(cross(up, axis));
vector yaxis = normalize(cross(axis, xaxis));
matrix3 default = set(xaxis, yaxis, zaxis);

// create the orient quaternion as a point attribute
p@orient = quaternion(default);
```

## matrix3

**Rotate Matrix about axis**
```cpp
vector axis = normalize(chv("axies"));
float angle = radians(chf('rotateAmount')*360); /// euler angle
matrix3 m = ident();  

rotate(m, angle, axis);  // rotate matrix
@P *= m;  

// rotate back matrix
@P*=invert(m);
matrix translate_matrix = ident();
translate(translate_matrix, set(0,chf("transY"),0));
translate_matrix*=m;
@P*=translate_matrix;
```


https://forum.patagames.com/posts/t501-What-Is-Transformation-Matrix-and-How-to-Use-It


**Roatate Matrix Normal Along Tangent**
(Run over points)
OpInput0: polyframe with `tangent`   
```cpp
float angle = radians(ch("angle"));
matrix rot = ident();

rotate(rot, angle, @tangent); // matrix to rotate, angle, vector to rotate about
@N= @N*rot;
```

**Rotate Quaternion in local space**
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

## Packed geometry
**Packed Geometry  Rotate**
(Run over Prims)  
OpInput0:  packed geo
```cpp
matrix3 x = primintrinsic(0, "transform", @primnum); // matrix3 x = ident();
vector axis = normalize(chv("axis"));
float euler_angle = radians(chf("angle"));

rotate(x, euler_angle, axis);
setprimintrinsic(0, "transform", @primnum, x, "set");
```

**Get Orient from packed**

```
matrix m = primintrinsic(0, "packedfulltransform", @primnum);
matrix3 m3 = matrix3(m);
p@orient = quaternion(m3);

```
**Get Pivot from packed**
```
vector3 pivot = primintrinsic(0, "pivot", @primnum);
v@pivot = pivot;

```

**Packed Geometry from RDB to copy to object**
https://youtu.be/W9ggbLr6wNY?t=1001
To transform to replace low proxy in RDB.
Copy intrinsic transforms to points:
```cpp
matrix m4 = primintrinsic(0,'packedfullytransform', @ptnum);
matrix3 m3 = matrix3(m4);
@orient = quaternion(m3);
@scale = cracktransform(0,0,2,0,m4);
v@pivot = primintrinsic(0,'pivot',@ptnum);


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


### Direction to surface (double cross)
https://voxelpixel.xyz/2020/06/05/vectors-double-cross-product/  
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