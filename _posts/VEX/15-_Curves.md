

####  Gradient along curve
(Run over points)
```cpp
float ValueAlongSpline = @ptnum/(@numpt-1.0);
```
#### Gradient along curve (ramp)
(Run over points)
```cpp
float gradient = @ptnum/(@numpt-1.0); //numpt is int .0 < will convert it   
@Cd.y = chramp('colorRamp', gradient);  
```

### Connect Adjacent Points
(Run over points)
```cpp
float   radius_max = chf("radius");
int     points_max = chi("connections");

int     points[] = nearpoints( 0, @P, radius_max, points_max );

int     prim;
string  name;

for ( int i = 0; i < len(points); i++ )
{
    if ( points[i] <= @ptnum )
        continue;         

    name = attrib( 0, "point", "name", points[i] );

    if ( name == s@name )
        continue;         

    prim = addprim( geoself(), "polyline" );            

    addvertex( geoself(), prim, @ptnum );
    addvertex( geoself(), prim, points[i] );

    @Cd = {1, 0, 0};
}
```

### Make Curve from points
(Run over detail)
OpInput0: points   
```cpp
int num = chi("num");

// get points and write position to array
int points[] = expandpointgroup(@OpInput1, "!");
vector pos_array[];
foreach(int i; int point; points)
{
    pos_array[i] = point(@OpInput1, "P", point);
    removepoint(geoself(), point);
}

// calculate position at t for berzier curve with degree len(pos_array) - 1
vector bezier_pos(const vector pos_array[]; const float t)
{
    int n = len(pos_array);
    vector p_array[] = pos_array;
    vector pos;
    while(n--)
    {
        for(int i = 0; i < n; i++)
            p_array[i] = p_array[i] * (1.0 - t) + p_array[i + 1] * t;
    }
    return p_array[0];
}

// create curve
float step_size = 1.0 / (num - 1);
for(int i = 0; i < num; i++)
{
    vector pos = bezier_pos(pos_array, step_size * i);
    points[i] = addpoint(geoself(), pos);     
}
addprim(geoself(), "polyline", points);
```



### Connect 2 curves
(Run over detail)
OpInput0: Merge 2 curves   
```cpp
float weight= ch("weight");
int num = chi("num");

// get endpoints and tangents
vector pos1 = point(@OpInput1, "P", 1);
vector pos4 = point(@OpInput1, "P", 3);
vector vec1 = normalize(point(@OpInput1, "P", 1) - point(@OpInput1, "P", 0)) * weight;
vector vec4 = normalize(point(@OpInput1, "P", 3) - point(@OpInput1, "P", 2)) * weight;
vector pos2 = pos1 + vec1 * (1.0 / 3);
vector pos3 = pos4 + vec4 * (1.0 / 3);

// create cubic bezier curve
float step = 1.0 / (num - 1);
int curve = addprim(geoself(), "polyline");
for(int i = 0; i < num; i++)
{
    float val = step * i;
    vector p =  pos1 +
                (3 * pos2 - 3 * pos1) * val +
                (3 * pos1 - 6 * pos2 + 3 * pos3) * pow(val, 2) +
                (-pos1 + 3 * pos2 - 3 * pos3 + pos4) * pow(val, 3);
    int point = addpoint(geoself(), p);
    addvertex(geoself(), curve, point);
}
```
## Polyframe and direction  
## Geometry From Spline

### Polywire shape with ramp for combined curves  
OpInput0: combined curves   
```cpp
// Create Primitive Wrangle before polywire, use @width as Wire Radius
// Get array of points in each curve (primitive)
i[]@primPts = primpoints(0, @primnum);
// For each point in current curve
foreach (int i; int currentPoint; @primPts){
    float ramp_index = fit(i, 0, len(@primPts)-1, 0,1);
    f@widthPrim = chramp("shape", ramp_index)/20;
    setpointattrib(0, "width", currentPoint, @widthPrim, "set");
    }
 ```

### PolyWire pscale SOP  
(Run Over Prims)
OpInput0: resample  
Output: polywire   
```cpp
i[]@primPts = primpoints(0, @primnum);
foreach (int i; int currentPoint; @primPts){
    float ramp_index = fit(i, 0, len(@primPts)-1, 0,1);
    f@widthPrim = chramp("shape", ramp_index)/20;
    setpointattrib(0, "width", currentPoint, @widthPrim, "set");
    }
```

