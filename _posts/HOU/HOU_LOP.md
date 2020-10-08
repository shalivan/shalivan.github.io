# Solaris

Opionion strength - overrides permitionswhen merging you can use same asset and it will use one with strongero opinion  
primitive and attributes are primary container objects


### Views

scene graph tree - main wiev
scene graph layer


#### USD
Usdc - crate - geomery
Usca - ASCII - ligh and properies


#### Manage
sop name + path attribute >> USD assemlies / groups /components   
sop geometry prim groups  - usd sub components - limited in USD (face set( FOR MATERIAL ASSIGNMENT   

`composition arc` -

`layer` - a file on disk (file on disk  
`stage` - loadeld file . composed  
`references` -  
`payloads` (like refs but posible to tell not to load until they are needed  
`variant set` -  


##### Kind and selectors (RMB)

>kind usd concept with definitions :  use kind and selectors (select pratym!!!) to chose what u work on

- kind authoring (sop import)
   - all geo is one componnent
   - nested feo and groupsu

selectors:
- Leaf geometry
- Component
- Subcomponent
- Model
- Group
- Assembly
- Point Instance (top level)
- Point Instance (leaf)

### SOP to USD workflow

- sop import lop - enter path. (use nested assembly groups and components
- s@path = "/Barrels/next level/ name" + s@name; -  name change tree  ROOT !!
- s@path = "Barrels/next level/ name" + s@name; -  name change tree   RELATIVE PATHG !! (import path prefix in import sop LOP  now is dynamic(
- use assembley SOP. >>

sop create LOP:
- subset groups like attrib / groups for assign materials

#####  material library
We can assign material to whatever level of chierarchy  
Czy materiał ma być z assetem Beczka czy osobno  - Zmienić materiał Path z - materials na barrel  
jest gdzies autofill  

`material lib ?`
`material assign` (2 way to do it) - material path + asset path  !( For procedural
`material linker`  more artistic  visual

## LOP nodes
### Nodes

prune isolae
layerbreak
ediscene
save edits

sop create
sublayer - merge
reference -

instancer - add point instances (
create lod - auto lod set


- merfe
- girafe
- leyers
- layout

##### Prune
Primitive pattern - jak było dobrze podzielone to spoko  / like isolate



##### SOP Import
load as reference (*rohan do) > as payload  multiple input can import same asset only as ref.  
- import group import part of geo
- subset groups to presere groups!!!
- default import with materials on tab.

##### Material Lib
-USE  auto fill !!!!

##### Assign Material
- drag and dropem from:  Scene graph tree


##### Reference



instance
----
stage manager > to folders
collection >  (name from folder)
instancer > %foldername )and add point inside !_
-----
