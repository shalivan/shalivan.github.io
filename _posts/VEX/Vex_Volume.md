Fog VDB from pomlygons, + color tuple
density (v3) + cd  (v3)


https://vimeo.com/448212258/4611b035be



Color from Volume bounds
```
vector bb = relbbox(0,@P);
@Cd = chramp('colour',bb.z);
```

Blend distance VDBs
```
float other_sdf = volumesample(1,0,v@P);
f@surface = lerp(f@surface, other_sdf, chf("blend"));
```