### Carve Curve
```cpp
float max = chf("max"); // like carve u parm
float min = chf("min"); // like carve v parm
vector uv;     
int primnum = @primnum;
float d = xyzdist(0, @P, primnum, uv);
@P = primuv(0, "P", primnum, set(fit01(uv.x,min,max), 0.0, 0.0));
```

```cpp
float animDur       = f@perimeter * 400.0;

float n             = fit( noise( v@P * 22.0 ), 0.2, 0.8, 0.0, 1.0 );
float offset        = fit01( lerp( n, rand( @primnum ), 0.35 ), 0.0, 15.0 );
float animPer       = fit( @Time - offset, 0.0, animDur, 0.0, 1.0 );

int primPts[]       = primpoints( 0, @primnum );
foreach( int pt; primPts )
{
    float u         = point( 0, "curveu", pt );
    if( u > animPer ){
        removepoint( 0, pt );
    }
}

if( animPer > 0.0 ){
    vector pos      = primuv( 0, "P", @primnum, set( animPer, 0.0, 0.0 ) );
    int newPt       = addpoint( 0, pos );
    addvertex( 0, @primnum, newPt );
}
```

// Scale 10 times first and last points

```cpp
if ((@ptnum == 0) || (@ptnum == (@numpt-1))) f@pscale = 10;
else f@pscale = 1;
// Scale 10 times first and last points, short form    
f@pscale = (@ptnum == 0) || @ptnum ==(@numpt-1) ? 10 : 1;
```

 convert | arg;
--- | ---
"poly" |  Closed polygon. Can use 0 or more points.
"polyline"  |  Open polygon. Can use 0 or more points.      
"tet" | Tetrahedron primitive. Requires exactly 4 points. You cannot add vertices to this primitive.
"sphere", "circle", "tube", "metaball", "metasquad" |   Require exactly 1 point. You cannot add vertices to these primitives.
"AlembicRef", "PackedDisk" | Packed Alembic or packed disk primitive. Require exactly 1 point. You cannot add vertices to these primitives.

### Concave points
(Run Over Prims)
```cpp
int points[] = primpoints(0, @primnum);
int num = len(points);
vector up = prim_normal(0, @primnum, 0.5, 0.5);

foreach(int i; int point; points) {
    vector pos      = point(0, "P", point);
    vector prev_pos = point(0, "P", points[i - 1]);
    vector next_pos = point(0, "P", points[(i + 1) % num]);

    vector edge_prev = normalize(pos - prev_pos);
    vector edge_next = normalize(next_pos - pos);

    float dist = dot(lerp(next_pos, pos, 0.5) - prev_pos, normalize(cross(edge_next, up)));
    if(dist > 0)
        setpointattrib(geoself(), "concave", point, 1, "set");
}
```
### Measure
```cpp
vector2 uv4 = set(f@curveu, 0);
uv4 = primuvconvert("op:../curve1", uv4, 0, chi("mode"));
f@curveu = uv4.x;
```

 convert | arg; | value
--- | --- | ---
real > unit |          0  |  0.11..   
real > unitlen |       1  |  0.9..
real > len |          2 |  15..
unit > real  |         3  |  9
unit > unitlen  |      4  | 0-1
unit > len    |        5  | dl! // 33
unitlen > real  |      6  |  9
unitlen > unit  |       7  | 0-1
unitlen > len  |       8  | dl! // 33
len > real   |        9  |  0.06
len > unit    |        10  |  0.07
len > unitlen |      11  |  0.033

#### Boolean Curve:
https://www.toadstorm.com/blog/?p=529  

### Snap Curve to terrain (heightfields / volumes)
points
in: curve
in2: terrain
```cpp
vector samplepos = set(@P.x, 0, @P.z);
int primid = nametoprim(1,"height");

float height = volumesample(1,primid,samplepos);
@P.y= height;
```

### Get height(y)-Slope
```cpp
vector flatnrm = @N;
flatnrm.y  = 0;
flatnrm = normalize(flatnrm);

f@slope = degrees(acos(dot(@N,flatnrm)));
```
