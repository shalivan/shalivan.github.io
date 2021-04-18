---
title: Vex Attributes
description: VEX @attributes, Groups, Casts
categories:
 - VEX
tags:
- VEX
- Code
permalink: /attribs/
---
[Vexpressions](/vexpressions/)  





<!-- more -->

# Read Attribute
Create foo attribute with value of:  
`@foo = v@P[0];` - Fetch 'x' position   (Can also use .x, .y, and .z  [0], [1], and [2] index)  
`@foo = v@opinput1_P;` - Fetch attribute from second input  
`@foo = point(1, "Cd", @ptnum);` - Read point attribute from second input  
`@foo = prim(0, "string_attribute_name", @primnum);` - Read primitive attribute from point wrangle     
`@foo = details(0, attribute);` -  Fetch from detail string    
`@foo = detail("../repeat_begin1_metadata1/","iteration", 0);` - Get iteration number      

# Attribute from Group
`i@foo = @group_bar;` - Store group 'bar' in attribute 'foo'  
`i@foo = (@group_bar==1) ? 1:0;` - Using if statement  
`i@foo = inpointgroup(0, "bar", @ptnum);` -  In Point group     
`i@foo = invertexgroup(0, "bar", int vertexnum)  ` - In Vertex group          
`i@foo = inprimgroup(0, string groupname, int primnum) `- In Prim group    

```cpp
if (@group_bar==1)
  @foo=1;
else
  @foo=0;
```
```cpp
int ingroup = inpointgroup(0,"bar",@ptnum);
if (ingroup == 1)
   @foo=1;
else
   @foo=0;
```

```cpp
if(inprimgroup(0,"barA", @id) == 1 && inprimgorup(0,"barB", @id)){
  @foo=1;
 }
 else if(inprimgroup(0,"barA", @id)){
  @foo=0;
 }
```



#  Group by Attribute
`Partition SOP` - Can create groups by rule  
`if (@P.x>0) i@group_bar = 1;` - Add to group by attribute threshold     
`if (match("*box1", s@objname) == 1) @group_bar = 1;` - Add to group if strings match   
`setpointgroup(0, sprintf("points_%g", (@ptnum + int(rand(@ptnum)) % ch("num_groups") ), @ptnum, 1, "set");` -   




# Group Operations

### Create Group by normal

```cpp
vector up = set(0,1,0);
vector N = v@N;
float angle = acos( dot(normalize(up), normalize(N)));
angle = angle/(3.14/180);
if(angle<chf("threshold")){
        @group_bar = 1;
}
```

`expandpointgroup(int opinput, string groupname)`   



# Casting

#### Class
`(float)foo` - Cast to float  
`float(foo)`  - Cast to float  
`vector(foo)` -  `v@foo = dot(v@N,normalize(vector(rand(@ptnum)))) * 0.5 + 0.5;`    

`s@foo =  itoa(i@number)` - Int > String   
`f@foo =  atof(f@number)` - String > Float (0.0 if the string does not contain a number)    
`i@foo =  int(rint(f@float))` - Float > Int        

`hsctorgb()`  
`rgbtohsv()`  
`rgbtoxyz()`  
`zyztorgb()`  

`serialize ()`  
`unserialize()`  

#### Conversion
`Cd = Cd.zzy;` - Swizzle  

---

# Transfer
#### Detail > Points (point wrangle)
Import `detailarray` as a local point array.
(If any array element modulo of 2  is equal to zero,
point with the same number is colored.)
```cpp
int importarray[] = detail(0, 'detailarray');
foreach(int i; importarray)
   {
   if(i%2 == 0)
      {
      setpointattrib(0, 'Cd', i, {1,0,0});
      }
   }
```
#### Points > Detail (detail wrangle)
Iterates over the geometry points, reads their positions  and puts each value into a detail array   
```cpp
v[]@myarray;

for(int i=0; i<@numpt; i++){
   vector item = point(0, 'P', i);
   insert(@myarray, 0, item);
   }
```
```cpp
int npt = npoints(0);
vector importarray[];

resize(importarray, npt);
for(int i = 0; i < npt; i++) {
    importarray[i] = point(0, "P", i);
    }
```
#### (point wrangle)
Export every point to one detail array
```cpp
int point[] = array(@ptnum);
setdetailattrib(0, "points", point, "append");
```




