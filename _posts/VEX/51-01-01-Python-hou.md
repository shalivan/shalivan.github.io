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


Install:  
1. Dowload a py3 release of houdini,
2. Install python 3.7.9 separately with pytorch somewhere on your machine (+add pythoin to PATH))
3. Define a the PYTHONPATH variable pointing to the site-package folder. Houdini will be able to use any libs installed here.
4. Instal additional libraries by pip
   - [Scipy](https://www.scipy.org/install.html) library - `python -m pip install numpy scipy ` will instal scipy library in : `Phyton/Lib/sire-packages/...`
5. Edit system enviroment variables > Environment Variables... > New...
 - Variable name" PYTHONPATH
 - VariableValue: `C:\Users... Lib/site-packages`

---




## Python Shell
Live code:  Windows>PythonShell
```python
 Python 2.7.15 (default, Dec  2 2020, 15:50:44) [MSC v.1916 64 bit (AMD64)] on wi
 n32
 Houdini 18.5.518 hou module imported.
 Type "help", "copyright", "credits" or "license" for more information.
 ```



```python
# Create geo container
>>> obj = hou.node("obj")
>>> obj.createNode("geo", "My_geo")
<hou.ObjNode of type geo at /obj/My_geo>
>>>
```

```python
# Store Value as variable
>>> foo = obj.createNode("geo", "My_geo")
```

```python
# Create Box inside
>>> foo.createNode("box", "My_box")
<hou.foo of type box at /obj/My_geo/My_box>
   ```



## Python Source Editor
Embeded in hip file. Can save  code and function, and call by: hou.session.myDefinedFunction()  




```python
def createSomeNodes():
   obj = hou.node("/obj")
   foo =  obj.createNode("geo", "My_Geo")
   box = foo.createNode("box", "My_Box")
```

Call fn from Source Editor in Python Shell:

```python
>>> hou.session.createSomeNodes()
```




##  Shelf Tool
Scripts section to write code Executed after shelf click



## Script node


# hou.

`hou.` is houdini python class. We can drop it in **expressions**:    
see what params is passing `kwargs` (pthos dict to see what is avalable)  



### Create function

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


# hou.node

[Hou.node documentation](https://www.sidefx.com/docs/houdini/hom/hou/Node.html)

## Operations on nodes  

```python
foo = hou.node('/path')
foo.name #return name of object.

ball = hou.node('/obj/ball') # Set ball as variable / getting a reference to the current node
ball = setSelected(True) # Select ball node
ball = isSelected() # return bool. Check if selected  
ball = type().name() # geo
ballTx = ball.parm("tx") # Get val of parameter
ball.evalParm("tx") # Get val of parameter in particular moment
ball.setParms({"tx":3, "tx":2, "tx":1})


for parm in ball.parms(): # get all parameters names in ball obj
     print parm.name()


mynode = hou.node('/obj/ball') # print all inputs of node
for input in mynode.inputs():
     print input


mynode = hou.node('/obj/ball') # print all outputs of node
for output in mynode.outputs():
     print output

# change which node input node
hou.node('/obj/nodetochange').setInput(0, hou.node('/obj.newnode'))

box = hou.node('/obj/ball').createNode("box","NewBoxName")

# create node conected to parrent
box = ball.createNode("box","NewBoxName")
box.destroy
```

evalParm(path) - to access each parameter / Reference to this Python SOP via the node variable, we can use  
```python
seed = node.evalParm('seed')
threshold = node.evalParm('threshold')
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



# hou.parm

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

# hou.objNode
how is displayed and how manipulate
```python

ball = hou.node("/obj/ball") # creates hou.ObjNode of type geo at /obj/ball

ball.setDisplayFlag(False)
ball.isDisplayFlagSet() # False
ball.isObjectDisplayed()
ball.setSelectableInViewport(False)

parent = ball.parentTransform()
pre = ball.preTransform()
parm = ball.parmTransform()
world = ball.worldTransform()
product = parent * pre * parm
print (product == world) # True

ball.mmoveParmTransformIntoPreTransform()


```

# hou.geometry
Define 3d geo shape  
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



## geometry method
`geo = node.geometry()` - grabs the geometry data that is being fed into this node by calling its geometry() method    




---
---
---
---
---
---
---
---


# RAW NOTES
### Groups:

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

### Attributes:

`points[index].setAttribValue("Cd",(1.0,1.0,1.0))` - Set attribute  
`redVal=point.attribValue("Cd")[0]` - Get attribute   

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

### setattrib
```
geo.addAttrib(hou.attribType.Point, "PointFoo", 14)
geo.addAttrib(hou.attribType.Vertes, "VertFoo", 15)
geo.addAttrib(hou.attribType.Prim, "PrimFoo", 44)
geo.setPrimIntAttribValues("PrimFoo", (11))
```
### import geo

geo.loadFromFile("C:/Temp/red.geo")

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
