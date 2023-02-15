---
title: Python unreal.
description: Unreal class
categories:
 - VEX
tags:
- Python
- Game Dev
- Code
---

https://docs.unrealengine.com/5.0/en-US/PythonAPI/

in sequener:
https://forums.unrealengine.com/t/ue4-sequencer-python-cookbook/265097

## Usage
### In Console
```python
import unreal

def log_hello():
    '''
    print to unreal log
    '''
    unreal.log("Foo")
```

### files.py in folders

content folder which have `Python` folder will be at python paths Print path to script folders:
```python
for path in sys.path
    print path
```

for file `unreal_python_test.py`:

```python
import unreal_python_test
reload(unreal_test)
import unreal_python_test
unreal_python_test.log_foo()
```

---

# Caviots

### Get/Set
There are two methods (fn vs attribute property method) to set parameter attributes that differ in visibility and settings behavior's:
1. get/set functions (as method) (or by BP) fn will:
 -   envoke post notification for editor
2. traditional set by atribute  (property method)

```python
prop = chair_asset.get_editor_property("load_for_occluder_mesh")
prop = chair_asset.set_editor_property("load_for_occluder_mesh", 1)

```



===

### console python
1. instal plugin python
2. change cmd to python > can execute python files
3. new file: python.py
```
import unreal
unreal.log("foooo")
unreal.log_warning("foooo")
```
4. copy path and past into console : `C:/..../ python.py S`

#### console REPL
- interactive codinb  
- it will show resoult without printing
- eplore python api in unrela

```

```
###
widget  > editor utility