----


# Accumulate

```cpp
f@accusum = 0;

for(int i=0; i<@numpt; i++){
    @accusum = @accusum + point(0, 'mattemp', i);
    @testloopcount += 1;
    }

for(int j=0; j<@numpt; j++){
    setpointattrib(0, 'accu', j, @accusum);
    }
```

Collect in detail attrib:
```cpp
vector p[];
p[0] = v@P;
setdetailattrib(0, "pArray", p, "append");
```

----


# Attributes



#### Material:

`s@shop_materialpath` - Path to a material. You can add this attribute to points using the Material surface node. When you instance an object onto a point with this attribute, the instanced object uses the given material. Not supported in the viewport.  

`s@material_override` A serialized Python dictionary mapping parameter names to values. You can add this attribute to points using the "override" controls on the Material surface node. When you instance an object onto a point with this attribute, the instanced object applies the given overrides to its material.  

#### Time
`$F` - The current frame, (as set with the play bar controls)  
`$FSTART` - start frame, `$FEND` - end frame  
`f@Time` -  Float time `$T` -  Current time, in seconds  
`f@Frame` -  Float frame `$FF`    
`f@SimTime` - Float simulation time `$ST`, only present in DOP contexts.  
`f@SimFrame` -Float simulation frame `$SF`, only present in DOP contexts.  
`f@TimeInc` - Float time step `1/$FPS`    

#### General
`i@ptnum` - Current point number / `i@primnum` /  `i@vtxnum`  
`i@numpt` - Total number of points  / `i@numprim`   / `i@numvtx`    

#### Geometry  
`v@P` - Point/Primitive Position  
`v@N` - Point/Primitive/Vertex Normal - to initialize normals @N = @N  
`v@Cd` - Color   
`v@v` - Velocity (e.g. for motion blur / in particle systems)  
`v@pivot` - Local pivot point for instance  
`f@lod` - Detail/Primitive Level of detail  
`v@rest` - Rest position  
#### Pop  
`v@force` - Force (e.g. acting on particle)  
`f@age` - Particle Age  
`f@life` - Max. Particle Life  

#### Transform
`f@pscale` - Uniform scale. Used in copy-SOP or particle systems  
`v@scale` - Non-Uniform scale. For use see pscale  
`v@up` - Up-Vector. Used together with @N to orient point/particle/instance    
`p@orient` - Quaternion defining the rotation of a point/particle/instance  
`p@rot` - Quaternion defining additional rotation  
`v@trans` - Translation of instance  
`3@transform` - Transformation matrix (used e.g. in Copy-SOP)  

#### Volumes
`f@density` - Density of voxel  
`i@ix, @iy, @iz` - Voxel indices along each axis. Ranging from 0 to resolution-1  
`v@center` - Center of current Volume  
`v@orig` - Bottom left corner of current Volume  
`v@size` - Size of current Volume  
`v@dPdx` - Change in position to get from one voxel to the next in x direction  
`v@dPdy` - Change in position to get from one voxel to the next in y direction  
`v@dPdz` - Change in position to get from one voxel to the next in z direction  
`v@BB` - relative position inside bounding box. Ranging from {0,0,0} to {1,1,1}  

#### Shading
`v@Cd` - Diffuse Color  
`f@Alpha` - Alpha transparency  
`v@uv` - Point/Vertex UV coordinates  
`v@Cs` - Specular Color  
`v@Cr` - Reflective Color  
`v@Ct` - Transmissive Color  
`v@Ce` - Emissive Color  
`f@rough` - Roughness  
`f@fresnel` - Fresnel coefficient  
`f@shadow` - Shadow intensity  
`f@sbias` - Shadow bias  



### Intrinsic
- being an extremely important and basic characteristic of a person or thing.  


[andreasbabo93 Tip&Tricks](https://andreasbabo93.wixsite.com/sbabovfx/useful-vex-and-expressions   )     
[VEX Wrangle Cheat Sheet](http://mrkunz.com/blog/08_22_2018_VEX_Wrangle_Cheat_Sheet.html)     
