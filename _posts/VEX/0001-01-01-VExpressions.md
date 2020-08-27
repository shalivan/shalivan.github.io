---
title: Vexpressions
description: VEX basic expressions, Op()
categories:
 - VEX
tags:
- VEX
- Houdini
---


# Op()

`geoself()`, `0`, `@OpInput1`- Returns a handle to the current geometry  

### OpInputs:
`opname(".")` - node name `$OS`   
`opname("..")` - name of node Container   
`opinput(".", 0)` -  name of the node connected to input 0  
`opinputpath(".", 0)` - path of the node connected to input 0 (`/obj/geo/lastNodeName`)  
`opinputpath("/obj/geo/null1", 0)` - path to the node conected to first input of null1              
`opfullpath(".")` - returns the full path of a node   
`oprelativepath("../sourcePath","../targetPath")` - Returns the relative path from one node to another      

### op:
>`op` operator is that it allows you to grab live data from another node elsewhere in your scene.

This will work as long as the data being fed in is the type of data the parameter the path to the node must be an absolute path starting from the root path:  
`op:/img/img1/gamma1` - get texture in COPs/Imp. Put as image name  
`op:/obj/cop2net1/OUT` - get texture from COP  
`op:/obj/geo/MyNode` = ``` op: `opfullpath(“../../MyNode”)` ``` - For relative path use opfullpath    
``` point("op:`opfullpath("../../null1")`","Cd",@ptnum) ``` - Copy color from points of other node  
``` s@instancepath = sprintf(op:../../var_%s, VariantEnding); ```-


### Channels/Parameters

`ch()` -   
`chf()` - float  
`chs()` - string  
`chi()` - int  
`ch3()` - matrix3  
`chramp()` - rampo  f@Cd = chramp('Cd',rand(@ptnum));   - noise ramp
`chop("../chops/OUT/chan1")` - get chop channel    

#### Rampkeys:  
```glsl
int rampkeys = chramp("ramp");

for( int i=i; i<=rampkeys; i++){
    float pos = ch(sprintf("ramp%gpos", i));
    float val = ch(sprintf("ramp%gvalue", i));
}
```

 you can interact with ramp keys just like a multiparm block. The ramp parameter itself has the value of how many keys there are:
```
c int rampkeys = chramp(“ramp”);
for( int i=i; i<=rampkeys; i++){ float pos = ch(sprintf("ramp%gpos", i));
float val = ch(sprintf("ramp%gvalue", i)); // Do stuff }
```
@flight404 (I normally don’t condone 1-based loop indices but the keys do start at 1 and not 0. I supposed you could switch to doing `i+1` in the `sprintf` calls though if you wanted)  


---

# Patterns
Pattern may be a numeric pattern, attribute pattern, or group name pattern.
`?` -  Match any character  
`*` - Match any substring  
`^` - Exclude from match  
`[list]` - Match any of the characters specified in the list.  
`!*` - ????????????  
`a*`,`^aardvark` - Match any string beginning with a except for aardvark.    
`[abc]*z` - Match any string beginning with a, b or c and ending with z.    
`g*`,`^geo*` - Match any string beginning with g, but not any string beginning with geo.    
`^pattern` - Remove matching, `0-100:2 ^10-20` every other number 1 to 100 except the 10 to 20.  
`!pattern` - Every except the ones matching the pattern. `!1-10` means every except the numbers 1 to 10.   

### Points/primitives numbered
`n` - number n.   
`n-m` - from n to m (inclusive).   
`n-m:step` - from n to m (inclusive) skipping every step. Eg; `1-100:2` every other number from 1 to 100.    
`n-m:keep,step` - from n to m (inclusive). Use the first keep numbers and then skip every step after that.    

`0-5000:2 ^ 40-200`  - range with wxceptions
`!50-200`   
`@P.y>0` - all points whose Y component is greater than   
`0*/ $BBY>.9999`     
`@id=5-10`  
`@id="5 8 10 15"` - the attribute syntax //space separated list of integer values, need to enclose the list in quotes.
`@myattr=fooBar` - by name  
`@myattr="foo bar"` - quotation marks if it contains spaces   
`=`, `==`, and `!=`  - on string attr  
`(* and ?)` -  wildcards value when using   
`{arm* ^arm3*}`  - in the pattern. includes all groups whose names start with arm, but not arm3.   


---



# Vexpression

