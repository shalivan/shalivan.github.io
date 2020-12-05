---
title: CHOP

categories:
 - HOU
tags:
- Houdini

description: chops basics.
permalink: /chops/
---

Motion fx viewer - will show channels


## Import CHOP data
To importm data from chops  



### SOP node
`channel` node - (like material)  

![](/src/hou/chop/chop_channel.png)  


### SOP function

`chop("../chopnet1/null/chan1")` - Sops expression to import CHOPnet channel     
`chopcf("", 0, $F, )` - Sop expression with channel by number and time  

![](/src/hou/chop/chop_exp_fn.png)  

![](/src/hou/chop/chop_exp_fn2.png)  

### CHOP Export
orange flag: `export chop node` to export    
Activate will override SOP channel

![](/src/hou/chop/chop_exp.png)  

![](/src/hou/chop/chop_exp2.png)  




### Op: expresion  

nodes may have a parameter which expects a file name of a file containing a specific type of data. In these types of parameters you can usually use op:/path/to/node instead of a file name to grab data from live nodes in the scene hierarchy instead of from a file.

 ```op:/geo1/volume1``` - instead of a file name to grab data from live nodes using full path  
```op:`opfullpath('../../volume1')` ``` -  work around this by converting a relative path to an absolute path using the opfullpath






---

# Nodes
#### base
`Wave`, `Noise`


#### post
`limit` - clamp  
`envelope` - smooth  



---


# Vex

 import vis
 ```
 float t, s;
 string path;

 t = @Time * 44100; // 44khz, the sample rate of the audio
 path = chs('path');

 s = chop(path, 'chan0', t);

 @P.y += s * ch('amp');
 ```

quantise a value to steps, with variable smoothness:
by matte:
```
float smoothstep(float n; float x) {
    if (n == 0) return x;
    return 1.0/(1.0+pow(1.0/x-1.0,n) );
}

vector smoothstep(float n; vector x) {
    if (n == 0) return x;
    vector un = {1,1,1};
    return un/(un+pow(un/x-un,n) );
}

// step: levels of quantisation
// val: value to quantise
// rolloff: smoothness

val *= step;
vector fraction = smoothstep(rolloff, frac(val));
val = floor(val) + fraction;
val /= step;
```
