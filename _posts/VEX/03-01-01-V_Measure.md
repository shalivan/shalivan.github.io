---
title: VEX  Measurement
description: Measure, Point clouds
categories:
 - VEX
tags:
- VEX
- Code
permalink: /pc/
---


# Measure

`if (primvertexcount(0, @primnum) > 4)` -  test by by n-gons   **Find N-gones** /// UZUPEŁNIC   






## Distance
[`distance()`](https://www.sidefx.com/docs/houdini/vex/functions/distance.html) - Distence between 2 points  
[`surfacedist()`](https://www.sidefx.com/docs/houdini/vex/functions/surfacedist.html) -  Distance of a point to a group of points along the surface of a geometry   

[Distance From Geometry SOP](https://www.sidefx.com/docs/houdini/nodes/sop/distancefromgeometry.html)


`@dist = distance({0,0,0},@P);` -   
`@mask = 1-clamp(pow(distance(@P*{1,0,1},{0,0,0}),ch("pow"))*ch("multi"),0,1);` -   

**Spherical Mask between points**  
```cpp
vector p1 = point(1,'P',0);
vector p2 = point(1,'P',1);

float r = distance(p1,p2);
@Cd = (r-distance(@P, p1))/r;
```
**Linear Gradient**  
```cpp
vector p1, p2, v1, v2;
p1 = point(1,'P',0);
p2 = point(1,'P',1);

v1 = @P-p1; // treat p1 as origin;
v2 = normalize(p2-p1);

float r = distance(p1,p2);
@Cd = dot(v1,v2)/r;
```



## XYZ Dist
[Hou doc xyzdist()](https://www.sidefx.com/docs/houdini/vex/functions/xyzdist.html)    
[Hou doc PrimUV](https://www.sidefx.com/docs/houdini/vex/functions/primuv.html) - need to know the nearest @primnum and uv   
`primuv()` - interpolated value of an attribute over the parametric surface of the primitive
`primuv(2, "P", posprim, primuv)`



**Fix points on a moving object**  
Input0: the scattered points in a static   position (init frame)  
Input1:  geometry at rest position  
Input2:- moving object  

```cpp
int posprim;
vector primuv;
float maxdist = 10;
float dist = xyzdist(1, @P, posprim, primuv, maxdist);
vector pos = primuv(2, "P", posprim, primuv);
@P = pos;
```




## Nearpoint(s)
Use spatial proximity (closest point in a geometry)
`nearpoint()` -   
[`nearpoints()`](https://www.sidefx.com/docs/houdini/vex/functions/nearpoints.html) -   


`i@nearpt = nearpoints(0, @P, 1e34, 2)[1:][0];` - All the closest point in a geometry (not self)    

int pts[] = {1,2,3,4};




## Neighbour(s)
Return connected points (that share an edge with a given point)  
`Group Expand SOP` - Attribute is spread to its connected neighbors    

[`neighbour()`](https://www.sidefx.com/docs/houdini/vex/functions/neighbours.html) -      
`neighbours()` -   
`polyneighbours()` - same for shared edge in prims  

Return @ptnum or array of @ptnums of the next point connected to a given point  

` .... neighbour()` -    
`i[]@pts = neighbours(0, @ptnum);` - Array of Connected Points @ptnum's        

### Neighbourcount
[`neighbourcount()`](https://www.sidefx.com/docs/houdini/vex/functions/neighbourcount.html) - How Many points connected

`i@count = neighbourcount(0,@ptnum);` - How Many Edges from point     
`if (neighbourcount(0,@ptnum)<3) removepoint(0, @ptnum);` - Delete inline points with only 2 edges      




### ptlined
Distance to line   (defined by 2 points)   

`f@dist_to_line =   ptlined({0,0,0}, {0,1,0}, @P);`



## MinPos
[`minpos()`](https://www.sidefx.com/docs/houdini/vex/functions/minpos.html) -    stuff to “stick” stuff to an object.
Closest position on the surface of a geometry     
position of the closest point on the target geo  


**Closest point on geo to line** (RunOver:Prims)  
Input0: point or spline  
Input1: geometry or spline to find closest point  
```cpp
int pts[] = primpoints(0,@primnum);
int count = len(pts);
float mindist = 999999;
vector currminpos = {0,0,0};

for(int i=0;i<count;i++){
    vector minpos = minpos(1,point(0,"P",pts[i]));
    float dist = distance(minpos,point(0,"P",pts[i]));
    if(dist < mindist){
        mindist = dist;
        currminpos = minpos;
    }
}

addpoint(0, currminpos);
setpointgroup(0, "closest", count, 1, "set" );

```



###  Find Shortest Path
[Find Shortest Path](https://www.sidefx.com/docs/houdini/nodes/sop/findshortestpath.html)


## Bounding Box

`v@Cd = relbbox(0, @P);` - relative position of point in relation to bbox.  
`v@bbox_size = getbbox_size(0);` - Bound size     
`v@centroid =  getbbox_center(0);` - Relative Bbox       
`v@bbox_min = getbbox_min(0);` - get world min of geometry bounds    
`v@bbox_max = getbbox_max(0);` - get world max of geometry bounds    
`getbbox(0,vector min,vector max);` - get both min and max   

```cpp
vector min, max;
getbbox(0,min, max);
vector center = (min+max)/2;
```

[voxelpixel.xyz blog: dist and neighbors](https://voxelpixel.xyz/2020/05/27/houdini-vex-distance-and-neighbours/)   

---


# Point Clouds

!video[](Sources/h/2020-02-15_05-31-45.mp4)

> Point Clouds architecture in VEX is based on data structure called kd-trees. They are created in memory from Houdini geometry and kept in cache for a period of VEX execution. Handle is like a reference of this structure inside a single VEX instance . If you create two point clouds, they will probably have handles 0 and 1 pc functions require that handle to find the point cloud to both read and write in to the separate memory. It's basically an integer which lets you tell to other pc* functions which point cloud you're interested in (among many possibly created)


`pcopen()` - the points are ordered from closest to farthest. (Returns a handle to a point cloud file)      
`pcclose(handle)` Na koniec zamykamy uchwyt, aby uzyskać dostęp do bazy danych punktu      
`pcfilter()` - Filters points found by pcopen using a simple reconstruction filter      
[`pcfind`](https://www.sidefx.com/docs/houdini/vex/functions/pcfind.html) - [] List of closest points (nearpoints) `pcfind(1,'P',@P,ch('d'),25);`   
`pcfind_radius(1,"P","pscale", 1.0, @P, maxdist, maxpts);` - [] List of closest points taking into account their radius      
`pcfarthest()` Returns the distance to the farthest point found in the search performed by pcopen.   


**Nearest point distance**
```cpp
int handle = pcopen(0,"P",v@P, 111,2);
float dist = pcimportbyidxf(handle,'point.distance',1);
@dist_neartst = dist;
@pscale =  dist;
```


**Blur Attributes**
```cpp
int pc = pcopen(0, "P", @P, ch("rad"), chi("num"));
v@Cd = pcfilter( pc, "Cd");
```
**Points Density**
```cpp
int handle = pcopen(0, "P", @P, ch("rad"), chi("num"));
int count = pcnumfound(handle);
f@density = float(count)/float(chi("num"));
```

**Points Density**
```cpp
int pc[] = pcfind(0,'P',@P,ch('maxdist'),ch('maxpt'));
@Cd = float(len(pc))/ch('maxpt');
```

**Transfer Attributes**
```cpp
int handle = pcopen(1,"P", @P, ch("rad"), chi("num"));
@`chs("attribute")` =  pcfilter(handle,chs("attribute"));
```
**Iterate**
```cpp
int handle = pcopen(0,"P", @P, ch('rad'), 2);
vector close_pt;
while(pciterate(handle)){
    pcimport(handle, "P", close_pt);
    @N = close_pt - @P;
}
```

---

**Remove overlaped prims**

```cpp
int prim_points[] = primpoints( geoself(), @primnum );
vector pos_accum = 0;

for ( int i = 0; i < len(prim_points); i++ )
{
    pos_accum += attrib( 0, "point", "P", prim_points[i] );
}

pos_accum /= len(prim_points);

int xyz_prim;
vector xyz_uv;

float xyz_dist = xyzdist( 0, pos_accum, xyz_prim, xyz_uv);

if ( xyz_prim > @primnum && xyz_dist < 0.001 )
    removeprim(0, @primnum, 1);
else if ( xyz_prim < @primnum && xyz_dist < 0.001 )
    removeprim(0, xyz_prim, 1);
```



delete points

if(@myAttribute > 0)
removeprim(geoself(), @primnum, 1); // if you want to delete points owned by primitive itself
or

if(@myAttribute > 0)
removeprim(geoself(), @primnum, 0);