Backticks ``` ` ``` are for use in a string field: group input, name sop. (when fn inside ??)

## ForLoop Meta Import

``` `detail(-1,"iteration",0)` ```


## Name

``` `detail(-1,"iteration",0)` ``` - name by iteration



## Group field in every SOP
`GroupName` -  work only on group  
`!GroupName` - work only on inverted group    
`@name=NameAttrib` - by string name    
`group1` -by group name  
`@name=PrimitiveStringName` - by Primitive Name  
`@name=PrimitiveStringNamePattern*` - by Primitive Name pattern  
`@name="" ` - all without names



## Group / Split

`if(@primnum == -1) @group_disconnected = 1;` - Separate points and geometry   (prims)  
`@foo>=0.5`  - by Attribute  

## Delete node




#### Delete by Pattern   
``` 0-`npoints(0)-10` ``` - Leave last 9 points   
``` 0 `npoints(0)-1` ``` - First and last   


#### Delete by Expression  
`@ptnum==@numpt-1` / `@ptnum==npoints(0)-1` / `$PT==$NPT-1` - Last     
`@ptnum%(@numpt-1)==0`  - First and last   
`prim(0, $PR, "intrinsic:closed", 0) == 1` -  Delete polygonal curves which could be translated into NURBS, and cause crash. (dlelet non selected on prims)     

## Blast
```@manifoldnumber=`opdigits(".")` ``` - will delete group by digits in node name !!! (from Polydoctor SOP)     
`@shop_materialpath="/obj*"` -     
`detail(-1,'iteration',0)` -  
`if(@primnum==-1)` - points with are not a part of prim.

## Partition
#### Rule
```group_`@shop_materialpath` ``` - Make groups from materials  




## Switch / Transform

`detail(-1,'iteration',0)%4` - loop 4 (spare)    

binary  

`npoints(-1)!=0` - switch if there is any geometry   
`if (npoints("../intersectionanalysis2/")>0,1,0)` - switch if intersected        
`if (detail(-1,'iteration',0)%2==0,1,0)` -  switch even and odds     
`if (f@burned>0)`     
`if ($F%10==0, $FF,0)` -  ?wtfoO    

`if (@Cd.r < 0.1) {  i@group_mygroup=1;  }` - change group on color    
`if ( rand(@ptnum) > ch('threshold') ) {   removepoint(0,@ptnum);  }`       




## Add

`point(-1,0,"P",0)`, `point(-1,0,"P",1)` `point(-1,0,"P",2)`- x,y,z point position from point in spare referenced node  


## Group Expression
VExpression  
`neighbourcount(0, @ptnum)<=3` - By edges count from point    
`rand(@elemnum) > chf("amount")` - Random Amount   
`@Cd.r * chf("Amount")` - Color Amount   
`@elemnum % chi("pattern")` - Modulo Pattern   
`fit01(@ptnum % chi("modulo"),0,1)` - Modulo Pattern     
`dot(@N,chv("direction")) > chf("amount")` - Vector Normal    
`rand(float(i@piece)*.89461)<.5?1:0` - Group random conected pieces  (prims)    
`@Cd.x > 0.5 && @Cd.x < 0.8`    
``` @ptnum == `npoints(0)-1` ``` - z bloga jakiegos  (last pt on curve )  




 ##  Attrib Create
 Expression field:  
`if(@attrib > 1,5,0)`  
`if(@attrib > 1,if($ATTR < 4,0,5),0)`  




## Point

Vexpression:  
`self` - pass Trough    
`value` - set Value    
`self * value `  

`lerp(self, @opinput1_P, ch('amount'))` - morph with 2 input   
`set(self.x, 0, self.z)` - flatten to z (vector)  

`set(self.x, max(self.y, ch('level') + getbbox_min(0).y), self.z)` - Flatten P    
`set(self.x, max(self.y, ch('level') + getbbox_min(0).y), self.z)` - Roatet Up N     
`lerp(self, normalize(self-getbbox_center(0)) * ch('radius') + getbbox_center(0), ch('amount'))` - Spheryphy P  

`@P - getbbox_center(0)` - Spheryphy N  
`rand(@elemnum)`  
`@opinput1_P` - second input position  


---

```

## ENV

HOUDINI_EXTERNAL_HELP_BROWSER = 1

### Textport
HScript Textport

`exhelp` - and fn.  
`help`

### Python Shell
```