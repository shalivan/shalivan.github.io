---
title: Algebra
description: coordinates
categories:
- RT
tags:
- Math
---



# Coordinate Systems


#### Cartesian coordinates
x, y
Rene Descartes


TILES:
- trix
- squares
- hex 


#### Polar Coordinates
2d. where x, y >> angle, radius  

Polar (r,θ) to Cartesian (x,y):
```
x = r × cos( θ )
y = r × sin( θ )
```

Cartesian (x,y) to Polar(r,θ):
```
r = √ ( x2 + y2 )
θ = tan-1 ( y / x )
```

#### Barycentric coordinates
is specified as the center of mass, or barycenter,




#### Spherical coordinates
- parallels will converge (nachodzić na siebie)
- even if not changing direction you will get accumulated rotation

#### Euclidean
geomery  
- in Euclidian parallel will stay parallels


#### Hyperbolic coordinates
(2d plane circle)
- parallels will diverge (Opposite to spherical)
- even if not changing direction you will get accumulated rotation




https://youtu.be/FBn6VgoF3fE - patterns  



#### Mesh Uv's







### Euclidean space
log to cartesian (input grid)
```
float r     = pow( $E, @P.x );
@P.x       = r * cos( @P.z );
@P.z       = r * sin( @P.z );
```

cartesian to log
```
float p     = log( sqrt( pow(@P.x, 2.0) + pow(@P.z, 2.0) ) );
float f     = atan2( @P.z, @P.x );
@P.x       = p;
@P.z       = f;
```

#### Projective general linear group (PGL)


##### Möbius transformation
```
vector2 mobiusInverse(vector2 o; float r; vector p){
	float a = r*r/(pow(p.x = o.x),2) + pow(p.y - o.y),2);
    return set(a*(p.x - o.x) + o.x, a*(p.y-o.y)+o.y);
}
```

youtube.com/watch?v=0z1fIsUNhO4
http://virtualmathmuseum.org/ConformalMaps/inv/index.html

### Hyperbolic Geometry
>(Bolyai–Lobachevskian or Lobachevskian geometry) is a non-Euclidean geometry. The parallel postulate of Euclidean geometry is replaced with:For any given line R and point P not on R, in the plane containing both line R and point P there are at least two distinct lines through P that do not intersect R.

### Spherical

https://youtu.be/yY9GAyJtuJ0



line is drawn as arc  

tiling p

youtu.be/6z3rQb3fUMw



### Manifold - Curved spaces
manifold is a topological space, such that each point has a neighborhood that is homeomorphic to an open subset of a Euclidean space.

### Barycentric Coordinates
Find coords within triangle by jackie rice. "this also extends to tets as well, but it'd be a 4x4 matrix instead of a 3x3"   if everything is actually aligned to the z-1 axis, so if z is set to 1, then you can invert the solution as well to convert back to cartesian coordinates  

```cpp
//pts is the three points in your triangle
matrix3 gen_bary_mat(vector pts[]){
    matrix3 m = set(
                pts[0].x, pts[0].y, 1,
                pts[1].x, pts[1].y, 1,
                pts[2].x, pts[2].y, 1);
    return m;
}
vector tri_pts[] = array({10, 4, 1}, {3,2,1}, {0, 10, 1});
vector test_pt = {6, 5, 1};
matrix3 bary_matrix = gen_bary_mat(tri_pts);
vector bary_pt = test_pt * invert(bary_matrix);  //solution by inversion, this is big brain
printf("bary coords: %g \n", bary_pt);
```

projection with dihedral so u don't have to worry about any kind of scaling being applied to the triangle, like so:
```cpp
//this would gooooooooooooo in a prim wrangle, and then ud call the resulting trs matrix
//in a point wrangle to apply the positional changes
matrix3 m = dihedral(v@N, set(0,0,1));
matrix trs = m;
matrix mov_to_orig = ident();
matrix mov_z = ident();

translate(mov_to_orig, v@P);
translate(mov_z, set(0,0,1));

trs = invert(mov_to_orig) * m * mov_z;
```


###  4D






### OpenSubdiv rays projection
Evaluates an attribute at the subdivision limit surface using Open Subdiv.
Project high to low:
first input: hi res geo to deform,   
second input low res mesh (to project to subdiv pos)
(run on points)
```cpp
int primNum;
vector UV;

float dist = xyzdist( 1, @P, primNum, UV);

vector restN = primuv(1,"N",primNum,UV);
vector posOnRest = primuv(1,"P",primNum,UV);

//subdiv
float pU, pV;
int pId;
int patch = osd_lookuppatch( 1, primNum, UV.x, UV.y, pId, pU, pV);

//these two functions return the last argument
//so posOnRest is being overwritten in the function, much like xyzdist()
int sDN = osd_limitsurface( 1, 'N', pId, pU, pV, restN);
int sDP = osd_limitsurface( 1, 'P', pId, pU, pV, posOnRest);

@P = posOnRest;
```
#### Move out SDF collision

// OpInput1  SDF volume representing the collision geo
```
vector dir = volumegradient( 1, 0, @P);
vector dist = abs(volumesample( 1, 0, @P));
v@P += dir * dist;
```
