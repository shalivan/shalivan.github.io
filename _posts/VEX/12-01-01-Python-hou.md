---
title: Python hou.
description: Houdini class
categories:
 - VEX
tags:
- Python
- Game Dev
- Code
---

## Setup


1. Install python 3.7.9 separately with pytorch somewhere on your machine (+add pythoin to PATH))
2. Additional libraries: instal by pip
   - `python -m pip install numpy scipy`  will instal scipy library in : **Phyton/Lib/sire-packages/...** - [Scipy](https://www.scipy.org/install.html)
3. Edit windows paths: system enviroment variables > Environment Variables... > New...
 - Variable name" `PYTHONPATH` - Variable Value: **C:\Users... Lib/site-packages** (pointing to the site-package folder. Houdini will be able to use any libs installed here.)


## Usage

###  Session Code
- `Windows/Python Source Editor/..` - **Python Source Editor** - Persistant and embeded in hip file:  .     
- `hou.session.foo()`  - Call saved code and function

- Create foo function in session:  
```python
import hou
def foo():
   foo_obj = hou.node("/obj") # go to directory
   foo_geo = foo_obj.createNode("geo", "foo_geo") # create container
   foo_box = foo_geo.createNode("box", "foo_box") # create box
```

### Shell
- `Windows/Python Shell/..` - **Live code**, which will disappear after H is closed.   

- Call foo from session:
```python
Python 2.7.15 (default, Dec  2 2020, 15:50:44) [MSC v.1916 64 bit (AMD64)] on win32
Houdini 18.5.518 hou module imported.
Type "help", "copyright", "credits" or "license" for more information.
# Call fn from Source Editor in Python Shell:
>>> hou.session.foo()
```

### Shelf  
- `RMB on Shelf` > `New Tool` -  Scripts section to write code
- can call from: `hou.session.foo()`
- You can drag and drop nodes to shelf or make new one.


### Node
- Node Script

### Node Expression
- Session code is available in expressions without `hou.session.`


### TOP
- Mapper
- Partitioner
- Processor
- Script


## Classes  

- hou.node   
- hou.objNode   
- hou.geometry   

# [hou.](https://www.sidefx.com/docs/houdini/hom/hou/index.html)
Houdini python class. (hou. - can be droped it in expressions)      

```python
# Define fn.
def childrenOfNode(node):
	result = []
	for c in node.children():
		result.appnd(c)
		result += childrenOfNode(c)
	return result

# Call defined fn by calling var: n with (node):
childrenOfNode(n)
childrenOfNode(hou.node('/obj/adress'))  
```


```python
def examplereturn(name):
   return name.upper()

# will print HOUDINI with all big captions   
print examplereturn("houdini")
```


# [hou.node](https://www.sidefx.com/docs/houdini/hom/hou/Node.html)

### Create set flags and connect nodes

**Create node** node at `/obj/foo_geo/foo_box`
-
```python
hou.node("/obj").createNode("geo",'foo_geo').createNode("box","foo_box") #
```

**Store node**
-
```python
foo_obj = hou.node("/obj") # store context
foo_geo = foo_obj.createNode("geo", "foo_geo") # create container
foo_box = foo_geo.createNode("box", "foo_box") # create box
foo_sphere = foo_geo.createNode("sphere", "foo_sphere") # create box
```
- Store existing node in varaible
```python
foo_geo_copy = hou.node('/obj/foo_geo') # store node in variable (can drag from viewport)
```

**Connect nodes**   
-
```python
foo_box.setInput(0, foo_sphere,0)
```

**Flags**
-
```python
foo_sphere.setDisplayFlag(1)   
foo_sphere.setRenderFlag(False)   
foo_sphere.isDisplayFlagSet()    
foo_sphere.isObjectDisplayed()   
foo_sphere.setSelectableInViewport(False)   
```

**Select**
-  
```python
foo_sphere = setSelected(True) #- Select ball node  
foo_sphere = isSelected() # - Return bool. Check if selected    
```

Create 2 nodes and set flags
```python
def fooFunction():
     obj = hou.node("/obj")
     foo_geo = obj.createNode("geo", "foo_geo")
     foo_box = foo_geo.createNode("box", "foo_box")
     foo_sphere = foo_geo.createNode("sphere", "foo_sphere")
     foo_box.setInput(0, foo_sphere,0) # connect inputs
     foo_sphere.setDisplayFlag(1)
     foo_sphere.setRenderFlag(1)
```

<img src="/src/python/hou/aconnectflags.png" width="350" >

**Delete**
```python
foo_box.destroy
foo_sphere.destroy
```

## Storing Parameters

```python
hou.node().param("tx") # return a parameter for this node
hou.node().paramTuple() # for multi value params
hou.node().params() # return all parameters of this node
hou.node().param("tx").eval() # return actual value of param
hou.node().evalParam("tx") # return actual value of param  
hou.node().param("tx").set(2) # set param
hou.node().param("uniformscale").set(2)
```


-----

## Get node Info   
Node **Path**
```python
foo_box.name() # '/obj/foo_geo/foo_box'
```

Node **Name** / **Type**
```python
foo_box.name() # 'foo_box' -  
foo_box.type() # <hou.NodeType for Object geo> - its object that contain info
foo_box.type().name() # 'geo' -
```
Print all parameters of node
```python
for parm in foo.parms(): # get all parameters names in ball obj
     print parm.name()
```

**Childrens**
```python
foo_geo.children() # get listo of all childrens
```  


**Print**  
```python
print foo_geo.children()
```
```python
for i in foo_geo
   print i
```


## Get inputs/outputs  
```python
foo_box.inputs()
foo_box.outputs()
```

```python
fooBox = hou.node('/obj/foo_box') # print all inputs of node
for input in foo_box.inputs():
     print input

for output in foo_box.outputs():
     print output
```





# hou.objNode
[Hou.objNode documentation](https://www.sidefx.com/docs/houdini/hom/hou/ObjNode.html)
how is displayed and how manipulate

#### Transforms
```python
parent = fooBox.parentTransform()
pre = fooBox.preTransform()
parm = fooBox.parmTransform()
world = fooBox.worldTransform()
product = parent * pre * parm
print (product == world) # True

fooBox.mmoveParmTransformIntoPreTransform()
```

# hou.parm

```python
fooTx = foo.parm("tx") # Get val of parameter  
foo.setParms({"tx":3, "tx":2, "tx":1})  
```


```python
`foo.evalParm("tx")` # Get val of parameter in particular moment  
# evalParm(path) - to access each parameter / Reference to this Python SOP via the node variable, we can use
seed = node.evalParm('seed')
threshold = node.evalParm('threshold')
```

```
evalParmTuple('t')
```

behaviour of all parameters
```python
ty = hou.parmTuple('/obj/ball/t')[1]
ty.name() # 'ty'
ty.path() # 'obj/ball/ty'
ty.eval() # 1.11111
ty.evalAtFrame(10) # 1.44324

t = ty.tuple() # list of all params
len(t) # how many params have list

for parm in t:
  print parm.name() # tx, ty, tz

ry.hou.paramTuple('/obj/ball/r')[1]
ry.deleteAllKeyFrames()
ry.set(25) # will set rotationy in 25
ry.setRxpression("2*frame()") # now will rotate in time
ry.expression() # will give you: '2*frame()'

rx = hou.parmTuple('/obj/ball/r')[0]
keys = rx.keyframes()


for key in keys: # print keys
  print key  


for key in ry.keyframes(): # print expression anims we set earlier
	print key

ry.asCode() # will print code
```


#### Attributes:

`points[index].setAttribValue("Cd",(1.0,1.0,1.0))` - Set attribute  
`redVal=point.attribValue("Cd")[0]` - Get attribute   

#### setattrib
```
geo.addAttrib(hou.attribType.Point, "PointFoo", 14)
geo.addAttrib(hou.attribType.Vertes, "VertFoo", 15)
geo.addAttrib(hou.attribType.Prim, "PrimFoo", 44)
geo.setPrimIntAttribValues("PrimFoo", (11))
```


# hou.geometry
Define 3d geo shape  `geo = node.geometry()` - grabs the geometry data that is being fed into this node by calling its geometry() method    

```python
geo = hou.node('/obj/ball/AddPointNormal').geometry()


for point in points:
		pos = point.position()


for prim in prims:
		verts = prim.vertices()
		buff = "("
		for i in range(prim.numVertices()):
			buff += dtr(verts[i].point().number()) + " "
		buff += ")"
		print "(%d -> %s)" % (prim.number(), buff)
# (0) -> (1 1 1)
# (1) -> (1 2 1)

glob = geo.globPrims("50-60:2")
for prim in glob:
		verts = prim.vertices()
		buff = "("
		for i in range(prim.numVertices()):
			buff += dtr(verts[i].point().number()) + " "
		buff += ")"
		print "(%d -> %s)" % (prim.number(), buff)
# (50) -> (1 1 1)
# (52) -> (1 2 1)
#...
# (60) -> (1 2 1)

```

#### Create points and geo

```python
node = hou.pwd()
geo = node.geometry()

# --------------------------------------------- IN SOP
# moving point

point = geo.createPoint()
point.setPosition((0,-2,0))

# --------------------------------------------- IN SOP
# create trix
poly = geo.createPolygon()
for pos in (0,0,0),(1,0,0),(0,1,0):
	point = geo.createPoint()
	point.setPosition(pos)
	poly.addVertex(point)  

```




# Groups:

`myGrp=geo.createPrimGroup('name')` - Create group   
`group.destroy()` - Delete group, leaving contents intact  

Add Point to group:
```python
point=geo.createPoint()
myGrp=geo.createPointGroup('name')
myGrp.add(point)
```

Iterate group:
```python
groups = geo.primGroups()
for group in groups:
    print group.name
```

# I/O


### import geo
`geo.loadFromFile("C:/Temp/red.geo")``



# RAW NOTES



###  Delete primitives
```
deleteList=[]
for i in boundingGrp.prims():
    deleteList.append(i)
geo.deletePrims(deleteList)
```



### Timeline keys
```
rz = hou.paramTuple("/obj/ball/r")[2]
keys = rz.keyframes()

for key in keys:
		print key

# hou.Keyframe t=0 exp="becier()" lang=exprLanguage.Python v=0 s=0 in a=0.22 out a=0.42 use_acce_ratio=True

key4 = keys[3]
key4
# hou.Keyframe t=0 exp="becier()" lang=exprLanguage.Python v=0 s=0 in a=0.22 out a=0.42 use_acce_ratio=True

key4.frame() # 10.0
key4.time() # 24.00000
key4.expression() # 'bezier()'
key4.expressionLanguage() # exprLanguage.Python
ket4.value() # 114.22
key4.slope() #-123.442
key4.accle() # 34.324
key4.setExpression("spline()",exprLanguage.Python)

key4.setValue(400) #
rz.setKeyFrame(key4) # here change in wievport
```

`param = hou.ch("param")` - Read node parameter
`xBoundSize=lvar('SIZEX')` - Read local variables    
### UI

`hou.ui.displayMessage("hello")` #display popup
`print p.selectPosition()` - print location of click in the node editor  network

create new node with box on the position under mouse
```python
p = hou.ui.paneTabOfType (hou.paneTabType.NetworkEditor)
position = p.selectPosition() #position clicked
new_node = p.pwd().createNode("box") #posWorkDir
new_node.setPosition(position)
```

### Johny

```python
node = hou.pwd()
geo = node.geometry()

for shali in geo.points():
    print shali.number()
    node = hou.node('/obj/target%s' %int(shali.number()+1))
    pos = node.evalParmTuple('t')
    rot =node.evalParmTuple('r')
    shali.setPosition(pos)
    shali.setAttribValue("rot", rot)
```



#### swap HIP to JOB


```python
def hipToJob():
    for node in hou.node("/").allSubChildren():
        if node.type().name()=="redshift::TextureSampler":
            fileJob = node.parm("tex0").rawValue().replace("$HIP","$JOB")
            node.parm("tex0").set(fileJob)
# by NickD
```



### Import

```python
import test
reload(test)
from test import *
```

# Expressions:

`frame()/4` - $F/4    
`time()` - $T  
`lvar("nameoflocalVAr")`  
`lvar("PT")` - $PT  

10/frame() * sin(frame()/10.0)
(1+ch("../ty"))/2


# Viewport States
https://www.artstation.com/siver/blog/W9PL/houdini-blog-38-viewer-states  
https://youtu.be/iMb8W2dH4hs  

https://github.com/kiryha/Houdini/wiki/python-snippets


---

See what params is passing `kwargs` (pthos dict to see what is avalable)  
special local dictionary - pass info about particular instance . created automaticly
def export_params(kwargs)
